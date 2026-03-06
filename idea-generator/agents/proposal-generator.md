# Proposal Generator Agent

## Input

Seed content — either read from a user-provided file or generated inline by seed-generator.md.

## Step 1: Extract from the Seed(s)

If multiple seeds were generated (Seed A, B, C), read all of them and pull out:
- Domains of interest
- Frustrations, pain points, inefficiencies the user notices — across all personas
- Complaints about existing tools or services
- The users' skills and experience
- Any hints about who they'd want to build for
- Cross-persona patterns: pain points shared across seeds are stronger signals

## Step 2: Generate 8–10 Candidate Ideas

Come up with 8–10 distinct ideas. At this stage, do not apply strict filters yet — generate broadly across different user types, problem sizes, and revenue models.

Output a Markdown table in this exact format:

```markdown
| # | 名前 | ピッチ | クロスドメイン借用 | 意図的な省略 |
|---|------|--------|--------------------|--------------|
| 1 | [Product name] | [What it does and for whom] | [Mechanic borrowed from another industry + source] | [Standard feature deliberately left out] |
| 2 | ... | ... | ... | ... |
```

- **名前**: Short product name
- **ピッチ**: One-line description of what it does and for whom
- **クロスドメイン借用**: A mechanic borrowed from a completely different industry (e.g., Duolingo's streak, Airbnb's host/guest dynamic, insurance's deductible model) — must name the mechanic and its origin
- **意図的な省略**: One standard feature deliberately left out (e.g., no social feed, no notifications, no free tier)

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

## Step 4: Write Full Proposals

Write a full proposal for each selected idea using the structure in `references/proposal-template.md`.

Apply all constraints in `references/output-constraints.md`.

Each proposal must include the cross-domain mechanic and intentional omission identified in Step 2, and explain in the Overview why the omission is a strategic advantage — not just a scope cut.

After all proposals, add a ranked recommendation: which idea to build first and why. This is mandatory.
