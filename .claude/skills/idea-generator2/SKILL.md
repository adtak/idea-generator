---
name: idea-generator2
description: |
  Decides WHAT iPhone app to build by rejection sampling, generating ONLY novel ideas — ones not
  derived from complaints about existing apps. It repeatedly picks ONE domain + origination point,
  drafts ONE novel idea, and runs it through three kill-gates (a search-free reasoning gate, an
  App Store novelty-validation gate via the iTunes Search API, then a WebSearch gate for indirect
  demand and organic discoverability). It loops until an idea earns a Go or the budget is spent,
  then writes ONE full project proposal in Markdown.
  The platform is fixed: a solo-developer iPhone app (Expo / React Native, iOS only), shippable as a
  core MVP in 2-4 weeks. Ideas come from active origination points (technical enablement, play/habit,
  replacement, expression/connection, cross-domain borrowing), never from "fix what users hate about
  app X". No domain or seed file is required — the skill picks domains itself, ranging widely. An
  optional one-word nudge can mildly bias the picks but is never required.

  TRIGGER: Use when the user wants genuinely new / non-obvious iPhone app ideas, blue-sky ideation, or
  "what should I build that no one is asking for yet" — as opposed to incremental improvements on
  existing apps. For monetization-first ideas grounded in money that is already moving, use
  idea-generator instead.
argument-hint: "[optional-nudge]"
disable-model-invocation: true
allowed-tools: Read, Write, WebSearch, Bash
---

# Novel iPhone App Idea Generator (rejection-sampling loop)

This skill is a rejection-sampling loop, the same shape as `idea-generator`, but tuned for **novelty**
instead of money-that-is-already-moving. It generates ONE idea at a time and accepts the first that
clears an absolute bar. It stays deliberately thin: the whole loop lives in this file — there is no
`agents/` pipeline to follow.

## Fixed Constraints (apply at every step)

- **Platform**: iPhone app only — Expo / React Native, iOS distribution only. Not Android, not web.
- **Builder**: a single developer shipping a core MVP in 2-4 weeks.
- **iPhone-native capabilities** (Vision, HealthKit, Live Activities, Widgets, App Intents, on-device
  Core ML, etc.): use when they genuinely strengthen an idea, never forced. "iOS-only" is a focus
  decision, not a moat by itself. If the idea would be identical as a web app, do not credit the
  platform choice as defensibility.
- **Every idea must be Novel**: not derived from an existing app's complaints or a known unmet gripe.
  This skill does not do pain-driven ideation — if the best framing of an idea is "users of app X are
  frustrated by Y," it does not belong here.

## How the loop works

This skill does NOT generate a batch and rank it. It generates ONE novel idea at a time and accepts
the first that clears the bar.

**Before the loop:** read `memories/explored.md` — the cross-run memory of domains already won,
already-served (found non-novel), or explored. Use it to avoid re-mining the same ground each run.
If the file is absent, ignore it (it is local state, created at the end of the first run). The memory
format and its classification rules are defined at the end of this file.

Maintain three running values across iterations:

- `tried_domains` — domains already attempted this run (never repeat one)
- `search_count` — total WebSearch calls made this run
- `best_so_far` — the rejected idea that got closest to a Go, with its closeness note

**Stop conditions (check before each new iteration):**

- A Go was found → stop, write the proposal.
- `len(tried_domains) >= 8` → stop (domain cap).
- `search_count >= 25` → stop (search budget).

## Process — one iteration

1. **Pick a domain + origination point (search-free).** Reason only; do NOT search. Reach across
   multiple, distinct domains over the run — include at least one non-obvious context the user would
   never have proposed. A domain in `tried_domains` may not be reused. Choose the origination point
   the idea will come from (try several across the run; do not mechanically march down the list):
   - **Enablement**: a new technology or device capability makes a previously tedious/impossible
     behavior suddenly easy (on-device Vision, sensors/location, Live Activities).
   - **Play / habit**: no pain exists, but it's fun or rewarding enough to keep using.
   - **Replacement**: the user isn't suffering, but there's a clearly better way to do something they
     already do.
   - **Expression / connection**: recording, sharing, or interacting within a specific community is
     the point in itself.
   - **Cross-domain borrowing**: a mechanic from a completely different industry brought into this
     context for the first time — name the industry and the mechanic explicitly.
   Append the domain to `tried_domains`.

2. **Draft one novel idea.** Draft a single idea for that domain from the chosen origination point.
   Tag the origination point in one word. State in one line *why someone would actually start and keep
   using it* — a real trigger or moment of use, not just "it's new."

3. **Cheap gate (no search).** Reasoning only. KILL the idea if any of these fail:
   - **Buildable**: a solo dev can ship a core MVP in 2-4 weeks.
   - **Genuinely novel**: it is NOT a disguised pain-fix ("users of app X hate Y"). If its best
     framing is a complaint about an existing app, kill it.
   - **Real adoption trigger**: there is a concrete moment/reason to start and a reason to come back —
     not a "solution looking for a problem." Watch the novel-ideation traps: value only appears after
     weeks of use / a subscription forced onto a one-time life event / users learn the thing and churn
     / novelty with no repeat-use reason.
   If KILL → update `best_so_far` if this is the closest yet, print the iteration log, next iteration.
   If PASS → continue.

4. **Novelty-validation gate (iTunes Search API).** One network call to `itunes.apple.com` (Bash +
   curl), NOT a WebSearch — it does not touch `search_count` (keep to 1-2 iTunes calls per idea).
   Search the App Store for the idea's core concept. This gate validates the novelty claim — its kill
   condition is the **inverse** of `idea-generator`'s saturation gate:
   - If the App Store already has apps doing **essentially this same thing** → KILL. The premise "no
     one is doing this yet" is false; the idea is a me-too, not novel.
   - If results are empty or only tangential/adjacent → PASS (novelty is corroborated). An empty
     category is expected for a novel idea and is NOT a kill signal here; the risk of an empty
     category (no one is searching for it) is judged at the next gate, not this one.
   - If the API is unreachable → do NOT kill on that basis; pass through.
   If KILL → update `best_so_far`, log, next iteration. If PASS → continue.

5. **Expensive gate (WebSearch).** Add its searches to `search_count`. Novel ideas carry thin *direct*
   demand by design — do not kill merely for that. KILL only if:
   - **No demand of any kind**: there is neither direct demand NOR an **analogous adjacent behavior**
     that already exists (people already do this manually / in another medium). If even the analogue
     is absent, the idea is decoration → KILL.
   - **No viable discovery path**: no reason to share results, no community it spreads in, and search
     intent is thin — i.e. the only discovery path is App Store search for a category no one searches.
     Weight organic amplification more heavily than search intent; flag a search-only idea explicitly.
   - **Monetization can't work conservatively**: even at a conservative 3% conversion the money story
     is implausible, or the value can't be captured by a solo dev.
   If it clears all three → this is the winner (**GO**); stop the loop. If KILL → update `best_so_far`,
   log, next iteration.

**Iteration log** (print one line per iteration so the user sees the work):
`Domain N: [domain] ([origin]) → [idea name] → [killed @cheap | killed @novelty-validation | killed @expensive: reason | ✅ GO]`

## After the loop

- **If a Go was found:** write ONE full proposal for the Go idea, using `references/proposal-template.md`
  and the evidence gathered at the gates. Fill the template's "Central keyword & discovery path" field
  (under Go-to-Market) with the keyword/discovery note from the expensive gate. Always save the
  proposal as a Markdown file under `./idea-generator2-workspace/` (create the directory if needed —
  it is gitignored via the `/*-workspace/` pattern; name the file after the idea, e.g.
  `pocket-tide-poet-proposal.md`) and also print it to the user. Do not ask whether to save — saving
  to the workspace is the default.

- **If no Go (cap or budget hit):** Do NOT fake a winner. Output a **shortfall report**: a table of
  every attempt (domain → origin → idea → which gate killed it), then the aggregate pattern in one or
  two sentences (e.g. "5/8 died at novelty-validation — the App Store already served the concept").
  This pattern is itself a finding worth surfacing.

## Output language & constraints

- **Output language: Japanese.** Write the final deliverable — the proposal (or shortfall report) — in
  Japanese, regardless of the language of this file or the reference templates. Keep any English
  section labels from the templates, but write the content in Japanese. Internal working notes and the
  iteration log may be in any language.
- Apply `references/output-constraints.md` to the final proposal. Never inflate revenue; state
  "demand unvalidated — needs launch test" rather than inventing demand.

## Always: update the cross-run memory

Before finishing (whether a Go was found or not), append **every domain attempted this run** to
`memories/explored.md` (create the file if absent). Sort each into the right bucket by why it ended:

- **GO** → the winning idea. Add to the GO table with its origination point and adoption trigger.
- **Already-served** → killed at the novelty-validation gate because the App Store already does
  essentially this. The domain isn't necessarily dead, but this concept is taken; record the concept.
- **Explored, open** → killed for an idea-specific reason (weak adoption trigger, no analogous demand,
  monetization implausible). Record the dead idea and reason.

Classification rule when in doubt: ask "would a *different* novel idea in this domain plausibly clear
the bar?" Yes → Explored-open; No → the domain is exhausted for novelty, note it as such.

Also keep a short **Lessons** section in the same file: one line per recurring lesson (an origination
point that keeps yielding unadoptable ideas, a novelty pattern with no repeat-use reason, a discovery
path that only works with a community that doesn't exist). Don't duplicate what the repo or chat
already captures; update an existing lesson rather than adding a near-duplicate; delete lessons later
found wrong.
