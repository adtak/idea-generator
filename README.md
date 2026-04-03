# idea-generator

A Claude Code skill that turns zero input into three scored product proposals — no seed file, no domain expertise required.

## What it does

Give it a one-word domain hint (or nothing at all), and it generates a seed, extracts signals, produces 8-10 candidate ideas, scores them, and writes full proposals for the top 3.

This is a [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) — invoke it with `/idea-generator` inside Claude Code.

## Installation

```bash
git clone https://github.com/adtak/idea-generator.git
cd idea-generator
claude
```

Then run `/idea-generator` in the Claude Code prompt.

## What makes it different

- **Start from zero** — No seed file needed. A single hint like "fitness" auto-generates 3 realistic personas with real tool names, price sensitivity, and pain points. Provide a seed file and it skips straight to ideation.
- **Cross-domain borrowing** — Every candidate must name a mechanic borrowed from another industry (e.g., Duolingo's streak applied to meal planning). Forces novel combinations instead of me-too ideas.
- **Deliberate omission** — Every candidate must declare one standard feature it intentionally leaves out (e.g., no social feed, no free tier). Prevents feature bloat from the start.
- **Competitor overlap check** — After generating candidates, each idea is searched against existing products via WebSearch. Overlap level (High / Medium / Low / None) is annotated and fed into scoring. High-overlap clones get their Diff score capped automatically.
- **Market demand validation** — After selecting top 3, each idea is validated via WebSearch across 4 dimensions: pain point signals (forum/SNS posts), existing solution traction (user counts, revenue), market size, and failure warnings (similar products that shut down). Ideas with weak demand can be flagged for replacement.
- **Trap detection** — The scoring step auto-detects four common traps: *Clone trap* (existing product already does the same thing), *Time-to-value trap* (value requires weeks of logging), *One-shot trap* (infrequent life events forced into subscriptions), and *Graduation trap* (users internalize the lesson and cancel). Affected scores are capped automatically.
- **Solo-dev MVP scope** — All 6 scoring axes assume a single developer shipping in 2-4 weeks. Ideas that need months, heavy backends, or complex ML pipelines score low.
- **Tech stack agnostic** — Proposals cover audience, features, monetization, go-to-market, and competitive landscape. No architecture or tech stack section — that's a separate decision.

## Pipeline

```
Seed  -->  Candidates  -->  Competitor Check  -->  Scoring  -->  Demand Research  -->  Proposals
```

1. **Seed** — Auto-generate 3 personas from a hint, or read a provided seed file
2. **Candidates** — Extract signals and generate 8-10 ideas (Name / Pitch / Cross-domain Borrowing / Deliberate Omission)
3. **Competitor Check** — Search for existing products via WebSearch and annotate each candidate with overlap level
4. **Scoring** — Rate each on 6 axes (Speed / Diff / Moat / Mono / Build / Risk, each 1-3), apply trap detection (including Clone trap), select top 3
5. **Demand Research** — Validate real-world demand for the 3 selected ideas via WebSearch (pain points, traction, market size, failure signals)
6. **Proposals** — Write full proposals for the 3 selected ideas, incorporating market validation findings

## Usage

```
/idea-generator
/idea-generator fitness
/idea-generator seeds/my-domain.txt
```

## Output

Each proposal includes:

- Market Validation (evidence-based demand findings)
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
.claude/
├── CLAUDE.md                       # Project instructions for Claude Code
└── skills/
    └── idea-generator/
        ├── SKILL.md                        # Orchestrator — flow control only
        ├── agents/
        │   ├── seed-generator.md           # Seed auto-generation logic
        │   ├── candidate-generator.md      # Extracts signals and generates 8-10 candidate ideas
        │   ├── competitor-checker.md       # Searches for existing competitors and annotates overlap
        │   ├── idea-selector.md            # Scores candidates and selects exactly 3
        │   ├── market-researcher.md       # Validates demand via WebSearch (pain points, traction, market size, failures)
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
