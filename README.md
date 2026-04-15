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

## Vendored collections

**25 upstream collections mirrored into `skills/`** — clone this repo and
every skill is immediately available offline, with pinned upstream SHAs for
reproducible refresh. See [STRUCTURE.md](./STRUCTURE.md) for the full tree.

### Claude Code skills (high-star MIT collections)
| Collection | Path | Count | Upstream |
|---|---|---|---|
| **232+ Claude skills mega-collection** | `skills/alirezarezvani-claude-skills/` | 232+ | [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) |
| **66 full-stack developer skills** | `skills/fullstack-skills-66/` | 66 | [Jeffallan/claude-skills](https://github.com/Jeffallan/claude-skills) |
| **Multi-agent orchestration** | `skills/wshobson-agents/` | 33k★ | [wshobson/agents](https://github.com/wshobson/agents) |
| **Anthropic first-party** | `skills/claude/` | 13 + spec + template | [anthropics/skills](https://github.com/anthropics/skills) |
| **oaustegard curated** | `skills/oaustegard-skills/` | 114★ | [oaustegard/claude-skills](https://github.com/oaustegard/claude-skills) |
| **CLAUDE.md generator** | `skills/claudeforge/` | 346★ | [alirezarezvani/ClaudeForge](https://github.com/alirezarezvani/ClaudeForge) |

### Design skills
| Collection | Path | Upstream |
|---|---|---|
| **Superdesign Product Design Agent** | `skills/superdesign/` | [B12Labs/superdesign](https://github.com/B12Labs/superdesign) |
| **Superdesign skill** | `skills/superdesign-skill/` | [B12Labs/superdesign-skill](https://github.com/B12Labs/superdesign-skill) |
| **Apple HIG Designer** | `skills/apple-hig-designer/` | [axiaoge2/Apple-Hig-Designer](https://github.com/axiaoge2/Apple-Hig-Designer) |
| **DESIGN.md collection from popular sites** | `skills/awesome-design-md/` | [cendien/boss-agents-awesome-design-md](https://github.com/cendien/boss-agents-awesome-design-md) |
| **Design articles → skill** | `skills/designskills-01/` | [cendien/boss-skills-designskills-01](https://github.com/cendien/boss-skills-designskills-01) |
| **Taste / aesthetic judgment** | `skills/taste-skill/` | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) |
| **Graphify — AI coding + design** | `skills/graphify/` | [cendien/boss-skills-graphify](https://github.com/cendien/boss-skills-graphify) |

### Developer / engineering skills
| Collection | Path | Upstream |
|---|---|---|
| **Android apps (modern)** | `skills/android-skill/` | [dpconde/claude-android-skill](https://github.com/dpconde/claude-android-skill) |
| **Planning with files (Manus-style)** | `skills/planning-with-files/` | [OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files) |
| **Docs → skill converter** | `skills/skill-seekers/` | [yusufkaraaslan/Skill_Seekers](https://github.com/yusufkaraaslan/Skill_Seekers) |
| **Godot game projects** | `skills/godogen/` | [htdt/godogen](https://github.com/htdt/godogen) |
| **Prompt Architect — vague → structured** | `skills/prompt-architect/` | [ckelsoe/prompt-architect](https://github.com/ckelsoe/prompt-architect) |
| **Scientific / research / engineering** | `skills/scientific-skills/` | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) |

### SEO / marketing skills
| Collection | Path | Upstream |
|---|---|---|
| **Claude SEO (19 sub-skills)** | `skills/claude-seo/` | [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) |
| **Agentic SEO analysis** | `skills/agentic-seo/` | [Bhanunamikaze/Agentic-SEO-Skill](https://github.com/Bhanunamikaze/Agentic-SEO-Skill) |

### Domain / business skills
| Collection | Path | Upstream |
|---|---|---|
| **Bankr banker skills** | `skills/banker-skills/` | [idenis/banker-skills](https://github.com/idenis/banker-skills) |
| **Career ops (AI job search, 14 modes)** | `skills/career-ops/` | [cendien/boss-agents-career-ops](https://github.com/cendien/boss-agents-career-ops) |
| **Official GLM family skills** | `skills/glm-skills/` | [idenis/GLM-skills](https://github.com/idenis/GLM-skills) |

### Agent systems
| Collection | Path | Upstream |
|---|---|---|
| **Agency Agents — 172 roles, 15 divisions** | `skills/agency/<division>/` | [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) |
| **Canopy — agent workspace protocol** | `skills/canopy/` | [idenis/canopy](https://github.com/idenis/canopy) |

### Reference index
| Collection | Path | Upstream |
|---|---|---|
| **Awesome Agent Skills** (curated link list) | `skills/awesome-agent-skills/` | [idenis/awesome-agent-skills](https://github.com/idenis/awesome-agent-skills) |

**Every vendored collection carries** its own `UPSTREAM-README.md`, `LICENSE`
(or `LICENSE-<origin>`), and `.upstream-sha` so we can tell exactly what we
pulled and when.

**Source-available skills from `anthropics/skills`** (docx / pdf / pptx /
xlsx) are deliberately NOT vendored — Anthropic permits personal use and
reference but not redistribution. See
[`skills/claude/SOURCE-AVAILABLE-SKIPPED.md`](./skills/claude/SOURCE-AVAILABLE-SKIPPED.md)
for how to pull them locally.

### Why vendored everything?

The goal is **"clone the repo on a new computer and be productive
immediately"** — no hunting across 25 upstream repos, no broken network
fetches, no rediscovery of what works. One `git clone https://github.com/B12Labs/skills`,
full kit.

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
