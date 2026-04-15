---
name: skill-slug-here
version: 0.1.0
description: One-line capability summary (<200 chars) written for the PLANNER — precise wins over clever. State when to use it, not marketing copy.
capabilities:
  - example-capability-tag
requires:
  - node-22
author: B12 Labs
license: MIT
source: https://github.com/B12Labs/skills
---

# Skill Name

## What this skill does

Two to four sentences written for the planner. Include:
- When this skill is the right choice (vs. similar ones in the registry)
- What outcome the caller should expect
- The lake this fills (in Boil-the-Lake terms)

## Scripts

| Script | Purpose | Invocation |
|---|---|---|
| `scripts/example.ts` | one-liner | `node scripts/example.ts <arg>` |

## References

- `references/quick.md` — short cheat sheet the planner reads on activation
- `references/patterns.md` — common usage patterns with code

## Safety / side effects

List any operations that mutate shared state, hit external APIs, cost money,
or require elevated permissions. Personas check this before auto-running.

## Exit criteria

What does "done" look like? Be explicit:

- [ ] <outcome 1>
- [ ] <outcome 2>
- [ ] Tests added if applicable
- [ ] Doc updated if behavior changed
- [ ] Commit message explains WHY

## Example invocation

```ts
import { runSkill } from '@/lib/personas/engine';

await runSkill({
  persona: '<persona-id>',
  skill: 'skill-slug-here',
  args: { /* ... */ },
});
```

## Not for

- <explicit non-use case 1>
- <explicit non-use case 2>

## Related skills

- Before this: `<skill-that-typically-runs-first>`
- After this: `<skill-that-typically-runs-after>`
- Alternatives: `<similar-skill>` — when to pick that one instead
