# Early Digital Board

A single-page web app that scans [TMDB](https://www.themoviedb.org/) for films
that get a **digital release (stream / VOD) in a non-US market before the US** —
sorted as a departures board by the soonest foreign release.

It's a release-date radar built entirely on TMDB's public, community-sourced
data. Nothing is installed and nothing is sent anywhere except TMDB: your API
key stays in your browser the whole time.

## Quick start

1. Get a free TMDB API key under **Settings → API** at
   [themoviedb.org](https://www.themoviedb.org/settings/api). Either the v3 key
   (`abc123…`) or the longer v4 read-access token (`eyJ…`) works.
2. Open `index.html` in any browser.
3. Paste your key, pick a mode, and hit **Scan the board**.

## Sources

The **Source** selector chooses how candidate films are gathered:

- **🌍 Wide scan — recent foreign digital** *(default)* — queries TMDB's
  Discover endpoint once per foreign market for films with a digital release in
  a date window, pools the results, dedups them, and caps the pool before
  analysis. This casts a much wider net than the curated lists.
- **List · …** (In theaters now / Upcoming / Popular / Top rated) — scans one of
  TMDB's curated lists, a few pages deep. Faster, but limited to ~100 titles and
  sparse on digital dates.

A single title typed into **"Or search one title"** overrides everything and
just analyzes that one film.

### Wide-scan controls

- **Look back over** — how far back to pull digital releases (3 / 6 / 12 / 24
  months). A larger window finds more, but for the "available now" view a very
  long window mostly pulls in old titles that have since reached the US.
- **Max films to check** — a hard cap on the per-film detail pass so the scan
  stays fast and API-polite. The status line warns when you hit it.
- **Foreign markets** — comma-separated ISO 3166-1 country codes to scan
  (prefilled with ~23 common early-digital markets). Add or remove freely.
- **Pages per market** — Discover pages to pull per market (~20 candidates each).

## Show — the three views

The **Show** selector decides which hits make the board:

| View | What it shows |
|------|---------------|
| **Streaming abroad now · not yet in US** *(default)* | Earliest foreign digital date is already in the **past** (available somewhere abroad now) **and** the US has no past digital date (TBD or still ahead). Sorted newest-first. |
| **Not yet on US digital** | Anything the US hasn't released digitally yet, including foreign releases that are still upcoming. Sorted soonest-first. |
| **All foreign-before-US** | Every hit where a foreign digital date beats the US, no date filter. |

## Reading the board

- **Film · earliest foreign digital** — the title, plus the earliest foreign
  market and date. A green **"out now"** tag means that date has already passed.
- **US digital** — the US digital date, or **—** if TMDB has none yet.
- **Lead** — how many days the US is trailing the earliest foreign release, or
  **US TBD** when there's no US date.

Tap/click any row to expand every foreign digital date on file for that film.

## Caveats

- Release dates are **community-sourced** and can be incomplete, wrong, or shift.
  Confirm on an actual storefront before relying on a date.
- "Digital" means TMDB **release type 4** (streaming / VOD rent or buy).
- The board only reflects what TMDB has entered — a sparse result is often
  missing data, not a bug.

---

This product uses the TMDB API but is not endorsed or certified by TMDB.
