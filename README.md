# s3onghyun-soul

**The *soul* of a DevOps/Platform consultant — the temperament and judgment, not just the skills.**

Most agent configs tell an LLM *what to do*. This one defines *who it is while
doing it*: evidence-first, root-cause-killing, calm, and honest enough to correct
itself out loud and refuse to oversell. It encodes a real engineer's working style —
**[s3onghyun](https://github.com/s3onghyun)** — so an assistant doesn't just have the
knowledge, it has the *disposition* you'd want from a teammate.

> The idea behind it: on real teams, the person you **trust** beats the person who's
> merely brilliant. So this persona optimizes for *trusted* — verify before you
> answer, kill the cause not the symptom, hand back something runnable, own your
> mistakes, and don't perform.

## What's a "soul" (vs a skill)?

A **skill** is a capability: "generate a Terraform module," "write a regex." A
**soul** is the character that decides *how* every task gets done — values, voice,
judgment, boundaries. Same model, very different colleague. This repo follows the
emerging soul/persona convention (a structured markdown directory separating the
*who* from the *what*) and ships in the formats people actually load.

## What's in here

| File | Purpose |
|------|---------|
| [`SOUL.md`](SOUL.md) | Identity, values, working style, decision heuristics, boundaries — the core. |
| [`STYLE.md`](STYLE.md) | Voice & formatting: calm/plain, table-first (결정·차선책·비추), functional KO/EN, the explicit-correction move. |
| [`TOOLING.md`](TOOLING.md) | The toolchain it reaches for — and how it **asks you to add a skill/MCP when the work needs one**. |
| [`MEMORY.md`](MEMORY.md) | Session continuity — decisions, learned preferences, follow-ups it appends as it works (public-safe; no sensitive data). |
| [`examples/good-outputs.md`](examples/good-outputs.md) | What it sounds like working (verify → table → recommend → honest). |
| [`examples/bad-outputs.md`](examples/bad-outputs.md) | Off-soul anti-patterns to avoid (fabrication, hype, silent edits, scope creep). |
| [`.claude/agents/s3onghyun.md`](.claude/agents/s3onghyun.md) | Ready-to-use **Claude Code subagent** (drop-in). |
| [`soul.json`](soul.json) | Manifest for portability/discovery. |

## Install / use

**Claude Code (subagent):**
```bash
git clone https://github.com/s3onghyun/s3onghyun-soul
mkdir -p ~/.claude/agents
cp s3onghyun-soul/.claude/agents/s3onghyun.md ~/.claude/agents/
# then: "use the s3onghyun subagent to review this pipeline"
```

**Any other LLM / Cursor / Continue / a CLAUDE.md:** paste or include `SOUL.md` +
`STYLE.md` + `TOOLING.md` (and the `examples/` for calibration) into your system
prompt / rules file. It's plain markdown — no runtime required.

## It asks for its own tools

A real engineer has reflexes about *which* tool fits *which* moment — and says when
they're missing one. This persona does too: if work would go better with a skill or
MCP it doesn't have, it tells you ("this is an OTel Collector config — it'd be cleaner
with the otelcol-doctor skill that validates the output; want to enable it?") instead
of soldiering on with the wrong tool. See [`TOOLING.md`](TOOLING.md). It composes
naturally with task skills like the author's own
**[otelcol-doctor](https://github.com/s3onghyun/otelcol-doctor)** — the *soul* decides
how to work; the *skill* supplies the validated steps.

## The persona, in one table

| | |
|---|---|
| **Strong at** | GitLab CI/CD & Runners · Observability (Prometheus/Grafana/Loki/Tempo/Mimir/OpenTelemetry) · K8s/Helm/ArgoCD · Harbor · air-gap (crane) |
| **Defaults to** | settling questions with a tool (validator / MCP / rendered diff), not assertion |
| **For recurring failures** | kills the root cause, not the symptom |
| **Communicates in** | a 결정·차선책·비추 table, then a clear recommendation |
| **When wrong** | says "Correcting my earlier answer:" — and won't oversell its own work |
| **On any handed-off task** | shares progress before you ask — never goes silent and makes you wonder |
| **Optimizes for** | being trusted, not impressive |

## Honest scope

This is a *persona*, and personas help most when they're **tightly relevant**.
Research on persona prompting shows that padding a persona with irrelevant detail can
actually *hurt* task performance — so this one deliberately stays in the
DevOps/Platform lane it earns, and skips biographical filler. It won't make a model
omniscient; it makes it *behave like a specific, trustworthy engineer*.

## Disclaimer & privacy

- This repository is a **persona** published by [s3onghyun](https://github.com/s3onghyun).
  It represents a working style — **not the real person's live judgment**, employer, or
  any specific engagement.
- It is built **only from publicly shareable working style**. It contains **no client
  names, credentials, internal URLs, or sensitive data**, by design, and never will.
- Self-authored; consent is self-satisfied. Use it as a helpful colleague-shaped
  prompt, not as a representation that the real person endorses any particular output.

## License

[MIT](LICENSE). Attribution appreciated.
