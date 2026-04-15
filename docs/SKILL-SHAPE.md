# Canonical SKILL.md shape

Every skill in this repo — and in BOSS's consuming registry — follows this
file structure. Adopted from `conorluddy/ios-simulator-skill` (the de-facto
gold standard in the community) with small BOSS-specific additions.

## File tree

```
skills/<skill-slug>/
├── SKILL.md           ← required: frontmatter + prose
├── scripts/           ← optional: executable tools the skill provides
│   ├── <name>.py
│   └── <name>.sh
├── references/        ← optional: agent-facing cheat-sheets
│   └── <topic>.md
└── examples/          ← optional: golden-path invocation examples
    └── <scenario>.md
```

## SKILL.md frontmatter (required)

```yaml
---
name: <kebab-case-slug>          # filename-safe, lowercase, hyphens only
version: 1.0.0                   # semver
description: One line, <200 chars. Written for the PLANNER (Claude) — be specific about when to use it, not marketing copy.
capabilities:
  - <tag>                        # what this skill does in agent vocabulary
  - <tag>
requires:
  - <prereq>                     # prereqs that must be true at dispatch
author: <handle or name>
license: MIT                     # override per-skill if needed
source: https://github.com/B12Labs/skills
---
```

### Field details

- **`name`** — stable slug, never rename. Users' configurations reference it.
- **`version`** — bump patch on doc fixes, minor on capability additions,
  major on breaking changes to scripts or invocation shape.
- **`description`** — the planner's selector. This is the single most
  important line in the file. Rewrite it until it's precise.
- **`capabilities[]`** — agent-side vocabulary:
  - `planning`, `code-review`, `ui-critique`, `ship`, `qa-tests`,
    `retrospective`, `context-consolidation`, `browser-control`,
    `api-integration`, `security-scan`, `persona-evolution`, etc.
  - Use the same vocabulary across skills so the planner can match.
- **`requires[]`** — hard preconditions: `node-22`, `macos`, `docker`,
  `supabase-auth`, `vercel-cli`, `boss-persona-session`, etc. If a
  prereq isn't met, the skill MUST NOT run.
- **`license`** — MIT unless a specific skill has different constraints
  (vendored from GPL upstream, etc.).

## Body (required sections)

```markdown
# <Skill Name>

## What this skill does

Two to four sentences. Written for the planner, not for humans reading
docs. Include:
- When this skill is the right choice (vs. similar ones)
- What outcome the caller should expect
- The lake this fills

## Scripts

Table of every script in `scripts/` with one-line purpose + invocation.

| Script | Purpose | Invocation |
|---|---|---|
| `scripts/<name>` | one-liner | `node scripts/<name>.ts <args>` |

## References

List of files in `references/` — these get read into the planner's
context when the skill is activated.

## Safety / side effects

Any operation that:
- Mutates shared state (R2, Supabase, GitHub)
- Sends network traffic (and to where)
- Costs money (LLM calls, external API calls)
- Requires elevated permissions

Personas running under auto-approve policies check this before
executing.

## Exit criteria (boil-the-lake specific)

What does "done" look like? Be explicit:
- [ ] Test added
- [ ] Doc updated
- [ ] Commit with WHY
- [ ] ...

If a planner can't verify all boxes, the skill didn't finish — it
bailed.

## Example invocation

```ts
await runSkill({
  persona: '<persona-id>',
  skill: '<skill-slug>',
  args: { /* ... */ },
});
```
```

## Optional sections

- **Related skills** — links to skills that come before / after this one
  in typical workflows
- **Evolution** — how this skill has changed (scope expansions, narrower
  specializations) — if tracked
- **Not for** — explicit non-use cases to help the planner avoid
  mismatching

## Quality checklist before merging a new skill

- [ ] `description` is under 200 chars and agent-specific
- [ ] `capabilities[]` uses existing vocabulary (or adds a new one
      justified in the PR)
- [ ] `requires[]` is exhaustive — no implicit prereqs
- [ ] Scripts are executable (`chmod +x`) and documented in the table
- [ ] Exit criteria are listed and verifiable
- [ ] Boil-the-Lake: does this skill have a narrow lake? If the scope
      is "generic helper", split it.
