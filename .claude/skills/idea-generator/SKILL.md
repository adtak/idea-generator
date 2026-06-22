---
name: idea-generator
description: |
  Decides WHAT iPhone app to build by rejection sampling: it repeatedly picks ONE random domain, drafts ONE idea, and runs it through two kill-gates (a search-free reasoning gate, then a WebSearch gate for money-realness and solo-capturability). It loops until an idea earns a Go or the budget is spent, then writes a full project proposal in Markdown.
  The platform is fixed: a solo-developer iPhone app (Expo / React Native, iOS only), shippable as a core MVP in 2-4 weeks.
  No domain or seed file is required — the skill picks domains itself, ranging widely so it surfaces ideas the user would never have asked for. An optional one-word hint can mildly bias the picks but is never required.
  The bar is monetization-first: an idea only passes if real money is already moving in its space AND a solo developer can plausibly capture some of it (not locked inside a funded incumbent or behind a professional license).
  Produces a proposal covering target audience, core features, monetization, go-to-market, competitive landscape, and market validation.

  TRIGGER: Use this skill whenever the user wants to figure out what iPhone app to build, brainstorm a
  monetizable app idea, or generate a project proposal — even phrased casually like "what should I build"
  or "give me an app idea that could actually make money."
disable-model-invocation: true
allowed-tools: Read, Write, WebSearch, Bash
---

# iPhone App Idea Generator (rejection-sampling loop)

## Fixed Constraints (apply at every step)

- **Platform**: iPhone app only — Expo / React Native, iOS distribution only. Not Android, not web.
- **Builder**: a single developer shipping a core MVP in 2-4 weeks.
- **iPhone-native capabilities** (Vision, HealthKit, Live Activities, Widgets, App Intents, on-device Core ML, etc.): use when they genuinely strengthen an idea, never forced. "iOS-only" is a focus decision, not a moat by itself.

## How the loop works

This skill does NOT generate a batch and rank it. It generates ONE idea at a time and accepts the first that clears an absolute bar.

**Before the loop:** read `memories/explored.md` — the cross-run memory of domains already won, structurally closed, or explored. The domain-picker uses it to avoid re-mining the same ground each run.

Maintain three running values across iterations:

- `tried_domains` — domains already attempted this run (never repeat one)
- `search_count` — total WebSearch calls made this run
- `best_so_far` — the rejected idea that got closest to a Go, with its closeness note

**Stop conditions (check before each new iteration):**

- A Go was found → stop, write the proposal.
- `len(tried_domains) >= 8` → stop (domain cap).
- `search_count >= 25` → stop (search budget).

## Process — one iteration

1. **Pick a domain.** Read `agents/domain-picker.md` and follow it, passing `tried_domains` and the optional hint. It returns ONE fresh domain (search-free). Append it to `tried_domains`.

2. **Draft one idea.** Read `agents/idea-drafter.md` and follow it to draft a single idea for that domain.

3. **Cheap gate (no search).** Read `agents/gate-cheap.md` and follow it. If KILL → record the idea's closeness note into `best_so_far` if it's the closest yet, print a one-line iteration log, and start the next iteration. If PASS → continue.

4. **Saturation gate (iTunes Search API).** Read `agents/gate-saturation.md` and follow it — one network call to `itunes.apple.com`, not a WebSearch (does not touch `search_count`; keep to 1-2 iTunes calls per idea). If KILL (red ocean) → update `best_so_far`, log, next iteration. If PASS / incumbent-flagged / unchecked → continue. If the API is unreachable, do NOT kill on that basis — pass through.

5. **Expensive gate (WebSearch).** Read `agents/gate-expensive.md` and follow it; add its searches to `search_count`. If KILL → update `best_so_far`, log, next iteration. If GO → this is the winner; stop the loop.

**Iteration log** (print one line per iteration so the user sees the work):
`Domain N: [domain] → [idea name] → [killed @cheap | killed @saturation | killed @expensive: reason | ✅ GO]`

## After the loop

- **If a Go was found:** Read `agents/proposal-writer.md` and follow it to write a full proposal for the Go idea, using `references/proposal-template.md` and the evidence gathered at the gates. Always save the proposal as a Markdown file under `./idea-generator-workspace/` (create the directory if needed — it is gitignored via the `/*-workspace/` pattern; name the file after the idea, e.g. `kobutsu-shinsei-navi-proposal.md`) and also print it to the user. Do not ask whether to save — saving to the workspace is the default.

- **If no Go (cap or budget hit):** Do NOT fake a winner. Output:
  1. A **shortfall report**: a table of every attempt (domain → idea → which gate killed it), then the aggregate pattern in one or two sentences (e.g. "6/8 died at the capturability gate — the money was locked inside an incumbent the user already pays"). This pattern is itself a finding worth surfacing.

## Always: update the cross-run memory

Before finishing (whether a Go was found or not), append **every domain attempted this run** to `memories/explored.md`, sorting each into the right bucket by why it ended. Use the classification rule already written at the top of `memories/explored.md`:

- **GO** → the winning idea. Add to the GO table with the captured money.
- **Dead domain** → killed for a domain-structural reason (no real money in the domain, a funded incumbent owns the core, a license/liability gates the space, or the niche is an **oversupplied red ocean** per the saturation gate). Add to Dead domains.
- **Explored, open** → killed for an idea-specific reason (me-too, this idea needed maintained data, this idea's money thesis was weak). Add to Explored-open with the dead idea and reason.

When in doubt between Dead and Explored-open, ask: "would a _different_ idea in this domain plausibly clear the bar?" Yes → Explored-open; No → Dead. This is what keeps future runs from both re-mining won ground and prematurely burning domains that still have an unexplored angle.

## Constraints

Apply `references/output-constraints.md` to the final proposal. Never inflate revenue; state "No evidence found" rather than inventing demand.
