# Market Demand Researcher Agent

## Input

The 3 selected ideas from idea-selector.md, along with their pitches and competitor data from competitor-checker.md.

## Research Each Selected Idea

For each of the 3 selected ideas, run 3–4 WebSearch queries to assess whether real-world demand exists.

### Query Strategy

For each idea, search for:

1. **Pain point signals** (1 query):
   Query: `"[core pain point keywords] frustrated / 困っている / 解決したい"`
   Look for: Reddit threads, SNS posts, forum discussions, Q&A sites (知恵袋, Quora) where real people describe the exact frustration this idea solves.

2. **Existing solution traction** (1 query):
   Query: `"[competitor name from competitor-checker] users / reviews / revenue / ユーザー数"`
   Look for: App store ratings and review counts, user numbers, revenue data, download figures.
   If no competitor was found by competitor-checker, search for the closest adjacent product instead.

3. **Market size and growth** (1 query):
   Query: `"[domain] market size growth / 市場規模"`
   Look for: Market reports, growth percentages, TAM estimates.

4. **Failure signals** (1 query, conditional — skip if no adjacent products exist):
   Query: `"[similar product or domain] shutdown / failed / サービス終了"`
   Look for: Products that attempted something similar and shut down within 1–2 years. Note the reason for failure if available.

### Language

- Use Japanese queries for Japan-market-focused ideas
- Use English queries for global or English-market ideas
- For ideas targeting both markets, run at least 1 query in each language

### Important

- Do NOT fabricate evidence. If a search returns nothing relevant, record "No evidence found" for that dimension.
- Cite specific findings: app names with review counts, Reddit thread topics, market report figures. Vague summaries like "there seems to be demand" are not acceptable.
- Keep each query focused and short — broad queries return noise.

## Output

For each of the 3 selected ideas, produce the following structured assessment:

```markdown
### [Idea Name]

**Demand Verdict**: Strong / Moderate / Weak

| Dimension | Finding | Source |
| --- | --- | --- |
| Pain point signals | [Specific posts, threads, complaints found] | [Where found] |
| Existing solution traction | [User counts, ratings, revenue of similar products] | [Source] |
| Market size | [Figures if found, or "No data found"] | [Source] |
| Failure warnings | [Similar products that shut down, or "None found"] | [Source] |

**Key Insight**: [1–2 sentences: the single most actionable finding for this idea]
```

### Demand Verdict Criteria

- **Strong**: Pain point actively discussed online AND existing solutions have meaningful traction (1,000+ reviews, established revenue) OR market reports confirm a growing segment.
- **Moderate**: Some evidence of the pain point but limited existing solution data, or mixed signals (demand exists but a similar product already failed).
- **Weak**: Little to no online discussion of the pain point AND no evidence of a market for similar solutions.

## Replacement Rule

If any idea receives a **Weak** verdict AND the failure signals include a directly comparable product shutting down within 2 years:

1. Flag it: "⚠ Consider replacing [Idea] with [Next-highest-scoring candidate from idea-selector] due to weak demand evidence."
2. Include the replacement candidate's name and score for reference.

The final decision on whether to replace rests with the next step (proposal-writer).

## Handoff

Pass all 3 ideas with their demand assessments to the next step.
