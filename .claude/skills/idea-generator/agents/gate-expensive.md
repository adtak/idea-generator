# Expensive Gate (WebSearch — money & capturability)

## Input

One idea that PASSED the cheap and saturation gates, with its money thesis.

## Purpose

Decide GO / KILL on the three things that nothing survives by accident: is real money moving here, can a solo developer capture some of it commercially, and is capturing it regulatory-safe. Budget: 2-4 WebSearch calls total for this idea. Report the count so the controller can track the 25-search ceiling. Order the checks so you stop the moment one fails — Check 3 is mostly reasoning, so apply it as soon as the licensed monopoly is identified rather than spending more searches.

## Check 1 — The idea's money thesis is real (NOT just domain money)

Do not test whether the domain has money somewhere. Test whether the **specific spend named in the idea's money thesis** is real, and whether this idea plausibly captures or diverts a slice of it. Domain-level money the idea does not touch does not count.

Search to verify the named spend: a real product / service at a real price, or a real recurring / billable cost, that this idea sits beside and shaves, replaces, or wedges against.

**KILL** if any of these hold:
- The money thesis is "none identified".
- The thesis points only to an **avoided bad outcome** — a penalty, loss, shortfall, or wasted time the user dodges — with no existing payment the app redirects. Avoided pain is not captured money.
- The named spend does not actually exist, OR money in the domain exists but flows somewhere this idea does not touch (people pay X for Y, but this idea addresses Z).

**PASS** only when there is a real, named spend AND a credible path for this idea to take a slice of it. Record the figure, source, and the slice it captures, then continue to Check 2.

## Check 2 — A solo developer can capture it (commercially)

Search for who already serves this and how. **KILL — incumbent-locked** if a funded incumbent (the very tool people already pay for, or a platform giant) already ships this core feature, or would absorb it in a sprint. Money exists but is locked inside them.

**PASS shape to look for** (these survive): the idea *sits beside* a large existing spend and shaves it (e.g. lowers a professional's fee by pre-organizing the handoff), or takes a recurring/wedge position the incumbent structurally won't (privacy stance, an audience the incumbent can't serve, a slice too small for them to bother but real for a solo).

(Whether that fee is protected by a professional licence is Check 3, not here. Never GO on Check 2 alone.)

## Check 3 — Regulatory-safe (the fee-shaving trap)

Apply this to every idea that reaches here, because the winning shape pulls straight toward it: fragmented high fees usually exist *because* the work is a licensed monopoly (税理士 for 申告, 行政書士 for 官公署提出書類, 弁護士 for legal advice, 医師, financial advice…). "A solo can shave this fee" and "this fee is regulation-protected" almost always arrive together. Check 2 confirms no *company* owns the money; Check 3 confirms no *licence* does.

Name the licensed monopoly the fee sits inside, then apply the **Yayoi/freee test**:

> Software may generate or organize an official filing **only as long as the user stays the principal — they are the filer/applicant and the app is merely a tool.** It must NOT cross into the licensed act itself: no individual professional advice, no acting as the user's agent, no per-case human review-for-fee, none of the judgement the professional is actually paid to make.

- **PASS** — the app keeps the user as principal and stays on the tool side: it organizes, drafts from the user's own inputs, guides, or checks — like 弥生/freee generating a 申告書 the user files themselves, or a pre-flight checklist for a 車検 the inspection office still judges.
- **KILL — regulated act** — capturing the fee requires the app or its operator to *perform* the licensed act: give individual advice, make the judgement the fee pays for, file/submit as the user's agent, or sell a per-case human service.
- **KILL — regulatory grey** — when the line is genuinely ambiguous (e.g. the app auto-generates the official document itself), do NOT GO on a hopeful reading. Record the grey and let a cleaner idea win. This gate errs safe by design: shipping a machine that mass-produces legally fragile apps is worse than a lower pass rate.

Expect this to lower the fee-shaving pass rate — the margin lives near the regulatory wall, so cutting near the wall cuts some winners. That is intended.

## Output

```markdown
**Expensive gate**: ✅ GO   |   KILL — [Check 1 / 2 / 3, one-line reason]
**Money evidence**: [figure + source, or "none found"]
**Capturability**: [commercial wedge (C2), or what locks it]
**Regulatory**: [licensed monopoly identified + Yayoi/freee line held (C3), or why it crosses]
**Searches used**: [N]
**Closeness**: [1-5] — [for best_so_far tracking if killed]
```

GO → loop ends, proposal-writer.md runs. KILL → back to the loop controller.
