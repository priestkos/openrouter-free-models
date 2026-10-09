# Free OpenRouter Models

A small static site that lists every **free** (zero-cost) model available on OpenRouter — the pool the
[`openrouter/free`](https://openrouter.ai/openrouter/free) router draws from, plus the router itself.

- Dark theme with red → orange accents.
- Live search, modality filters (text / vision / audio / video / router), and sorting.
- Data is regenerated on every deploy straight from the [OpenRouter API](https://openrouter.ai/api/v1/models).

**Live:** https://priestkos.github.io/openrouter-free-models/

## How it works

| Piece | Role |
| --- | --- |
| `scripts/fetch-models.mjs` | Pulls the catalog and keeps models priced `$0 in / $0 out`. No dependencies. |
| `data/models.json` | Generated snapshot the page loads. Regenerated at build time. |
| `index.html`, `assets/` | The site (vanilla HTML/CSS/JS, no build step). |
| `.github/workflows/deploy.yml` | Builds the data, assembles `_site/`, publishes to GitHub Pages. Runs on push and on demand (no schedule). |

## Local preview

```bash
node scripts/fetch-models.mjs      # refresh data/models.json
python -m http.server 8000          # then open http://localhost:8000
```

(The page must be served over HTTP — opening `index.html` from disk blocks the JSON fetch.)
