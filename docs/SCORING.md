# Scoring — One-shot Success Rate

## The metric

For any skill invocation by a Persona or AI session:

```
one_shot = (
  1 if the skill finished all exit_criteria on first execution
  else 0
)

one_shot_rate = sum(one_shot) / count(invocations)
```

High one-shot rate = skill's scope is well-bounded AND planner-vocabulary
matches the task it's dispatched for. Low rate = some combination of
fuzzy scope, bad planner match, or under-specified exit criteria.

This is **Boil-the-Lake, quantified.**

## Why it matters

- **For skill authors:** a skill with one-shot rate < 0.6 is telling you
  either the scope is too wide or the description is misleading the
  planner. Fix the SKILL.md before adding more scripts.
- **For Persona evolution:** a Persona's aggregate one-shot rate across
  many skill invocations is a core fitness signal in the evolution loop
  (see `reference_minimax_evolution.md` in BOSS memory). High-fit Personas
  pick skills more accurately AND describe their goals in language that
  matches skill descriptions.
- **For planner tuning:** if two skills have overlapping capabilities but
  very different one-shot rates against the same task type, the lower-rate
  one probably has description drift — update it.

## How to detect retries

Two signals:

1. **Edit → Bash → Edit loops** in Claude Code / Codex traces (the
   [CodeBurn](https://github.com/AgentSeal/codeburn) detector heuristic).
   A session that writes, runs tests, fails, rewrites, re-runs is a retry.
2. **Multiple skill invocations on the same task** where the first
   invocation's exit criteria weren't met. Must be tracked by the
   dispatcher (BOSS Personas session ledger).

Both signals get rolled up into the same `one_shot_rate` metric.

## What "first try" means

First try does NOT mean zero iteration inside a single skill execution.
A skill can do write → test → fix → write → test → pass AS ONE INVOCATION
— that's the skill doing its own QA loop, which is exactly what QA skills
(e.g. gstack `qa`) are supposed to do.

First try means: **the skill finished on the first dispatch of it for this
task** — no retry dispatches against a different skill, no re-dispatching
the same skill after the first gave up, no caller bailing to manual
intervention.

## Thresholds we care about

- **`>= 0.85`** — the skill is dialed in, leave it alone
- **`0.70 – 0.85`** — the skill works but has edge cases. Add a `Not for:`
  section to the SKILL.md.
- **`0.50 – 0.70`** — the scope is probably too wide. Consider splitting
  into two narrower skills.
- **`< 0.50`** — the skill is actively misleading the planner. Revise the
  description urgently or deprecate.

## Related reading

- [CodeBurn](https://github.com/AgentSeal/codeburn) — the open-source tool
  that introduced the one-shot detector on Claude Code transcripts
- [gstack ETHOS](https://github.com/garrytan/gstack/blob/main/ETHOS.md) —
  where Boil-the-Lake comes from
- `reference_minimax_evolution.md` in BOSS memory — the Persona evolution
  loop that uses this metric as its fitness signal
