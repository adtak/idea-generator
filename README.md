# idea-generator

A Claude Code skill that generates structured iOS app proposals from a seed file.

## Skill

### `/idea-generator [seed-file]`

Reads a seed file (interests, pain points, domain notes) and outputs iOS app proposals in Markdown, assuming an Expo + AWS stack throughout.

**If no seed file is provided**, the skill generates a persona and pain points inline before producing proposals.

```
/idea-generator seeds/my-domain.txt
```

**Each proposal includes:**
- Target Audience table
- Core Features (MVP / Phase 2)
- Monetization Strategy with pricing table
- AWS architecture table
- Development Phases table
- Scorecard with star ratings
- Ranked recommendation summary

**Fixed tech stack:**

| Layer | Technology |
|-------|------------|
| Frontend | Expo (React Native) + TypeScript, Expo Router, Zustand / TanStack Query |
| Backend | AWS Lambda + API Gateway, DynamoDB, S3, Cognito |

## Repository structure

```
idea-generator/
├── SKILL.md                   # Skill definition
└── evals/
    ├── evals.json             # Eval cases (5 total)
    └── files/
        ├── seed-fitness.txt   # Eval seed — strength training
        ├── seed-reading.txt   # Eval seed — reading
        └── seed-freelance.txt # Eval seed — freelance

seeds/                         # Output directory for generated seeds (gitignored)
```

## Seed files

Seeds are short, first-person notes written in a conversational tone. Each seed must include:

- At least one real existing app/tool name with a specific complaint
- Usage frequency or years of experience
- Price sensitivity (monthly or annual amount)
- A `Target user: ...` line at the end

`seeds/` is gitignored. Only the handwritten seeds under `evals/files/` are tracked.
