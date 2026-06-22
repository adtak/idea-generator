# Saturation Gate (iTunes Search API — App Store red-ocean check)

## Input

One idea that PASSED the cheap gate, with its domain/niche and a few keywords.

## Purpose

Catch niches that are **flooded with near-duplicate apps that users did not bite on** — the vibe-coded gold-rush failure mode the reasoning-only cheap gate misses (it only knows incumbents by memory). This gate looks at the actual App Store via the iTunes Search API.

This sits between the cheap gate (reasoning, free) and the expensive gate (WebSearch). It costs one network call, not WebSearch budget — so it kills red oceans *before* any search is spent.

> Requires network access to `itunes.apple.com`. If the call fails (host blocked / no network), do NOT kill on that basis — record "saturation: unchecked (no API access)" and pass through to the expensive gate.

## How to query

Use Bash + curl. 1-2 queries max. Pick the niche's most natural search term (Japanese for a JP-targeted idea; add an English term if it targets the US). URL-encode the term.

```bash
curl -s "https://itunes.apple.com/search?term=<URL-encoded term>&country=jp&entity=software&limit=50"
```

Parse `results[]`. For each app extract: `trackName`, `sellerName`, `userRatingCount`, `averageUserRating`, `currentVersionReleaseDate`, `formattedPrice`. (`jq` or a short `python3` snippet is fine.)

## Read the field

1. **Filter to genuinely same-niche apps** — the API matches loosely; use judgment to drop unrelated results. Call the filtered set R.
2. Profile R:
   - `|R|` — how many real near-duplicates.
   - **ratings distribution** — how many in R have meaningful traction (`userRatingCount` ≥ ~200) vs near-zero (`< ~50`).
   - **recency** — how many have `currentVersionReleaseDate` within the last ~12 months.

## Decision (NEVER kill on existence alone)

The kill condition is the **combination** "many duplicates × ratings not accumulating", not mere presence of competitors. A handful of similar apps, or a field with real demand, passes — a quality / interaction wedge can still win there.

- **PASS** — `|R| ≤ ~2` (whitespace; demand is the expensive gate's job, not this gate's), OR a competitive-but-healthy field where several apps have real traction (multiple with ≥ ~200 ratings). Real market with winners ≠ red ocean.
- **PASS (incumbent flagged)** — one or two apps dominate with large `userRatingCount` (≥ ~1,000) and the rest trail. Not junk-saturated; it's an incumbent. Pass through but note it so the expensive gate's C2 can judge capturability.
- **KILL — red ocean** — `|R|` is high (≥ ~8 genuine near-duplicates) AND the large majority sit under ~50 ratings, especially if many were released/updated within ~12 months. Many builders chased it; users didn't bite. Supply >> demand.

Thresholds are heuristic — adapt to the category and state the actual numbers you saw. When the field is ambiguous, pass through to the expensive gate rather than killing.

## Output

```markdown
**Saturation gate**: PASS → expensive gate | PASS (incumbent flagged) → expensive gate | KILL — red ocean | unchecked (no API access) → expensive gate
**Field**: [N relevant apps; ratings profile e.g. "9 apps, 7 under 50 ratings, 5 updated <12mo"; top app [name] (X ratings, formattedPrice)]
**Read**: [one line]
**Closeness**: [1-5] — [for best_so_far tracking if killed]
```

A red-ocean KILL is **domain-level** — record it as a Dead domain (the niche is oversupplied; a different idea won't fix it). PASS / flagged → hand off to gate-expensive.md.
