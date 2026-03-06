---
name: idea-generator
description: |
  Generates iOS app ideas for indie developers and outputs a structured project proposal in Markdown.
  Assumes TypeScript + Expo + AWS as the tech stack throughout.
  Reads a seed text file (interests, pain points, domain notes, etc.) and produces a proposal
  covering target audience, monetization strategy, tech architecture, core features, and dev phases.

  TRIGGER: Use this skill whenever the user wants to brainstorm iOS app ideas, generate a project
  proposal, plan an indie app, or turn a seed file into an app concept — even if they phrase it
  casually like "I want to build something" or "give me app ideas" or "help me figure out what to make."
argument-hint: "[seed-file]"
disable-model-invocation: true
allowed-tools: Read, Write
---

# iOS App Idea Generator

Generate actionable, scoped iOS app ideas from a seed text file and output a full project proposal
in Markdown. Designed for solo indie developers who will build and ship alone.

## Assumed Tech Stack

All proposals are written against this stack. Do not suggest alternatives unless the user asks.

- **Frontend**: Expo (React Native) + TypeScript
- **Backend**: AWS Lambda + API Gateway, DynamoDB, S3, Cognito
- **Auth**: AWS Cognito / Expo AuthSession
- **State**: Zustand or TanStack Query
- **Navigation**: Expo Router

Keep scope realistic for a solo developer — one person building, shipping, and maintaining.

## Process

### Step 0: Seed Generation (when no seed file is provided)

Check whether the user has provided a seed file path.

**If a seed file is provided** — skip this step and go to Step 1.

**If no seed file is provided** — generate a seed inline before proceeding. Good ideas require a concrete persona and real pain points; a generated seed is always better than working from a vague prompt alone.

Pick a domain based on any hints the user gave (e.g., "健康系で", "副業向けで"). If no hint, choose a domain that feels underserved and specific — avoid generic catch-alls like "productivity" or "health" without a narrower angle.

Write the seed in the same first-person, conversational style as a real user's notes. The seed must include:

- **一人称・口語調** — 「〜している」「〜が苦手」「〜なら払える」などの語尾。ユーザーの独り言・メモ風。
- **既存ツール名と具体的な不満** — Notion, Toggl, Apple Health など実在するアプリを挙げ、何が不満かを述べる。
- **使用頻度・経験年数** — 「3年続けている」「週3回」「月5〜10冊」など数字で具体化。
- **価格感度** — 月額または年額の金額（例: 「月500円なら払える」）。
- **想定ユーザーの一行説明** — 末尾に「想定ユーザー：〜」の形式で必ず配置。

Show the generated seed to the user with a brief note like "シードを生成しました。このペルソナをもとにアイデアを考えます。" Then continue directly to Step 1 using the generated seed content — do not wait for user confirmation unless they indicate they want to review or change it.

### Step 1: Read the seed file

Read the file the user specifies, or use the seed content generated in Step 0.

Extract from the seed:
- Domains of interest
- Frustrations, pain points, inefficiencies the user notices
- Complaints about existing tools or apps
- The user's skills and experience
- Any hints about who they'd want to build for

### Step 2: Generate 3–5 app ideas

Based on the seed, come up with 3–5 distinct ideas. Each should pass these filters:

- **Scope**: An MVP one person can ship within ~3 months
- **Differentiation**: A clear angle that isn't just "existing app + minor tweak"
- **Monetization path**: A believable route to revenue (subscription, freemium, one-time, ads)
- **Buildable**: Achievable with Expo + AWS, no exotic infrastructure required

### Step 3: Output the proposals

Write a full proposal for each idea using the template below.
If generating multiple ideas, add a ranked recommendation summary at the end.

Ask the user (or infer from context) whether to save to a file or print inline.

---

## Proposal Template

Use this exact structure for each idea:

```markdown
# [App Name] — Project Proposal

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
| Switch trigger | [What makes them download this] |

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

**Rationale**: [Why this model fits this app and audience]

**Conservative revenue estimate**:
- DAU 1,000 × 3% conversion = 30 paying users
- $[X]/month × 30 = $[total]/month

---

## Tech Architecture

### Frontend (Expo + TypeScript)
- Key Expo modules: [list]
- Notable screens: [list main views]

### Backend (AWS)

| Service | Purpose |
|---------|---------|
| Lambda + API Gateway | [API logic] |
| DynamoDB | [Data storage] |
| S3 | [File/media storage] |
| Cognito | [Auth] |
| [Other] | [Purpose] |

### Third-party integrations
- [Any external APIs or services, if needed]

### Estimated monthly AWS cost (small scale)
- AWS Free Tier covers most of it: ~$0–$10/month at launch

---

## Development Phases

| Phase | Timeline | Milestone |
|-------|----------|-----------|
| Phase 1 | Weeks 1–4 | Auth + basic CRUD + UI skeleton |
| Phase 2 | Weeks 5–8 | Core features + AWS integration |
| Phase 3 | Weeks 9–12 | TestFlight + user feedback |
| Phase 4 | Ongoing | App Store submission + monetization live |

---

## Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| [Risk 1] | [Mitigation] |
| [Risk 2] | [Mitigation] |

---

## Competitive Landscape

| Competitor | Weakness | This app's edge |
|------------|----------|-----------------|
| [App/service] | [What it lacks] | [Your advantage] |

---

## Scorecard

| Dimension | Score (1–5) | Notes |
|-----------|------------|-------|
| Market need | ★★★★☆ | |
| Technical feasibility | ★★★★☆ | |
| Differentiation | ★★★☆☆ | |
| Monetization potential | ★★★★☆ | |
| Build complexity | ★★★☆☆ | |
```

---

## Output Guidelines

- Be specific — describe features in terms of what the user taps and what happens, not abstract capabilities
- Keep revenue estimates conservative; don't inflate numbers to make ideas sound exciting
- Choose AWS services that fit solo-dev budget and ops burden (prefer DynamoDB, Lambda, S3, Cognito)
- Note any Expo managed workflow constraints if the idea requires native modules
- When outputting multiple proposals, end with a ranked recommendation: which idea to build first and why
