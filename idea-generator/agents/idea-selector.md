# Idea Selector Agent

## Input

The candidate idea table produced by candidate-generator.md.

## Select the Top 3 Ideas

Evaluate all candidates and select exactly 3 using the six filters below.

**Filters (score each 1–3):**

- **Speed (Scope & Effort)**: Can a solo developer ship a core MVP in 2-4 weeks? (1 = requires months, heavy backend, or complex ML; 3 = doable in weeks, mostly frontend/simple logic)
- **Diff**: Clear angle vs. existing products (1 = me-too, 3 = meaningfully different)
- **Moat (Defensibility)**: If a giant competitor (e.g., Cookpad, Kurashiru) copies this UI in a 2-week sprint, do we survive? (1 = easily crushed/just a UI gimmick; 3 = survives via unique niche, data lock-in, or specific community focus)
- **Mono (Monetization)**: Is there a clear, defensible path to revenue under the model best suited to the product's usage pattern? Pick the strongest fit from: **subscription** (recurring need weekly+), **one-time purchase** (infrequent but high-stakes events), or **usage-based/pay-as-you-go** (variable frequency). _CRITICAL RULE: Do NOT propose ad-supported or two-sided marketplaces, as they require unrealistic scale/liquidity for a solo MVP._ (1 = unclear how to monetize or model mismatch with usage pattern; 2 = plausible but thin; 3 = obvious path with strong WTP under the chosen model)
- **Build**: No exotic dependencies or prohibitive costs (1 = high risk, 3 = low risk)
- **Risk (Liability & Ops)**: Are there legal, medical, or heavy ongoing data-maintenance dependencies? (1 = high liability like allergy/health/finances, or manual DB updates; 3 = low risk, zero to minimal external dependencies)

**⚠️ Time-to-value trap**: If an idea's core value only materializes after 2+ weeks of consistent user behavior (e.g., daily logging streaks, data accumulation), cap Mono at 2 — unless the MVP includes a Day-1 hook that delivers a clear insight or "aha" moment on first use (e.g., surfacing a known baseline pattern immediately, instant before/after comparison, or a result visible within session 1). "Users will keep logging for 30 days" is not a valid assumption; most B2C users drop off within 3 days.

**⚠️ One-shot trap**: If the product's core use case is tied to an infrequent life event (e.g., job interviews, moving, weddings, tax filing), do NOT choose subscription — choose one-time purchase or usage-based instead. If no non-subscription model yields clear WTP, cap Mono at 1.

**⚠️ Clone trap**: If the competitor-checker flagged an idea as "High" overlap with an existing product and the Key Difference is trivial (e.g., minor UI change, same concept for a slightly different audience), cap Diff at 1. "Medium" overlap caps Diff at 2 unless the rationale identifies a concrete, defensible angle the existing product lacks.

**⚠️ Graduation trap**: If the product's core value proposition is teaching a behavior or mindset (e.g., "change one habit per week," "learn to track your skin"), cap Moat at 2 — users will internalize the lesson within weeks and cancel without guilt. A strong Moat requires something the app keeps doing better than the user can do alone (e.g., continuous data the user cannot replicate manually, a community, or personalization that compounds over time).

**Step A — Write rationale first (before scoring).** For each candidate idea, write one bullet per filter axis with a short factual reason. Incorporate the competitor-checker results when assessing Diff. Flag any trap that applies. Example:

```markdown
**Rationale:**

- IdeaA:
  - Speed: frontend-only, no backend needed
  - Diff: no direct competitor in JP
  - Moat: UI easily copied, no data lock-in
  - Mono: one-shot use (One-shot trap → one-time purchase)
  - Build: no external API
  - Risk: no legal/health concerns
- IdeaB:
  - Speed: requires ML pipeline...
```

**Step B — Score based on the rationale.** Convert each reason to 1–3 and fill in the table. If the rationale says "requires external data" then Build must not be 3. Scores must be consistent with the rationale written in Step A.

Output the score table in this exact format:

```markdown
| Idea | Speed | Diff | Moat | Mono | Build | Risk | Total | Decision |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [Name] | 3 | 3 | 3 | 3 | 3 | 3 | **18** | ✅ Selected |
| [Name] | 2 | 2 | 2 | 2 | 2 | 2 | 12 | ❌ [One-line reason for rejection] |
```

Exactly 3 ideas must have `✅ Selected`. If scores are tied, prefer the idea with higher Diff.
After the table, add a one-sentence note explaining any non-obvious tie-breaking decisions.
