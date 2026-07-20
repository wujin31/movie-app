# Purchase-Only Radar

A single-page web app that catalogs **popular, well-rated films that are not on
any major US streaming subscription — only available to rent or buy digitally**.
The Oppenheimer problem: it's in every digital store, but on none of your
services.

Availability comes live from **[JustWatch](https://www.justwatch.com/) (via
TMDB)**, so the board reflects what providers actually carry today. Nothing is
installed and nothing is sent anywhere except TMDB: your API key stays in your
browser the whole time.

## Quick start

1. Get a free TMDB API key under **Settings → API** at
   [themoviedb.org](https://www.themoviedb.org/settings/api). Either the v3 key
   (`abc123…`) or the longer v4 read-access token (`eyJ…`) works — the v4 token
   is preferred (it travels in a header, not the URL).
2. Open `index.html` in any browser.
3. Paste your key, pick a view, and hit **Scan the board**.

## How it works

Each scan pulls the US digital catalog from TMDB's Discover endpoint (films
currently rentable or buyable in the US, with quality gates on rating and vote
count), dedups and caps the pool, then checks each film's live
**watch/providers** data. A film makes the board when it can be rented or
bought digitally in the US **and** no major subscription service carries it.

**The majors:** Netflix, Amazon Prime Video, Disney+, Hulu, HBO Max, Paramount+,
Peacock, and Apple TV+ — including their channel variants ("Paramount+ Amazon
Channel") **and their ad-supported tiers**, which TMDB files under a separate
`ads` bucket (Peacock's ad tier, Netflix with Ads, Paramount+ Essential…). A
film carried any of those ways is treated as streaming and excluded. A film
that's only on a niche subscription — Starz, Criterion Channel, Kanopy, MGM+ —
still counts as fallen-off, and the row tells you so ("Starz only").

Every row's expanded detail has a **Verify on JustWatch ↗** link that opens the
film on justwatch.com for a live second opinion.

A title typed into **"Or check one title"** overrides the view and just checks
that one film — handy for confirming a specific case like Oppenheimer.

## Views

| View | What it shows |
|------|---------------|
| **Fallen off the majors · catalog** *(default)* | Films older than ~18 months (past the usual theatrical→streaming window), rated 6.5+ with 500+ votes, that you can only rent or buy. |
| **Never landed · recent releases** | Films from the last ~18 months already on US digital storefronts but still not on any major streamer. Lower vote floor (200) since recent films accumulate votes slowly. |

## Sort

- **Popularity** *(default)* — TMDB popularity score, most popular first.
- **TMDB rating** — TMDB user score (`vote_average`), highest first, with vote
  count as a tiebreak. This is TMDB's own rating, **not IMDb** — IMDb scores
  aren't available from the TMDB API.
- **Year** — newest first.

## Reading the board

- **Film · where to rent or buy** — title, year, and the top storefronts
  carrying it (with `+N` for the rest).
- **Streaming** — **✗ none** (amber) when no US subscription has it, or the
  niche service that does (e.g. "Starz only").
- **★ TMDB** — the film's TMDB rating.

Tap/click any row to expand the full US breakdown: rent, buy, niche
subscription, and free-with-ads availability.

## Caveats

- Availability is **JustWatch data via TMDB** and reflects current providers.
  Titles rotate on and off services constantly — confirm on the storefront
  before buying.
- It's a snapshot of *now* — the data carries no "coming to Netflix on X" dates.
- The quality gates (rating/vote floors) are intentional: the board is meant to
  surface notable films, not every purchase-only title in existence.

---

This product uses the TMDB API but is not endorsed or certified by TMDB.
Streaming availability data is provided by JustWatch.
