# crane — air-gap image mirroring know-how

Why `crane` (from go-containerregistry): it's a **static binary that talks to
registries directly, with no Docker daemon** — so it works on locked-down jump hosts
where you can't (or won't) run Docker. That property is the whole reason it fits
air-gapped delivery.

## The core flow

| Step | Command | Note |
|------|---------|------|
| Extract (external network) | `crane pull <img> out.tar` | No daemon. Modern multi-arch: `--format oci` (OCI layout) |
| Carry in | move the tarball via approved media | offline transfer |
| Load (internal registry) | `crane push out.tar <registry>/<img>` | straight into Harbor/etc. |
| When a network path exists | `crane copy <src> <dst>` | registry→registry, **blob-level dedup** — only missing layers move |
| Inventory | `crane catalog <registry>` / `crane ls <repo>` | what's there / what to mirror |
| **Verify** | `crane digest <img>` | capture sha256, re-compare after import |
| Patch without rebuild | `crane mutate` / `crane rebase` | swap a base image or edit labels with no rebuild — decisive when you can't rebuild in air-gap |

## Gotchas (the actual know-how)

**1. cosign signatures don't follow the image automatically.** ⚠️ The most common
mirroring incident. Signatures/attestations live as *separate tags*
(`sha256-<digest>.sig`, `.att`). Copy only the image and verification breaks inside.
→ Mirror the `.sig`/`.att` tags too, or use `cosign copy`.

**2. Pin by digest, not tag.** Reference `<img>@sha256:...` rather than `:tag` for
reproducibility and to catch tampering. For a specific arch use
`--platform linux/amd64`; to preserve a full multi-arch index, `crane copy` it
(digest preserved).

**3. `crane copy` preserves digests** (it copies blobs as-is), which is why
signatures survive a clean copy. `crane mutate` changes the digest — a mutated,
previously-signed image needs re-signing.

**4. Helm OCI charts mirror the same way** — charts are OCI artifacts, so `crane copy`
moves them too.

## Scripting pattern

A bulk mirror is a loop: read an image list → `pull` → record `digest` →
`push` → re-check `digest` after import. End with a **digest match + image-count
check** — that final verification is what prevents silent layer-drop on import.

> Version note: the exact default behavior of `crane pull` for multi-arch and the
> `--format` options vary by crane version. Confirm with `crane version` before
> finalizing a mirror script — verify, don't assume.
