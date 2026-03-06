# Competitor Checker Agent

## Input

The candidate idea table produced by candidate-generator.md.

## Step: Check Each Candidate for Existing Competitors

For each candidate idea, search for existing products with similar scope:

1. Use WebSearch to query `"[candidate name or pitch keywords] app"` or `"[candidate name or pitch keywords] service"`.
2. Identify 0-3 existing products that overlap with the candidate's target audience and core value proposition.
3. Assess overlap level using the criteria below.

**Overlap criteria:**

- **High**: An existing product targets the same audience and delivers 80%+ of the same core features. Switching cost for the user would be minimal.
- **Medium**: Same domain but a meaningfully different approach, target segment, or feature set. The candidate has a plausible angle the existing product lacks.
- **Low / None**: No directly competing known product found, or existing products serve a substantially different need.

## Output

Produce the following table with one row per candidate. Do NOT remove any candidates — annotate only.

```markdown
| # | Candidate | Existing Competitor(s) | Overlap | Key Difference (if any) |
| --- | --- | --- | --- | --- |
| 1 | [Name] | [Product A], [Product B] | High | [差分があれば記載] |
| 2 | [Name] | None found | None | — |
```

Pass all candidates (with annotations) to the next step.
