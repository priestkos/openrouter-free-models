# Free OpenRouter Models

A small static site that lists every **free** (zero-cost) model available on OpenRouter — the pool the
[`openrouter/free`](https://openrouter.ai/openrouter/free) router draws from, plus the router itself.

- Dark theme with red → orange accents.
- Live search, modality filters (text / vision / audio / video / router), and sorting.
- Data is regenerated straight from the [OpenRouter API](https://openrouter.ai/api/v1/models) on every deploy, and refreshed automatically once a day by GitHub Actions.

**Live:** https://priestkos.github.io/openrouter-free-models/

## How it works

| Piece | Role |
| --- | --- |
| `scripts/fetch-models.mjs` | Pulls the catalog and keeps models priced `$0 in / $0 out`. No dependencies. |
| `data/models.json` | Generated snapshot the page loads. Regenerated at build time. |
| `index.html`, `assets/` | The site (vanilla HTML/CSS/JS, no build step). |
| `.github/workflows/deploy.yml` | Builds the data, assembles `_site/`, publishes to GitHub Pages. Runs on push, daily at 06:00 UTC, and on demand. |

**Auto-updates run on GitHub Actions only** — nothing is scheduled on any local machine. The daily
`schedule:` trigger executes on GitHub's runners; trigger a manual refresh from the repo's Actions
tab (*Run workflow*) or with `gh workflow run "Deploy to GitHub Pages"`.

## Local preview

```bash
node scripts/fetch-models.mjs      # refresh data/models.json
python -m http.server 8000          # then open http://localhost:8000
```

(The page must be served over HTTP — opening `index.html` from disk blocks the JSON fetch.)
