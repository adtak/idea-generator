# Cheap Gate (reasoning only — NO WebSearch)

## Input

One drafted idea from idea-drafter.md.

## Purpose

Kill obviously-doomed ideas using reasoning alone, BEFORE any search budget is spent. This gate is what makes the loop affordable — most bad ideas must die here, at zero search cost. Do NOT use WebSearch in this gate.

## Two kill checks (fail either → KILL)

1. **Buildable solo in 2-4 weeks.** KILL if the core honestly needs a heavy backend, a trained ML model, regulated-data handling, a large content/data library that must be maintained, or two-sided liquidity. A thin client over an existing API is fine; a platform is not.

2. **Differentiated beyond repackaging.** KILL if the idea is an obvious me-too of a product you already know exists, or if its only "edge" is being iOS-only / a nicer UI over something a well-known incumbent already does. (If a giant could clone it in a two-week sprint and the idea has no niche, data, or positioning angle to survive that — it dies here.)

Reason from what you already know. If you find yourself unsure whether an incumbent already owns this, that is NOT a reason to pass it — flag it and let the expensive gate verify; but if you already know an incumbent owns it, KILL now.

## Output

```markdown
**Cheap gate**: PASS → expensive gate   |   KILL — [which check, one-line reason]
**Closeness**: [1-5] — [if killed: how close it was, for best_so_far tracking]
```

If PASS, hand off to gate-saturation.md. If KILL, return to the loop controller.
