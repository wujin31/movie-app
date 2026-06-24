# Early Digital Board

A single-page web app that finds films you can **stream, rent, or buy digitally
outside the US right now — but not inside it**. It uses live availability data
from **[JustWatch](https://www.justwatch.com/) (via TMDB)**, so it reflects what
providers actually carry today rather than guessing from patchy release dates.

Nothing is installed and nothing is sent anywhere except TMDB: your API key
stays in your browser the whole time.

## Quick start

1. Get a free TMDB API key under **Settings → API** at
   [themoviedb.org](https://www.themoviedb.org/settings/api). Either the v3 key
   (`abc123…`) or the longer v4 read-access token (`eyJ…`) works — the v4 token
   is preferred (it travels in a header, not the URL).
2. Open `index.html` in any browser.
3. Paste your key, pick a view, and hit **Scan the board**.

## How it works

Each scan queries TMDB's Discover endpoint once per foreign market (~23 are
baked in) for recent films currently available via a provider there, pools and
dedups them into one candidate set, caps it, then checks each film's live
**watch/providers** data (JustWatch via TMDB) to keep only the ones available
abroad but **not** in the US.

A title typed into **"Or search one title"** overrides the view and just
analyzes that one film.

## Views

The **View** selector picks which kind of availability counts:

| View | What it shows |
|------|---------------|
| **On streaming abroad · not in US** *(default)* | On a streaming **subscription** (flatrate) somewhere abroad, but on no US subscription. |
| **Rent/buy abroad · not in US** | Available to **rent or buy** abroad, but not in the US. |
| **Any digital abroad · not in US** | Streamable, rentable, or buyable abroad, but not available in the US. |

"Not in US" is judged for the same monetization type(s) the view is about — so
the streaming view still lists a film that's rentable in the US as long as it
isn't on a US subscription. Each view also gates on the film's own release date
(last 24–36 months) so the board stays current instead of dredging up catalog.

## Sort

- **Popularity** *(default)* — TMDB popularity score, most popular first.
- **TMDB rating** — TMDB user score (`vote_average`), highest first, with vote
  count as a tiebreak. This is TMDB's own rating, **not IMDb** — IMDb scores
  aren't available from the TMDB API.
- **Most markets** — by how many countries carry it abroad.

## Reading the board

- **Film · where to watch abroad** — title, year, TMDB ★ rating, and the top
  providers it's available on abroad (with `+N` for the rest).
- **US** — always **✗**: by definition these aren't available in the US for the
  selected view.
- **Markets** — how many non-US countries carry it.

Tap/click any row to expand the per-country provider breakdown.

## Caveats

- Availability is **JustWatch data via TMDB** and reflects current providers,
  which change often and differ by storefront. Confirm before relying on it.
- It's a snapshot of *now* — there are no "coming soon" dates in this data.
- **Availability is not legality.** Whether you may access a given title from
  your location is on you; this tool only reports where it's listed.

---

This product uses the TMDB API but is not endorsed or certified by TMDB.
Streaming availability data is provided by JustWatch.
