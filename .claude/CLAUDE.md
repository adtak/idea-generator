# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

This is a **Claude Code skill** repository. It defines two sibling skills that both decide WHAT iPhone app to build via a rejection-sampling loop, differing only in the bar an idea must clear:

- `idea-generator` — **monetization-first**: accepts an idea only if real money is already moving AND a solo dev can plausibly capture some. Split into an `agents/` pipeline.
- `idea-generator2` — **novelty-first**: accepts only genuinely novel ideas (never derived from complaints about an existing app). Deliberately thin — the whole loop lives in one `SKILL.md`, no `agents/` pipeline.

There is no build system, runtime, or test runner. The primary artifacts are:

- `.claude/skills/idea-generator/SKILL.md` — loop orchestrator (flow control only)
- `.claude/skills/idea-generator/agents/domain-picker.md` — picks ONE fresh domain per iteration (search-free)
- `.claude/skills/idea-generator/agents/idea-drafter.md` — drafts ONE idea for that domain
- `.claude/skills/idea-generator/agents/gate-cheap.md` — reasoning-only kill gate (buildable solo? differentiated?)
- `.claude/skills/idea-generator/agents/gate-saturation.md` — App Store red-ocean check via iTunes Search API
- `.claude/skills/idea-generator/agents/gate-expensive.md` — WebSearch gate (money thesis real? solo-capturable? regulatory-safe?)
- `.claude/skills/idea-generator/agents/proposal-writer.md` — writes ONE full proposal for the Go idea
- `.claude/skills/idea-generator/agents/seed-generator.md` — LEGACY, no longer referenced by SKILL.md
- `.claude/skills/idea-generator/memories/explored.md` — cross-run memory (GO / Dead domains / Explored-open)
- `.claude/skills/idea-generator/references/proposal-template.md` — Markdown template for the proposal
- `.claude/skills/idea-generator/references/output-constraints.md` — non-negotiable output rules
- `.claude/skills/idea-generator2/SKILL.md` — self-contained novelty loop (loop + 3 gates + memory rules all inline; no `agents/`)
- `.claude/skills/idea-generator2/references/proposal-template.md` — Markdown template (includes a "Central keyword & discovery path" field)
- `.claude/skills/idea-generator2/references/output-constraints.md` — output rules (novelty-flavored; single winning proposal, Japanese output)

## Skill Behavior

The `idea-generator` skill runs a rejection-sampling loop:

1. Reads `memories/explored.md` to know which domains are already won, structurally closed, or explored
2. Picks ONE domain (`agents/domain-picker.md`) — search-free, avoids explored domains
3. Drafts ONE idea (`agents/idea-drafter.md`) — cross-domain borrowing + deliberate omission + money thesis
4. Cheap gate (`agents/gate-cheap.md`) — kills obviously-doomed ideas with reasoning only, no WebSearch
5. Saturation gate (`agents/gate-saturation.md`) — one iTunes Search API call; kills red-ocean niches
6. Expensive gate (`agents/gate-expensive.md`) — WebSearch; kills on money thesis, capturability, or regulatory grounds
7. First idea that passes all three gates is the winner → writes a full proposal (`agents/proposal-writer.md`) using `references/proposal-template.md`
8. Updates `memories/explored.md` with every domain attempted this run

Platform is fixed: solo-developer iPhone app (Expo / React Native, iOS only), MVP in 2-4 weeks. Bar is monetization-first.

The `idea-generator2` skill runs the same loop shape, tuned for **novelty** and kept thin (everything in one `SKILL.md`):

1. Reads `memories/explored.md` (cross-run, local/gitignored) to avoid re-mining
2. Picks ONE domain + origination point (Enablement / Play / Replacement / Expression / Cross-domain) — search-free
3. Drafts ONE novel idea (never a disguised pain-fix; must state a real adoption trigger)
4. Cheap gate — reasoning only: buildable solo? genuinely novel (not a pain-fix)? real adoption trigger?
5. Novelty-validation gate (iTunes Search API) — the **inverse** of idea-generator's saturation gate: kills if the App Store already does essentially this (me-too); an empty category PASSES
6. Expensive gate (WebSearch) — kills only on no demand-of-any-kind (not even an analogous behavior), no viable discovery path, or implausible conservative monetization
7. First idea that earns a Go wins → writes ONE full proposal, saved to `./idea-generator2-workspace/` and printed; output in Japanese
8. Updates `memories/explored.md` (buckets: GO / Already-served / Explored-open, plus a Lessons section)

If no Go, both skills emit a shortfall report and never fake a winner.

## Modifying the Skill

After any change to skill files, check whether `CLAUDE.md` needs to be updated.

When editing files, preserve:
- The proposal template structure in `references/proposal-template.md` exactly — sections include Target Audience table, Monetization table, Go-to-Market Phases table, Scorecard with star ratings, and Market Validation
- The constraint in `references/output-constraints.md` that prohibits tech stack / architecture sections
- The `agents/` files are plain Markdown read by SKILL.md via the Read tool — they are not registered Claude Code sub-agents and do not need YAML frontmatter
- `memories/explored.md` is the cross-run state file — edits affect all future runs. Both skills' `memories/` dirs are gitignored (local state); the classification rules live in the skill files, not in a tracked seed
- `idea-generator2` is intentionally thin: its whole loop (loop + 3 gates + memory rules) lives in one `SKILL.md` with NO `agents/` pipeline. Keep it that way — do not split it into agent files. Its novelty-validation gate is deliberately the inverse of idea-generator's saturation gate
