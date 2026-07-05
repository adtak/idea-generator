---
name: novel-explorer
description: |
  Explores across domains to decide WHAT iPhone app to build, generating ONLY novel ideas — ones
  not derived from complaints about existing apps. Produces 3 scored project proposals in Markdown.
  Ideas come from active origination points (technical enablement, play/habit, replacement,
  expression/connection, cross-domain borrowing), never from "fix what users hate about app X".
  The platform is fixed: a solo-developer iPhone app (Expo / React Native, iOS only), shippable as a
  core MVP in 2-4 weeks. Covers target audience, core features, monetization, go-to-market,
  discoverability, and demand signals via WebSearch. Architecture and tech-stack detail are out of scope.

  TRIGGER: Use when the user wants genuinely new / non-obvious iPhone app ideas, blue-sky ideation,
  or "what should I build that no one is asking for yet" — as opposed to incremental improvements on
  existing apps.
argument-hint: "[optional-nudge]"
disable-model-invocation: true
allowed-tools: Read, Write, WebSearch
---

# Novel iPhone App Explorer

This skill is deliberately thin. It gives you a goal, fixed constraints, and a quality bar — not a
procedure. How you explore, ideate, and verify is yours to decide.

## Goal

Explore domains yourself and decide what iPhone app to build, then output 3 scored proposals.
Every idea must be **Novel**: not derived from an existing app's complaints or a known unmet
gripe. This skill does not do pain-driven ideation — if the best framing of an idea is "users of
app X are frustrated by Y," it does not belong here.

## At the start

- If `lessons/explore-lessons.md` exists, read it first. Apply past lessons (origins that kept
  producing weak ideas, "clever but unadoptable" patterns, discovery paths that never worked). If
  absent, ignore.

## Fixed constraints

- iPhone app only — Expo / React Native, iOS distribution only. Not Android, not web.
- Solo developer. Core MVP must be shippable in 2-4 weeks.
- iPhone-native capabilities (Vision, HealthKit, Live Activities, Widgets, App Intents, on-device
  Core ML, etc.): use them only when they strengthen an idea. Never forced.
- iOS-only is not a moat by itself. If the idea would be identical as a web app, do not credit the
  platform choice as defensibility.

## Quality bar (do not drop these)

- **Explore widely.** Do not ask me for a domain. Reach across multiple, distinct domains yourself.
  Include at least one non-obvious context I would not have proposed.

- **Generate from active origination points, not from pain.** Drive ideation from these starting
  points (try several; do not just work down the list mechanically):
  - **Enablement**: a new technology or device capability makes a previously tedious/impossible
    behavior suddenly easy (e.g. on-device Vision, sensors/location, Live Activities).
  - **Play / habit**: no pain exists, but it's fun or rewarding enough to keep using.
  - **Replacement**: the user isn't suffering, but there's a clearly better way to do something
    they already do.
  - **Expression / connection**: recording, sharing, or interacting within a specific community is
    the point in itself.
  - **Cross-domain borrowing**: a mechanic from a completely different industry brought into this
    context for the first time — name the industry and the mechanic explicitly.
  Tag each idea with which origination point it came from (one word).

- **Origin diversity (replaces lane-mixing).** The 3 selected ideas must come from at least 2
  distinct origination points — never all from the same origin (e.g. not three "enablement" apps).
  This keeps the set from collapsing into one flavor of novelty.

- **Guard against "solution looking for a problem."** The central failure mode of pure-novel
  ideation is cleverness with no adoption path. For each idea, state in one line *why someone would
  actually start and keep using it* — a real trigger or moment of use, not just "it's new." If you
  can't, the idea is decoration; cut it.

- **Be skeptical about solo-dev reality, defensibility, and monetization.** Watch for traps:
  value only appears after weeks of use / forcing a subscription onto a one-time life event /
  users learn the thing and churn / novelty with no repeat-use reason.

- **Discoverability (App Store), as an independent axis.** Novel ideas carry a built-in handicap:
  no one is searching for a category that doesn't exist yet. So:
  - Search intent will usually be weak for novel ideas — do not over-penalize that. Note the
    likely central keyword honestly even if it's thin.
  - Weight **organic amplification** more heavily instead: is there a reason to share results,
    recommend it, or a specific community where it spreads? A novel idea whose only discovery path
    is App Store search is the most dangerous case — flag it explicitly.
  - In each proposal, state the assumed central keyword and primary discovery path, and name its
    weakness in 1-2 sentences.

- **Validate demand via WebSearch, honestly.** Don't fabricate. For novel ideas, direct demand
  evidence is thin by definition — do not discard an idea for lack of it. Instead look for an
  **analogous adjacent behavior** that already exists (people already do X manually / in another
  medium) as indirect evidence. If even that is absent, write "demand unvalidated — needs launch
  test" plainly. Keep revenue estimates conservative.

- **Format and hard rules from existing assets.** Read and apply `references/proposal-template.md`
  and `references/output-constraints.md`. Fill the template's "Central keyword & discovery path"
  field (under Go-to-Market) with the keyword/discovery note.

- **Output language: Japanese.** Write the final deliverable — the 3 proposals and the ranking — in
  Japanese, regardless of the language of this skill file or the reference templates. If a reference
  template has English section labels, keep the structure but write the content in Japanese. Your
  internal working notes and verifier exchanges can be in any language; everything I read at the end
  must be Japanese.

- End with a ranking: which to build first, and why.

## How to proceed

- This is an autonomous task. I do not specify the procedure — you decide how to explore, whether
  to use subagents, and how to verify. Do not follow any older agents/ pipeline.
- When you have enough to act, act. Only pause for me when the work genuinely requires it
  (irreversible action, real scope change, input only I can give).
- After one exploration pass, briefly surface the result (domains hit, candidate directions) before
  continuing. Assume I am not watching in real time; state each phase's conclusion concisely.
- Before finalizing the 3, spin up a separate fresh-context verifier subagent (not self-critique).
  Have it check this skill's constraints and quality bar: origins span >=2 points / no idea is a
  disguised pain-fix / each idea has a stated real adoption trigger / discoverability weakness is
  named / revenue is conservative / each demand claim is either evidenced or flagged unvalidated.
  Fix what it flags before output.
- Before reporting progress, audit each claim against an actual WebSearch result. Mark anything
  unverified as such.
- You don't need to reproduce your reasoning in the response body. Stating decision bases as
  deliverables (why an idea scored as it did) is fine; narrating your thinking is not.
- Lead with the outcome. Give a recommendation, not an exhaustive survey of options you won't take.

## At the end

- Append this run's lessons to `lessons/explore-lessons.md` (create if absent). One entry per lesson,
  one-line summary on top. E.g. "origination point that kept yielding unadoptable ideas",
  "novelty pattern with no repeat-use reason", "discovery path that only works with a community
  that doesn't exist". Don't record what the repo or chat already captures; prefer updating an
  existing entry over duplicating; delete lessons later found wrong.

Deliverable: 3 proposals + a ranking, written in Japanese. Ask whether to save to a file or print
inline at the end.
