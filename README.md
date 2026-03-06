# idea-generator

A Claude Code skill that generates structured product and service proposals from a seed file.

## Skill

### `/idea-generator [product-or-service]`

Reads a seed file (interests, pain points, domain notes) and outputs product or service proposals in Markdown. Works for any type of product — mobile apps, web services, SaaS tools, physical products, and more. Tech stack and implementation details are intentionally out of scope.

**If no seed file is provided**, the skill generates 3 personas (Seed A/B/C) inline before producing proposals.

```
/idea-generator seeds/my-domain.txt
```

**Each proposal includes:**
- Target Audience table
- Core Features (MVP / Phase 2)
- Monetization Strategy with pricing table
- Go-to-Market Phases table
- Risks & Mitigations
- Competitive Landscape
- Scorecard with star ratings
- Ranked recommendation summary

## Repository structure

```
idea-generator/
├── SKILL.md                        # Orchestrator — flow control only
├── agents/
│   ├── seed-generator.md           # Seed auto-generation logic
│   ├── candidate-generator.md      # Extracts signals and generates 8–10 candidate ideas
│   ├── idea-selector.md            # Scores candidates and selects exactly 3
│   └── proposal-writer.md          # Writes full proposals for selected ideas
├── references/
│   ├── proposal-template.md        # Markdown template for each proposal
│   └── output-constraints.md       # Non-negotiable output rules
└── evals/
    ├── evals.json                  # Eval cases (3 total)
    └── files/
        └── seed-fitness.txt        # Eval seed — strength training

seeds/                              # Output directory for generated seeds (gitignored)
```

## Seed files

Seeds are short, first-person notes written in a conversational tone. Each seed must include:

- At least one real existing product/tool name with a specific complaint
- Usage frequency or years of experience
- Price sensitivity (monthly or annual amount)
- A `Target user: ...` line at the end

`seeds/` is gitignored. Only the handwritten seeds under `evals/files/` are tracked.
