---
name: idea-generator
description: |
  Generates product and service ideas from a seed file or domain hint, and outputs structured project proposals in Markdown.
  Covers any type of product or service — mobile apps, web services, SaaS tools, physical products, and more.
  Produces proposals covering target audience, core features, monetization strategy, go-to-market phases, and competitive landscape.
  Tech stack and implementation details are intentionally out of scope.

  TRIGGER: Use this skill whenever the user wants to brainstorm product or service ideas, generate a
  project proposal, or turn a seed file into a concrete concept — even if they phrase it casually like
  "I want to build something" or "give me product ideas" or "help me figure out what to make."
argument-hint: "[product-or-service]"
disable-model-invocation: true
allowed-tools: Read, Write
---

# Product & Service Idea Generator

Generate actionable, scoped product and service ideas from a seed file and output full project proposals
in Markdown. Designed for solo builders who will design, build, and ship alone.

## Process

### Step 0: Seed Generation (when no seed file is provided)

Check whether the user has provided a seed file path.

**If a seed file is provided** — skip this step and go to Step 1.

**If no seed file is provided** — generate a seed inline before proceeding. Good ideas require a concrete persona and real pain points; a generated seed is always better than working from a vague prompt alone.

Pick a domain based on any hints the user gave (e.g., "健康系で", "副業向けで", "for freelancers"). If no hint, choose a domain that feels underserved and specific — avoid generic catch-alls like "productivity" or "health" without a narrower angle.

Write the seed in the same first-person, conversational style as a real user's notes. The seed must include:

- **First-person, conversational tone** — written like a personal memo or stream of thought ("I've been doing X for 3 years", "I find Y frustrating", "I'd pay Z/month for this").
- **Real existing tool/service names with specific complaints** — name actual products (Notion, Toggl, Goodreads, etc.) and explain what exactly falls short.
- **Usage frequency or years of experience** — quantify with numbers ("3 years", "3x a week", "5–10 books/month").
- **Price sensitivity** — a concrete monthly or annual amount ("I'd pay $5/month", "up to $50/year feels fair").
- **A target user summary line** — placed at the very end, starting with "Target user: …"

Show the generated seed to the user with a brief note like "Generated a seed. Using this persona as the basis for ideas." Then continue directly to Step 1 — do not wait for user confirmation unless they indicate they want to review or change it.

### Step 1: Read the seed file

Read the file the user specifies, or use the seed content generated in Step 0.

Extract from the seed:
- Domains of interest
- Frustrations, pain points, inefficiencies the user notices
- Complaints about existing tools or services
- The user's skills and experience
- Any hints about who they'd want to build for

### Step 2: Generate 3–5 ideas

Based on the seed, come up with 3–5 distinct ideas. Each should pass these filters:

- **Scope**: An MVP one person can ship within ~3 months
- **Differentiation**: A clear angle that isn't just "existing product + minor tweak"
- **Monetization path**: A believable route to revenue (subscription, freemium, one-time, ads)
- **Buildable**: No exotic dependencies or prohibitive upfront costs

### Step 3: Output the proposals

Write a full proposal for each idea using the template below.
If generating multiple ideas, add a ranked recommendation summary at the end.

Ask the user (or infer from context) whether to save to a file or print inline.

---

## Proposal Template

Use this exact structure for each idea:

```markdown
# [Product/Service Name] — Project Proposal

## Overview

[2–3 sentences: who it's for, what problem it solves, how it solves it differently]

**Tagline**: [One punchy sentence that sells the concept]

---

## Target Audience

| Attribute | Details |
|-----------|---------|
| Primary user | [Concrete persona] |
| Demographics | [Age, occupation, lifestyle] |
| Core pain point | [Specific frustration they feel today] |
| Current workaround | [What they use now instead] |
| Switch trigger | [What makes them try this] |

---

## Core Features

### MVP (ship this first)
- [Feature 1]
- [Feature 2]
- [Feature 3]

### Phase 2 (after gaining traction)
- [Feature 4]
- [Feature 5]

---

## Monetization Strategy

### Recommended model: [Freemium / Subscription / One-time purchase / Ad-supported]

| Plan | Price | What's included |
|------|-------|-----------------|
| Free | $0 | [Core features] |
| Pro | $[X]/month | [Premium features] |

**Rationale**: [Why this model fits this product and audience]

**Conservative revenue estimate**:
- 1,000 active users × 3% conversion = 30 paying users
- $[X]/month × 30 = $[total]/month

---

## Go-to-Market Phases

| Phase | Timeline | Milestone |
|-------|----------|-----------|
| Phase 1 | Weeks 1–4 | Core feature set + basic UX |
| Phase 2 | Weeks 5–8 | Feedback loop + iteration |
| Phase 3 | Weeks 9–12 | Beta / early access launch |
| Phase 4 | Ongoing | Public launch + monetization live |

---

## Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| [Risk 1] | [Mitigation] |
| [Risk 2] | [Mitigation] |

---

## Competitive Landscape

| Competitor | Weakness | This product's edge |
|------------|----------|---------------------|
| [Product/service] | [What it lacks] | [Your advantage] |

---

## Scorecard

| Dimension | Score (1–5) | Notes |
|-----------|------------|-------|
| Market need | ★★★★☆ | |
| Feasibility | ★★★★☆ | |
| Differentiation | ★★★☆☆ | |
| Monetization potential | ★★★★☆ | |
| Build complexity | ★★★☆☆ | |
```

---

## Output Guidelines

- Be specific — describe features in terms of what the user does and what happens, not abstract capabilities
- Keep revenue estimates conservative; don't inflate numbers to make ideas sound exciting
- When outputting multiple proposals, end with a ranked recommendation: which idea to build first and why
