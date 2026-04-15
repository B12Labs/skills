# B12 Labs — Skills

A curated registry of **AI coding / agent skills** organized around the
**"Boil the Lake"** philosophy: do the complete small thing, not the
incomplete large thing.

Used by [BOSS](https://boss.ceo) and [Cintrico](https://cintrico.com) to
equip AI agents, Personas, and Claude Code sessions with narrow, reliable,
composable capabilities.

---

## The "Boil the Lake" Principle

> A *lake* is boilable — 100% test coverage for a module, full migration,
> complete doc coverage.
> **Boil lakes. Flag oceans as out of scope.**

This is the inverse of the consulting phrase "boil the ocean" (trying to do
too much). It says: when AI makes the marginal cost near-zero, **don't trim
80% of a task to save effort** — the savings are tiny and you leave a tail
of rework. Don't expand into the sea — flag it and ship the lake you
defined.

Every skill in this repo follows this principle. Each skill has:

- A **narrow, named purpose** (one thing, done completely)
- **Explicit preconditions + postconditions**
- **Clear exit criteria** (you know when it's done)
- **Retrospection hooks** (how did it go, what's next)

See [`docs/BOIL-THE-LAKE.md`](./docs/BOIL-THE-LAKE.md) for the full
derivation and operating rules.

---

## Repo structure

```
B12Labs/skills/
├── README.md                ← this file
├── LICENSE                  ← MIT
├── docs/
│   ├── BOIL-THE-LAKE.md     ← the philosophy in detail
│   ├── SKILL-SHAPE.md       ← canonical SKILL.md structure we use
│   └── SCORING.md           ← one-shot success rate + Persona evolution
├── skills/                  ← BOSS-authored, first-class skills
│   ├── _template/           ← copy this to start a new skill
│   │   └── SKILL.md
│   └── (future: persona-evolution, security-scan, etc.)
└── references/              ← links to external skills we study
    └── INDEX.md
```

---

## Canonical skill shape

Every skill is a directory containing at minimum a `SKILL.md` with this
frontmatter:

```yaml
---
name: <kebab-case-slug>
version: 1.0.0
description: One line, <200 chars. Agents read this to decide relevance — be specific.
capabilities:
  - <tag>
requires:
  - <prerequisite>
license: MIT
---
```

See [`docs/SKILL-SHAPE.md`](./docs/SKILL-SHAPE.md) for the full spec
(scripts, references, safety notes, example invocation).

---

## Vendored collections (under `skills/`)

Two large upstream collections are mirrored into this repo so agents can
load them directly without network fetches:

| Collection | Path | Count | License | Upstream |
|---|---|---|---|---|
| **Claude Skills** (Anthropic) | `skills/claude/` | 13 + spec + template | Apache 2.0 | [anthropics/skills](https://github.com/anthropics/skills) |
| **Agency Agents** (roles) | `skills/agency/<division>/` | 172 across 15 divisions | MIT | [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) |

Each vendored collection carries its own `UPSTREAM-README.md`, `LICENSE` (or
`LICENSE-<origin>`), and `.upstream-sha` so we can tell exactly what we
pulled and when.

**Source-available skills from `anthropics/skills`** (docx / pdf / pptx /
xlsx) are deliberately NOT vendored — Anthropic permits personal use and
reference but not redistribution. See
[`skills/claude/SOURCE-AVAILABLE-SKIPPED.md`](./skills/claude/SOURCE-AVAILABLE-SKIPPED.md)
for how to pull them locally.

---

## References we study (don't vendor here)

These libraries are linked but not duplicated — their content is large,
fast-moving, or specialized in ways that reference (not vendor) fits better:

| Source | Purpose | License |
|---|---|---|
| [garrytan/gstack](https://github.com/garrytan/gstack) | 23 opinionated Claude Code skills, origin of Boil-the-Lake | MIT |
| [conorluddy/ios-simulator-skill](https://github.com/conorluddy/ios-simulator-skill) | Canonical shape for scripts + references + SKILL.md layout | MIT |
| [anthropics/skills](https://github.com/anthropics/skills) | Anthropic's upstream skill examples | MIT |

Full index in [`references/INDEX.md`](./references/INDEX.md).

---

## How BOSS consumes these skills

BOSS [Personas](https://boss.ceo/personas) are digital workforce actors
with role, identity, memory, and **a skill registry**. The skills in this
repo plug into that registry via capability tags. At runtime, a Persona
given a task picks the skill whose `capabilities[]` best match the task
type, then executes the skill's scripts.

This repo is the **canonical source** — BOSS pulls from here rather than
authoring skills inside `boss-platform`, so the library stays portable,
open-source, and reusable across Cintrico products + external contributors.

---

## Contributing

This library grows with the BOSS team and community. To add a skill:

1. Copy `skills/_template/` to `skills/<your-skill-name>/`
2. Edit `SKILL.md` frontmatter + body
3. Add scripts (`scripts/*`) and references (`references/*.md`) as needed
4. PR against `main`

Every PR must pass the "Boil the Lake" check: does this skill have a clear,
narrow purpose with explicit exit criteria? If the description is "generic
helper" or the scope is fuzzy, it doesn't belong here — split it into
multiple skills or rename.

---

## License

MIT — see [`LICENSE`](./LICENSE). Every skill file retains this license
unless an individual `SKILL.md` declares a different one in its frontmatter.
