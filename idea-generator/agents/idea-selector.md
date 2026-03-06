# Idea Selector Agent

## Input

The candidate idea table produced by candidate-generator.md (Step 2).

## Step 3: Select the Top 3 Ideas

Evaluate all candidates and select exactly 3 using the six filters below.

**Filters (score each 1–3):**

- **Speed (Scope & Effort)**: Can a solo developer ship a core MVP in 2-4 weeks? (1 = requires months, heavy backend, or complex ML; 3 = doable in weeks, mostly frontend/simple logic)
- **Diff**: Clear angle vs. existing products (1 = me-too, 3 = meaningfully different)
- **Moat (Defensibility)**: If a giant competitor (e.g., Cookpad, Kurashiru) copies this UI in a 2-week sprint, do we survive? (1 = easily crushed/just a UI gimmick; 3 = survives via unique niche, data lock-in, or specific community focus)
- **Mono (Monetization)**: Is there a clear, defensible path to revenue — subscription or high-value one-time? (1 = unclear how to monetize, weak WTP; 2 = plausible but thin; 3 = obvious path — strong subscription lock-in OR one-time with a clear loss-aversion trigger like "cheaper than one mistake")
- **Build**: No exotic dependencies or prohibitive costs (1 = high risk, 3 = low risk)
- **Risk (Liability & Ops)**: Are there legal, medical, or heavy ongoing data-maintenance dependencies? (1 = high liability like allergy/health/finances, or manual DB updates; 3 = low risk, zero to minimal external dependencies)

**⚠️ Time-to-value trap**: If an idea's core value only materializes after 2+ weeks of consistent user behavior (e.g., daily logging streaks, data accumulation), cap Mono at 2 — unless the MVP includes a Day-1 hook that delivers a clear insight or "aha" moment on first use (e.g., surfacing a known baseline pattern immediately, instant before/after comparison, or a result visible within session 1). "Users will keep logging for 30 days" is not a valid assumption; most B2C users drop off within 3 days.

**⚠️ Graduation trap**: If the product's core value proposition is teaching a behavior or mindset (e.g., "change one habit per week," "learn to track your skin"), cap Moat at 2 — users will internalize the lesson within weeks and cancel without guilt. A strong Moat requires something the app keeps doing better than the user can do alone (e.g., continuous data the user cannot replicate manually, a community, or personalization that compounds over time).

Output a Markdown table in this exact format:

```markdown
| Idea   | Speed | Diff | Moat | Mono  | Build | Risk | Total  | Decision                           |
| ------ | :---: | :--: | :--: | :---: | :---: | :--: | :----: | ---------------------------------- |
| [Name] |   3   |  3   |  3   |   3   |   3   |  3   | **18** | ✅ Selected                        |
| [Name] |   2   |  2   |  2   |   2   |   2   |  2   |   12   | ❌ [One-line reason for rejection] |
```

Exactly 3 ideas must have `✅ Selected`. If scores are tied, prefer the idea with higher Diff.
After the table, add a one-sentence note explaining any non-obvious tie-breaking decisions.
