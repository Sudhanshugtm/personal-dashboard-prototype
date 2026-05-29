# Personal Dashboard — design exploration notes (T419358)

Control + a set of variations of the unified "For You" dashboard. Each is a
live, standalone, mobile-first prototype built on Wikimedia Codex tokens +
CSS-only components. Same card content throughout, so the **structure** is the
variable under test.

The core problem the variations attack: a single flat "For You" feed asks one
person to be four people at once (reader, contributor, patroller, investigator),
gives every card equal weight, and takes no stance on what matters now.

| # | Name | URL | The bet | Optimises for | Must be true | What gets worse |
|---|------|-----|---------|---------------|--------------|-----------------|
| 0 | **Baseline** | `/` | One flat feed across all intents | Simplicity, one stream | A flat mix is legible | Mode-mixing, no hierarchy |
| 1 | **Intent filter** | `/intent/` | Chips collapse the feed to one mindset | Focus on demand | User knows their intent & taps | Default still mixed; offloads triage |
| 2 | **Default to intent** | `/v2-stance/` | Lead with the user's primary intent, demote the rest | Clarity + conversion | We can infer primary intent | "Neutral, shows everything" feel |
| 3 | **One thing today** | `/v3-hero/` | One hero next-action + compact "more" | Decisiveness, low cognitive load | One action can be confidently ranked #1 | Breadth/serendipity at a glance |
| 4 | **Grouped sections** | `/v4-grouped/` | One scroll, but grouped under intent headers | Structure without hiding anything | Sections are scannable on mobile | Longer scroll; less "focus" |
| 5 | **Translator journey** | `/translate/` | A feed of only Section Translation tasks, ordered as a journey | Momentum + repeat contribution | Translation is a primary intent for this user | Single-purpose; not a whole-dashboard answer |

## Translator journey — the arc (variant 5)
A feed made entirely of Section Translation (SX) suggestions, sequenced as a journey rather than a list. Card data mirrors the real SX suggestion shape (source article, source→target language, the *missing* section, an effort cue from section size, and the reason surfaced):

1. **Land** — one easy, personalised pick ("because you edited it") to kill the cold start.
2. **Flow** — quick wins + your-topic + popular (the real `mostpopular` / by-topic ranking modes).
3. **Belong** — a collection with collective progress ("Colombian artists, 3 of 8").
4. **Impact** — reads earned on your translations (CX's real impact signal).
5. **Return** — a weekly goal / streak that pulls you back tomorrow.

Grounded in the extension: suggestions come from cxserver `/suggest/sections` + the recommendation API (`/sections`, mostpopular, by topic/country/collection) and the `cx_significant_edits` recent-edits signal; the CTA can deep-link into the `/sx` flow with `sourceLanguage/targetLanguage/pageTitle` + section.

How we'd know a direction worked: tap-through on the lead section, and the
reader → first-contribution rate, beating the flat baseline.

## Open questions for the morning
- Should the dashboard infer intent (role/history) or ask once?
- Is "Moderate" even a peer of Read/Contribute, or its own gated surface? (a
  later variant pulls it out, Reddit-style.)
- Is *intent* the right axis, or is *effort* (quick win vs deep work) better for
  newcomers and *urgency* better for patrollers?

## Build notes
- Shared baseline styles live in `/styles.css`; each variant adds a small CSS file.
- Codex via CDN (tokens + `codex.style.css`); buttons/icons are native `cdx-*`.
- Accessibility debt to clear: the filter/tab chips need a complete tab pattern
  + an `aria-live` count announcement when filtering removes cards.
