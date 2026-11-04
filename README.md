# Roy Cooper's Relationship Network

Interactive map of Senator-elect Roy Cooper's 48 documented political relationships, built for CARE USA foreign aid advocacy.

**Live site:** https://aprofit-cooks.github.io/cooper-relationship-map/

## What's here

- `index.html` — Self-contained interactive 3D network visualization (Three.js + 3d-force-graph). No server needed.
- `relationships.csv` — All 48 relationships with evidence, sources, influence scores, and aid stances. Downloadable from the site's Sources tab.

## Data

- **48 edges** connecting Roy Cooper to 38 people and organizations
- **6 allies** who oppose the 2025 foreign aid cuts
- **11 persuadable bridges** — cross-party ties or members who supported cuts
- Every relationship has a dated source URL
- Data date: November 2026. Census trade data pulled 2026-10-26.

## Data sources

- NC Governor press releases (governor.nc.gov)
- Congressional roll call votes (clerk.house.gov, senate.gov)
- CGD country-level USAID cut estimates (Mar/Aug 2025, Apr 2026)
- U.S. Census Bureau International Trade API
- AP, WUNC, Reuters, and other news sources

## How to update

1. Edit `relationships.csv` (or the upstream `appendix_relationships_cooper.csv`)
2. Run: `python build_site.py <input.csv> <template.html> <output.html>`
3. Copy the new `index.html` to this repo
4. Commit and push:
   ```
   git add index.html relationships.csv
   git commit -m "Update relationship data"
   git push
   ```
   GitHub Pages will redeploy automatically within ~60 seconds.

## Influence scoring

Each relationship is scored on a 1–5 scale:

| Component | Values |
|---|---|
| tie_strength | 0.5 (group-level), 1.5 (individual interaction), 2.5 (direct collaboration) |
| aid_power | 1.0 (aid committee/party leadership), 0.5 (other sitting member), 0 (none) |
| aid_stance | 1.0 (opposes cuts), 0.5 (no record), 0.0 (supported cuts) |
| base | +0.5 |

Node score = max edge score for that person.

## License

Data compiled for academic research (Stanford IR 192, Dr. Gould, Fall 2026). Not for redistribution without permission.
