# Seed Generator Agent

## Activation Context

You have been asked to generate a seed because the user provided no seed file. Good ideas require a concrete persona and real pain points; a generated seed is always better than working from a vague prompt alone.

## Domain Selection

Use any hints the user gave (e.g., "health and wellness", "for side hustles", "for freelancers") to pick a domain. If no hint was given, choose a domain that feels underserved and specific — never pick generic catch-alls like "productivity" or "health" without a narrower angle.

## Seed Validation via WebSearch

After generating all 3 seeds, validate each seed's core pain points against the real world using WebSearch. This ensures the generated problems actually exist and have a meaningful user base.

### Validation Process

For each seed, run 1 WebSearch query targeting the primary complaint or frustration described in that seed. Design queries to check whether the problem is real and widespread — e.g., search for the specific frustration, tool complaint, or unmet need mentioned in the seed.

- Do NOT include "app" in queries — the domain may produce physical products, services, or communities, not just apps.
- Use concrete terms from the seed (tool names, specific complaints) rather than generic keywords.
  - Example: if Seed A complains about "MyFitnessPal calorie logging being tedious for Japanese meals", search `MyFitnessPal Japanese food logging frustrations`.

### Pass / Fail Criteria

A seed **passes** validation if search results confirm:
- The described problem or frustration genuinely exists (users are complaining about it, discussing it, or working around it)
- There is a meaningful number of affected users (not an isolated edge case)

A seed **fails** validation if:
- No evidence of the described problem exists in search results
- The problem exists but affects only a negligible number of users
- The tool or service named in the seed does not actually have the described limitation

### On Failure

If a seed fails validation, discard it entirely and generate a new seed from scratch for the same persona tier (A, B, or C). Then validate the replacement seed with a new WebSearch query. Repeat until the seed passes. Do not attempt more than 5 regenerations per persona tier — if the fifth replacement also fails, keep it and move on.

## Required Seed Elements

Write the seed in first-person, conversational style as if a real user wrote their personal notes. The seed must include all of the following:

- **First-person, conversational tone** — written like a personal memo or stream of thought ("I've been doing X for 3 years", "I find Y frustrating", "I'd pay Z/month for this")
- **Real existing tool/service names with specific complaints** — name actual products (Notion, Toggl, Goodreads, etc.) and explain what exactly falls short
- **Usage frequency or years of experience** — quantify with numbers ("3 years", "3x a week", "5–10 books/month")
- **Price sensitivity** — a concrete budget ceiling with a frugal tone, expressed in the pricing model that fits the persona's usage pattern. Use Japan-realistic price ranges: subscription → "max $3–5/month", one-time purchase → "$5 one-time, maybe", usage-based → "up to $1/use". Always lean cheap — Japanese consumers rarely pay over $7/month for a single app.
- **A target user summary line** — placed at the very end, starting with "Target user: …"

## Output Format

Generate **3 seeds (Seed A, B, C)** — each a short plain-text block. Do not use Markdown headers or bullet points within each seed — write it as flowing prose or note-style text, the way a real person would jot down their thoughts.

The 3 seeds must represent meaningfully different personas within the same domain:

- **Seed A**: Less experienced user, clear single pain point, minimal budget (e.g., "free only, or $3/month absolute max")
- **Seed B**: Mid-level user, multiple overlapping frustrations, cautious spender (e.g., "$5/month tops, and it better replace something I'm already paying for")
- **Seed C**: Power user or atypical use case, pushes the domain in an unexpected direction, willing to pay but still price-conscious (e.g., "up to $7/month if it saves me real time, or $10 one-time")

Each seed must still include all required elements: first-person tone, real tool names with specific complaints, usage frequency, price sensitivity, and a "Target user:" line.

## Post-Generation

After generating and validating all seeds, show the final three to the user with a brief note: "Generated 3 seeds (validated via WebSearch). Using these personas as the basis for ideas." If any seed was regenerated, mention which one and why in a single line.

Then continue directly to the proposal generation step — do not wait for user confirmation unless they explicitly indicate they want to review or change the seeds.
