# Repo Structure

Complete directory tree of B12Labs/skills. Use this as the map when
browsing the repo or when deciding where to add new content.

```
B12Labs/skills/
│
├── README.md                           ← start here
├── STRUCTURE.md                        ← you are here
├── LICENSE                             ← MIT
│
├── docs/                               ← our own philosophy + specs
│   ├── BOIL-THE-LAKE.md                ← core philosophy
│   ├── SKILL-SHAPE.md                  ← canonical SKILL.md structure
│   └── SCORING.md                      ← one-shot success rate metric
│
├── references/
│   └── INDEX.md                        ← external reference library links
│
└── skills/                             ← ALL vendored + authored skills
    │
    ├── _template/                      ← copy this to start a new skill
    │
    ├── ── VENDORED: CLAUDE CODE SKILLS ──
    ├── alirezarezvani-claude-skills/   ← 11k★ MIT — 232+ skills, MEGA COLLECTION
    ├── fullstack-skills-66/            ← 8k★ MIT — 66 full-stack dev skills
    ├── wshobson-agents/                ← 33k★ MIT — multi-agent orchestration
    ├── oaustegard-skills/              ← 114★ MIT — curated Claude skills
    ├── claudeforge/                    ← 346★ MIT — CLAUDE.md generator & maintainer
    ├── claude/                         ← Apache 2.0 — 13 Anthropic first-party skills
    │                                     (docx/pdf/pptx/xlsx linked, not vendored)
    │
    ├── ── VENDORED: DESIGN ──
    ├── superdesign/                    ← B12Labs — AI Product Design Agent
    ├── superdesign-skill/              ← B12Labs — superdesign as a skill
    ├── apple-hig-designer/             ← 108★ MIT — Apple HIG design skill
    ├── awesome-design-md/              ← Cendien — DESIGN.md collection from popular sites
    ├── designskills-01/                ← Cendien — design articles as skill
    ├── taste-skill/                    ← Leonxlnx — taste / aesthetic judgment skill
    ├── graphify/                       ← Cendien — AI coding assistant skill
    │
    ├── ── VENDORED: DEVELOPER / ENGINEERING ──
    ├── android-skill/                  ← 170★ MIT — modern Android apps
    ├── planning-with-files/            ← 18k★ MIT — Manus-style markdown planning
    ├── skill-seekers/                  ← 12k★ MIT — docs→skill converter
    ├── godogen/                        ← 2.8k★ MIT — Godot game projects
    ├── prompt-architect/               ← 107★ MIT — vague prompts → structured briefs
    ├── scientific-skills/              ← 18k★ MIT — research / science / engineering
    │
    ├── ── VENDORED: SEO / MARKETING ──
    ├── claude-seo/                     ← 4.8k★ MIT — 19 SEO sub-skills + 12 subagents
    ├── agentic-seo/                    ← 367★ MIT — LLM-first SEO analysis
    │
    ├── ── VENDORED: DOMAIN / BUSINESS ──
    ├── banker-skills/                  ← Bankr — plug-and-play banker tools
    ├── career-ops/                     ← Cendien — AI job search, 14 skill modes
    ├── glm-skills/                     ← Official Z.ai skills for GLM family models
    │
    ├── ── VENDORED: AGENT SYSTEMS ──
    ├── agency/                         ← 172 role-based agents across 15 divisions
    │   ├── academic/                    (5)
    │   ├── design/                      (8)
    │   ├── engineering/                 (29)
    │   ├── finance/                     (5)
    │   ├── game-development/            (5)
    │   ├── marketing/                   (30)
    │   ├── paid-media/                  (7)
    │   ├── product/                     (5)
    │   ├── project-management/          (6)
    │   ├── sales/                       (8)
    │   ├── spatial-computing/           (6)
    │   ├── specialized/                 (41)
    │   ├── strategy/                    (3)
    │   ├── support/                     (6)
    │   └── testing/                     (8)
    ├── canopy/                         ← AI agent workspace protocol
    │
    └── ── VENDORED: REFERENCE INDEX ──
        └── awesome-agent-skills/       ← idenis — curated link list of 1000+ agent skills
```

## By vendor source

| Org / User | Collections |
|---|---|
| **anthropics** | claude/ (13 skills + spec + template) |
| **B12Labs** (this org) | superdesign/, superdesign-skill/ |
| **Cendien** | designskills-01/, graphify/, awesome-design-md/, career-ops/ |
| **alirezarezvani** | alirezarezvani-claude-skills/ (232+), claudeforge/ |
| **wshobson** | wshobson-agents/ |
| **AgriciDaniel** | claude-seo/ |
| **Jeffallan** | fullstack-skills-66/ |
| **K-Dense-AI** | scientific-skills/ |
| **dpconde** | android-skill/ |
| **axiaoge2** | apple-hig-designer/ |
| **ckelsoe** | prompt-architect/ |
| **Bhanunamikaze** | agentic-seo/ |
| **OthmanAdi** | planning-with-files/ |
| **htdt** | godogen/ |
| **yusufkaraaslan** | skill-seekers/ |
| **oaustegard** | oaustegard-skills/ |
| **msitarzewski** | agency/ (172 agents) |
| **Leonxlnx** | taste-skill/ |
| **idenis** | banker-skills/, GLM-skills/, canopy/, awesome-agent-skills/ |

## Total inventory

- **~25 vendored collections**
- **500+ individual skill/agent definitions** (counting by SKILL.md files + role markdown files)
- **~164 MB** vendored content
- **~11,800 files**
- All with `.upstream-sha` pinned for reproducible refresh

## How to add a new vendored collection

1. Pick a slug (kebab-case, short)
2. `git clone --depth 1 https://github.com/<upstream> /tmp/<slug>`
3. Copy into `skills/<slug>/` excluding `.git` + `node_modules` + `dist`
4. Save `/tmp/<slug>/LICENSE` or `LICENSE-<source>` into the vendored dir
5. Write `git rev-parse HEAD` output to `skills/<slug>/.upstream-sha`
6. Add a row to this STRUCTURE.md under the appropriate category
7. Add to `references/INDEX.md` with "How BOSS uses it" note
8. Commit with message: `vendor: <slug> from <upstream@sha>`

## How to promote a vendored skill to first-class

When a specific vendored skill is ready to become a BOSS-authored skill
(with BOSS-specific frontmatter, scripts, and capability tags):

1. Copy `skills/<vendor>/<skill>/` to `skills/<promoted-name>/`
2. Edit the SKILL.md frontmatter to use BOSS vocabulary:
   - `capabilities:` use our canonical tag set (see docs/SKILL-SHAPE.md)
   - `requires:` include BOSS-specific preconditions if any
   - `license:` keep upstream license
   - `source:` point back to the vendored original
3. Remove anything unnecessary for BOSS use (upstream examples, tests that
   don't apply, etc.)
4. Add to the "BOSS-authored" section of the README (to be created when
   we have our first promoted skill)

## Goal

Clone this repo on a new machine, and a Claude Code / Codex / Cursor
session with any of its agents immediately has access to hundreds of
proven skills. No hunting across multiple repos. No rediscovery of what
works. One `git clone`, full kit.
