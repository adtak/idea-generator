# Proposal Generator Agent

## Input

Seed content — either read from a user-provided file or generated inline by seed-generator.md.

## Step 1: Extract from the Seed

Read the seed and pull out:
- Domains of interest
- Frustrations, pain points, inefficiencies the user notices
- Complaints about existing tools or services
- The user's skills and experience
- Any hints about who they'd want to build for

## Step 2: Generate 3–5 Ideas

Come up with 3–5 distinct ideas. Each must pass all four filters:

- **Scope**: MVP one person can ship within ~3 months — keeps the project realistic for a solo builder; ideas that require a team or years of work are out
- **Differentiation**: A clear angle that isn't just "existing product + minor tweak" — without a meaningful difference, there's no reason for users to switch
- **Monetization path**: A believable route to revenue (subscription, freemium, one-time, ads) — validates that the idea has a business model, not just utility
- **Buildable**: No exotic dependencies or prohibitive upfront costs — reduces the risk of getting blocked before launch

## Step 3: Write the Proposals

Write a full proposal for each idea using the structure in `references/proposal-template.md`.

Apply all constraints in `references/output-constraints.md`.

After all proposals, add a ranked recommendation: which idea to build first and why. This is mandatory.
