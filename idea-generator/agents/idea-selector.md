# Idea Selector Agent

## Input

The candidate idea table produced by candidate-generator.md (Step 2).

## Step 3: Select the Top 3 Ideas

Evaluate all candidates and select exactly 3 using the four filters below.

**Filters (score each 1–3):**
- **Scope**: MVP one person can ship within ~3 months (1 = unrealistic, 3 = clearly doable)
- **Diff**: Clear angle vs. existing products (1 = me-too, 3 = meaningfully different)
- **Mono**: Believable revenue route (1 = unclear, 3 = obvious path)
- **Build**: No exotic dependencies or prohibitive costs (1 = high risk, 3 = low risk)

Output a Markdown table in this exact format:

```markdown
| Idea | Scope | Diff | Mono | Build | Total | Decision |
|------|:-----:|:----:|:----:|:-----:|:-----:|----------|
| [Name] | 3 | 3 | 3 | 3 | **12** | ✅ Selected |
| [Name] | 2 | 2 | 2 | 2 | 8 | ❌ [One-line reason for rejection] |
```

Exactly 3 ideas must have `✅ Selected`. If scores are tied, prefer the idea with higher Diff.
After the table, add a one-sentence note explaining any non-obvious tie-breaking decisions.
