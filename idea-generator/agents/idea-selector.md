# Idea Selector Agent

## Input

The candidate idea table produced by candidate-generator.md (Step 2).

## Step 3: Select the Top 3 Ideas

Evaluate all candidates and select exactly 3 using the six filters below.

**Filters (score each 1–3):**

- **Speed (Scope & Effort)**: Can a solo developer ship a core MVP in 2-4 weeks? (1 = requires months, heavy backend, or complex ML; 3 = doable in weeks, mostly frontend/simple logic)
- **Diff**: Clear angle vs. existing products (1 = me-too, 3 = meaningfully different)
- **Moat (Defensibility)**: If a giant competitor (e.g., Cookpad, Kurashiru) copies this UI in a 2-week sprint, do we survive? (1 = easily crushed/just a UI gimmick; 3 = survives via unique niche, data lock-in, or specific community focus)
- **Reten (Retention & Monetization)**: Is there a painful, undeniable reason for users to _keep paying_ month after month? (1 = high churn risk, one-and-done utility, nice-to-have; 3 = deep lock-in, recurring pain solver)
- **Build**: No exotic dependencies or prohibitive costs (1 = high risk, 3 = low risk)
- **Risk (Liability & Ops)**: Are there legal, medical, or heavy ongoing data-maintenance dependencies? (1 = high liability like allergy/health/finances, or manual DB updates; 3 = low risk, zero to minimal external dependencies)

Output a Markdown table in this exact format:

```markdown
| Idea   | Speed | Diff | Moat | Reten | Build | Risk | Total  | Decision                           |
| ------ | :---: | :--: | :--: | :---: | :---: | :--: | :----: | ---------------------------------- |
| [Name] |   3   |  3   |  3   |   3   |   3   |  3   | **18** | ✅ Selected                        |
| [Name] |   2   |  2   |  2   |   2   |   2   |  2   |   12   | ❌ [One-line reason for rejection] |
```

Exactly 3 ideas must have `✅ Selected`. If scores are tied, prefer the idea with higher Diff.
After the table, add a one-sentence note explaining any non-obvious tie-breaking decisions.
