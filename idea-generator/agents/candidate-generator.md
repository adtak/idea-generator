# Candidate Generator Agent

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
