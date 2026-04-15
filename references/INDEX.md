# External skill libraries — index

Skills we study, don't vendor here. Link + one-line "why it matters to us"
+ license so the planner and humans can dig deeper.

## Canonical references

### [garrytan/gstack](https://github.com/garrytan/gstack)
- **Stars:** 72k+ · **License:** MIT · **Lang:** TS + shell + MD
- **Why:** Origin of Boil-the-Lake philosophy. 23 opinionated skills named
  like job titles (CEO, Designer, Eng Manager). Every skill has a SKILL.md
  + scripts + templates.
- **How BOSS uses it:** 7 core skills vendored into
  `boss-platform/lib/personas/skills/_reference/gstack/` (autoplan,
  plan-eng-review, qa, design-review, ship, retro, checkpoint) + the
  philosophy docs.

### [conorluddy/ios-simulator-skill](https://github.com/conorluddy/ios-simulator-skill)
- **Stars:** 788 · **License:** MIT · **Lang:** Python + shell
- **Why:** The canonical file shape for a SKILL.md + scripts/ + references/
  layout. Our own template is derived from this.
- **Requires:** macOS + Xcode 16. Not runnable in BOSS's Linux/Windows fleet.
- **How BOSS uses it:** shape reference only. When we land macOS build
  infra, we'll promote it to a runtime skill under `skills/ios-simulator`.

### [anthropics/skills](https://github.com/anthropics/skills)
- **License:** MIT
- **Why:** Anthropic's first-party skill collection — `webapp-testing`,
  `frontend-design`, `pdf-generation`, `xlsx-parser`. Sets the official
  SKILL.md spec that clients like Claude Code implement.
- **How BOSS uses it:** format compliance baseline. Our SKILL-SHAPE.md tracks
  any changes to the upstream spec.

## Adjacent references

### [AgentSeal/codeburn](https://github.com/AgentSeal/codeburn)
- **Stars:** 909 · **License:** MIT · **Lang:** TypeScript
- **Why:** Introduced the one-shot success rate detector that we use in
  `docs/SCORING.md`. 13-category task classifier + LiteLLM pricing cache.
- **How BOSS uses it:** metric + patterns (not runtime). Task classifier
  + one-shot detector slated for port into `boss-platform`'s /spend page.

### [block/goose](https://github.com/block/goose)
- **Stars:** 42k · **License:** Apache 2.0 · **Lang:** Rust + TS
- **Why:** Declarative provider adapter pattern (drop a JSON file =
  add a provider). Not a skill library per se but the composability
  philosophy overlaps.
- **How BOSS uses it:** Council router adopted the declarative JSON
  adapter pattern for 19 LLM providers.

## How to add to this index

1. The library must be public and OSS-licensed (MIT / Apache / BSD / GPL
   acceptable; AGPL / PolyForm-NC flagged but not excluded).
2. Entry format: heading → stars, license, lang → why → how BOSS uses it.
3. Keep sections alphabetical within categories.
4. Link to the repo's root, not a deep file (deep links rot).
5. "Why" must be specific — not "cool AI skills library" but "introduces
   the one-shot detector we use for scoring."
