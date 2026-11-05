# Roy Cooper: Relationship Network Map

> Interactive 3D network visualization of Senator-elect Roy Cooper's 47 documented political relationships, built for foreign-aid advocacy research.

**[→ Live site](https://cooper-relationship-map.netlify.app)**

## Overview

This project maps every documented relationship between incoming North Carolina Senator Roy Cooper and the people and organizations relevant to U.S. foreign-aid policy. Each relationship is backed by a primary source (press releases, roll-call votes, LDA filings, government records), scored on a 1–5 influence rubric, and classified as an **ally**, **cross-party contact**, or **adversarial** tie.

The visualization lets researchers and advocates quickly identify which of Cooper's contacts are most likely to influence his position on foreign aid — and what evidence supports each connection.

## Features

- **3D force-directed network** (Three.js + 3d-force-graph) with 3D/2D toggle
- **"Start here" panel** with ranked allies and cross-party contacts
- **Filters**: relationship type, minimum score, group toggles, text search
- **Click-to-inspect sidebar** with full evidence text and clickable source URLs
- **Sources tab** with sortable relationship table and CSV download
- **Mobile-responsive**: collapsible filter drawer, bottom-sheet sidebar
- **Accessibility**: keyboard navigation, Esc to close, ARIA labels, sufficient contrast
- **Self-contained**: single HTML file (~107 KB), no backend, works on `file://` or any static host

## Data

| Metric | Value |
|---|---|
| Documented relationships | 47 |
| Unique people and organizations | 38 |
| Sitting members of Congress | 13 |
| Source domains | 15 |
| Data date | November 2026 |

All data lives in [`data/relationships.csv`](data/relationships.csv) with a full [data dictionary](docs/DATA_DICTIONARY.md).

## Tech Stack

| Component | Technology |
|---|---|
| 3D rendering | [Three.js](https://threejs.org/) v0.160.0 |
| Force layout | [3d-force-graph](https://github.com/vasturiano/3d-force-graph) v1.73.3 |
| Data | CSV embedded as JSON at build time |
| Hosting | [Netlify](https://netlify.com) (also mirrored on GitHub Pages) |
| Trade analysis | Python (pandas, matplotlib), U.S. Census International Trade API |
| Network scoring | Custom influence rubric (see [methodology](docs/METHODOLOGY.md)) |

## Influence Scoring

Each relationship is scored on four components:

```
influence_score = tie_strength + aid_power + aid_stance + 0.5
```

| Component | Range | Description |
|---|---|---|
| `tie_strength` | 0.5 / 1.5 / 2.5 | Group-level → individual interaction → direct collaboration |
| `aid_power` | 0 / 0.5 / 1.0 | None → sitting member → aid committee or party leadership |
| `aid_stance` | 0 / 0.5 / 1.0 | Supported 2025 cuts → no record → opposed cuts |
| base | 0.5 | Floor |

Node score = maximum edge score for that person.

## Project Structure

```
├── index.html              # Self-contained interactive visualization
├── data/
│   └── relationships.csv   # All 47 relationships with sources and scores
├── docs/
│   ├── METHODOLOGY.md      # Scoring rubric, source verification, country groups
│   └── DATA_DICTIONARY.md  # Column definitions
└── README.md
```

## How to Update

1. Edit `data/relationships.csv`
2. Re-run the build script to regenerate `index.html`:
   ```bash
   python build_site.py data/relationships.csv index.html
   ```
3. Deploy:
   ```bash
   npx netlify-cli deploy --prod --dir .
   ```

## Research Context

This network visualization is one component of a larger research project on North Carolina's economic exposure to the 2025 U.S. foreign-aid cuts, conducted for Stanford's IR 192 (International Relations capstone). The full project includes:

- **Trade analysis**: NC exports to 31 aid-cut countries using Census International Trade API data (HS4-level, matched-month comparisons)
- **Firm-level research**: NC textile exporters to Honduras and CAFTA-DR partners
- **NC–Malawi connections**: National Guard partnership, UNC Project-Malawi, Presbyterian church ties
- **Candidate network analysis**: 47 documented Cooper relationships with influence scoring

## Author

**Alexander Profit** — Stanford University, Class of 2027
B.A. Candidate, International Relations and Computer Science
