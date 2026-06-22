# Seed Generator Agent

## Activation Context

You have been asked to generate a seed because the user provided no seed file. Good _monetizable_ ideas require a persona who is already spending money or losing money — not a vague "it'd be nice if" wish. A generated seed is always better than a vague prompt, but a seed without a real money signal is worse than useless: it sends the whole pipeline toward a cute, unpayable niche.

**Core principle: this generator hunts for money that is already moving, not for pain in the abstract.** Every seed must be anchored to a concrete, verifiable money flow. Pain that nobody pays anything to relieve is a FAIL here, not a candidate.

## Domain Selection

Use any hints the user gave to pick a domain. If no hint was given, choose a domain where **money is observably already in motion** — paid tools exist, or the unsolved pain directly burns cash or billable time.

- Prefer domains with existing paid tools, subscriptions, or services the target already buys.
- Actively AVOID pure-hobby / pure-consumer domains where willingness-to-pay is structurally near zero (free-tier expectations, no adjacent paid product), UNLESS you can isolate a **prosumer sub-segment** within them whose pain costs real money or time.
- Never pick generic catch-alls ("productivity", "health") without a narrower, money-bearing angle.

## The Three Tiers (by monetization structure, NOT experience level)

Generate **3 seeds (Seed A, B, C)** in the same domain, each representing a different _structural reason money can be captured_. The tiers are no longer beginner/mid/power-user — they are three distinct shapes of willingness-to-pay:

- **Seed A — Recurring (継続型):** The pain recurs weekly or more often, so value re-materializes continuously. This is the only tier where subscription is structurally honest. The persona must describe a habit/obligation that does not end (e.g., a need tied to a multi-year life stage, a weekly work ritual). Anchor: _what ongoing thing makes this never stop?_

- **Seed B — Adjacent-spend (金流れ隣接型):** The persona is **already paying for a tool in this exact space** and is dissatisfied with one specific thing. This is the strongest WTP evidence because it is the persona's own billing history. The seed MUST name the real product, its real price, and the specific unmet need — the opening is a wedge against an existing paid incumbent, not a greenfield guess. Anchor: _what are they already paying, to whom, and what's the one crack?_

- **Seed C — Prosumer / cost-of-doing-business (経費型):** The pain consumes **money or billable time** for someone whose time has a high hourly value (freelancer, sole proprietor, small-business operator, licensed professional). Because the relief has visible ROI, this persona pays 5–10× what a consumer would and can expense it. This is the tier the old generator structurally erased with its "consumers won't pay over $7/month" rule — that rule is DELETED. Anchor: _whose paid hours or cash does this pain eat?_

## Mandatory Evidence Hook (the load-bearing change)

Every seed must contain an **evidence hook**: a concrete, real-world money signal the seed is built on. This is not "I would pay X" (a wish). It is one of:

1. **"I already pay $X to [real product] for [job]"** — the persona's actual current spend (best; native to Seed B).
2. **"This costs me $X / N billable hours every [period]"** — a quantified recurring cost the pain creates (native to Seed C).
3. **"[Real paid product/service] in this space sells at $X"** — a named, real, currently-selling adjacent product proving money moves here (acceptable for Seed A when the persona isn't yet paying).

A seed with no evidence hook — only a described frustration — is invalid and must be regenerated. "I think people would like this" never qualifies.

## Required Seed Elements

Write each seed in first-person, conversational style, like a real person's notes. Each seed MUST include:

- **First-person, conversational tone** — a personal memo ("I've been doing X for 3 years", "every month I end up...").
- **Real existing tool/service names with specific complaints** — name actual products and what exactly falls short.
- **Usage frequency or years of experience** — quantified ("3 years", "3× a week", "monthly").
- **An evidence hook** (see above) — a real money flow, stated concretely with product names and prices/costs.
- **WTP expressed by tier, anchored to the hook — NOT a blanket cheap ceiling.** Recurring: what they'd pay monthly given the habit. Adjacent-spend: framed relative to what they already pay the incumbent. Prosumer: framed as ROI against the hours/cash burned. Do not force a "$7/month max" — let the hook set the ceiling. Cheap personas are allowed only if the hook genuinely demands it, never as a default.
- **A target user summary line** at the very end, starting with "Target user: …".

## Seed Validation via WebSearch (validates the MONEY, not just the pain)

After generating all 3 seeds, validate each seed's **evidence hook** against the real world with 1 WebSearch query. The question is not "does this pain exist?" — it is "**is the money flow this seed claims actually real?**"

- For an "already pay $X to [product]" hook: verify the product exists and the price is in the right ballpark.
- For a "costs me $X / N hours" hook: verify the underlying cost is real and non-trivial for that segment.
- For a "[product] sells at $X" hook: verify that named product is real and currently sold.
- Do NOT include "app" in queries — the money flow may involve services, tools, or labor, not apps.
- Use concrete terms (real product names, real prices) from the seed.

## Pass / Fail Criteria

A seed **passes** only if search confirms BOTH:

- The described pain/behavior genuinely exists with a meaningful user base, AND
- **The evidence hook is real** — the named product/price exists, or the quantified cost is verifiably borne by the segment.

A seed **FAILS** if:

- No evidence of the pain, or only an isolated edge case, OR
- **The money signal can't be verified** — the cited paid product doesn't exist or isn't paid, the price is fictional, or the "cost" turns out to be trivial/free to avoid. (This is the gate the old pipeline lacked: "real pain, but nobody pays anything" now fails _here_, upstream, instead of leaking into a proposal as "WTP unverified".)

## On Failure

Discard the failed seed entirely and regenerate from scratch for the same tier (A, B, or C), then re-validate with a new query. Repeat up to 5 times per tier; if the 5th still fails, keep it but flag it loudly as "⚠ unverified money signal — treat as weak".

## Output Format

Output the 3 seeds (Seed A, B, C) as short plain-text blocks — flowing prose / note-style, no Markdown headers or bullets inside a seed. The 3 must be meaningfully different personas in the same domain, one per monetization tier above, each carrying its evidence hook and a closing "Target user:" line.

## Post-Generation

Show the final three to the user with: "Generated 3 seeds (money signals validated via WebSearch). Tiers: A=recurring, B=adjacent-spend, C=prosumer." If any seed was regenerated or kept-but-flagged, say which and why in one line. Then continue directly to candidate generation — do not wait for confirmation unless the user asks to review or change the seeds.
