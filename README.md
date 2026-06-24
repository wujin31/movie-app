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

## How it works

Each scan queries TMDB's Discover endpoint once per foreign market (~23 common
early-digital markets are baked in) for films with a digital release in a date
window, pools and dedups the results into one candidate set, caps it, then pulls
each film's full release-date breakdown to find the ones where a foreign digital
date beats the US. No knobs to tune — the **View** picks the window and filter
for you.

A title typed into **"Or search one title"** overrides the view and just
analyzes that one film.

## Views

The **View** selector is the main control — each is a self-contained preset:

| View | What it shows |
|------|---------------|
| **Streaming abroad now · not yet in US** *(default)* | Earliest foreign digital date is already in the **past** (available somewhere abroad now) **and** the US has no past digital date (TBD or still ahead). |
| **Dropping soon abroad · before the US** | Foreign digital release still **ahead**, landing before the US (or with no US date yet). |
| **All · foreign digital beats the US** | Every hit where a foreign digital date beats the US, past or future. |

## Sort

The **Sort by** selector orders the board:

- **Popularity** *(default)* — TMDB popularity score, most popular first.
- **TMDB rating** — TMDB user score (`vote_average`), highest first, with vote
  count as a tiebreak. Note this is TMDB's own rating, **not IMDb** — IMDb scores
  aren't available from the TMDB API.
- **Release date** — by earliest foreign digital date (newest first for the
  "now" view, soonest first for the forward-looking views).

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
