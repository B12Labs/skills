# Boil the Lake

## The principle in one sentence

When AI makes the marginal cost of completeness near-zero, **do the complete
small thing, not the incomplete large thing.**

---

## The origin

The phrase comes from Garry Tan's [gstack](https://github.com/garrytan/gstack)
ETHOS, which reformulates the consulting cliché "boil the ocean" (trying to
do everything, accomplishing nothing) into its constructive inverse:

> Lake vs. ocean: A "lake" is boilable — 100% test coverage for a module,
> full migration, complete doc coverage. Boil lakes. Flag oceans as out of
> scope.

Read Garry's original: https://garryslist.org/posts/boil-the-ocean

---

## Why it matters now

Before LLMs, "do the complete thing" was expensive because writing extra
code, extra tests, extra docs took linear human time. So we scoped tasks
small AND incomplete (tested the happy path, skipped error handling,
deferred docs).

With AI assistance, the marginal cost of "complete" collapses:

| Task type | Human-only time | AI-assisted time | Speedup |
|---|---|---|---|
| Boilerplate / scaffolding | 2 days | 15 min | ~100x |
| New feature on known stack | 3 days | 4 hours | ~10x |
| Refactor with good tests | 1 day | 1 hour | ~10x |
| Novel research | 1 week | 4 days | ~2x |

In the first three rows, **completeness is nearly free.** Not writing tests
is no longer a time-saver; it's just tech debt you're choosing to carry.
Not writing docs isn't a time-saver either.

So: **pick a smaller scope and fill it completely.**

---

## Operating rules

### 1. Scope the lake up front

Before writing any code, state in one paragraph:

- What is the lake? (What exactly am I finishing?)
- What is the ocean? (What am I explicitly NOT doing this session?)
- What does "complete" look like? (What are my exit criteria?)

If you can't write this paragraph, your scope is still fuzzy. Narrow it.

### 2. Filling the lake means ALL of:

- The code path works end-to-end for the happy case
- Reasonable error handling for the sad cases
- Tests that exercise both (where a test harness exists)
- A doc update if behavior or API changed
- A commit message that explains the WHY, not just the what

### 3. Explicit ocean-flags

If during the work you hit something that should be done but is outside the
lake, don't pivot into it. Write an ocean-flag:

```
TODO(ocean): the FooBar API also needs pagination but that's out of scope
for this PR — filed as #123.
```

Flagging protects the lake you committed to without losing the signal.

### 4. One-shot success rate is the KPI

A Persona (or AI session) that retries and rewrites is boiling the ocean —
they scoped too wide, got tangled, and had to restart. A Persona that
nails it first try scoped the lake well.

See [`SCORING.md`](./SCORING.md) for how we measure this.

### 5. Don't boil the lake AND the adjacent lake

Sometimes the instinct is "well, while I'm here I should fix this other
small thing." Resist. That's two lakes, not one. Ship one, come back for
the other.

---

## Anti-patterns

These are the shapes of oceans we've seen:

- **"Quick refactor while I'm here"** — expands scope without changing
  exit criteria. Now you have two tasks, shipping worse than one.
- **"Skip tests this round"** — tests are the cheapest part of the lake.
  Not writing them is what tech debt actually is.
- **"Nail the architecture first"** — architecture emerges from shipping
  2-3 lakes. Don't boil architecture before you've shipped a lake.
- **"Touch everything so the scope is clearly reviewed"** — the bigger the
  PR, the worse the review. Smaller lake, higher signal per commit.
- **"It's mostly working"** — error paths count. "Mostly working" is the
  modal state of tech debt.

---

## Applied to BOSS

**Persona skills** — Every skill in this repo is a defined lake. A skill
that's vague or broad gets split or renamed.

**Agent evaluation** — Personas are scored on one-shot success rate (did
they complete their lake first try). High rates correlate with good lake
scoping by the Persona's author.

**Product work on `boss-platform`** — Every PR answers: "what lake did this
fill?" Commits with multiple lakes are unacceptable.

**AI Engine Intelligence Dream Cycles** — Memory consolidation uses
Boil-the-Lake: one Persona, one session, full consolidation — not
"process half this user's memory and come back tomorrow."

---

## Why NOT ever boil the ocean

Because the tail of rework on a 70%-done ocean is bigger than a fully-done
lake. An ocean half-filled is just a marsh — you can't walk on it and you
can't sail in it.

You already know this. The only question is whether you scope it
explicitly at the start or regret it at the end.
