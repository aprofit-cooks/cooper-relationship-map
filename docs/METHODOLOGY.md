# Methodology

## Source Verification

Every relationship in the dataset is backed by a primary source URL. Each source was verified through a multi-step pipeline:

1. **Direct fetch** with browser-equivalent headers (`requests` + `trafilatura` for text extraction)
2. **Wayback Machine** fallback for pages that block automated access
3. **PDF extraction** via `pdftotext` for government documents
4. **Manual verification** for sources that remained uncheckable after automated methods

A relationship is classified as:
- **SUPPORTED**: source page contains both parties' names and describes the claimed relationship
- **PARTIAL**: source mentions one party or describes a related but not identical relationship
- **UNCHECKABLE**: source could not be fetched or parsed

Only SUPPORTED relationships appear in the final dataset.

## Influence Scoring Rubric

```
influence_score = tie_strength + aid_power + aid_stance + 0.5
```

### Tie Strength (0.5 / 1.5 / 2.5)

| Score | Definition | Examples |
|---|---|---|
| 0.5 | Group-level only | Delegation-wide letter; NGA committee membership |
| 1.5 | Documented individual interaction | Named in press release; specific meeting; staff overlap |
| 2.5 | Direct collaboration | Joint deal/legislation; endorsement; employment; state grant |

### Aid Power (0 / 0.5 / 1.0)

| Score | Definition |
|---|---|
| 0 | Not a member of Congress or senior official |
| 0.5 | Sitting member of Congress or senior administration official |
| 1.0 | Member of Appropriations, Foreign Affairs, or Senate Foreign Relations; or party leadership |

Committee assignments sourced from official congressional websites (house.gov, senate.gov) as of October 2026.

### Aid Stance (0 / 0.5 / 1.0)

| Score | Definition | Source requirement |
|---|---|---|
| 0 | Supported the 2025 foreign-aid cuts | Roll call vote or public statement with URL |
| 0.5 | No public record on 2025 cuts | — |
| 1.0 | Opposed the 2025 cuts | Roll call vote or public statement with URL |

The primary proxy for aid stance is the vote on the **Rescissions Act of 2025 (H.R. 4)**, which cut $7.9 billion from international assistance programs:
- House: Roll Call 203, July 18, 2025 ([clerk.house.gov](https://clerk.house.gov/Votes/2025203))
- Senate: Vote 411, July 17, 2025 ([senate.gov](https://www.senate.gov/legislative/LIS/roll_call_votes/vote1191/vote_119_1_00411.htm))

## Country Group Classification

The "high-cut" country group used in the trade analysis is defined as:

**Criterion**: CGD-estimated 2025 USAID cut ≥ 0.5% of GNI, OR ≥ $200M absolute

**Source**: Sandefur and Kenny, "USAID Cuts: New Estimates at the Country Level," Center for Global Development, March 26, 2025 (corrected August 2025). FY2025 realized figures from Kenny and Sandefur, "USAID Spending at the Country and Sector Level," CGD, April 2026.

**31 countries** in the group, including Honduras, Colombia, Ethiopia, DRC, Kenya, Tanzania, Bangladesh, South Africa, Uganda, Malawi, Mozambique, and others.

## Trade Data

All trade figures come from the U.S. Census Bureau International Trade API:

- **Exports endpoint**: `api.census.gov/data/timeseries/intltrade/exports/statehs`
- **Imports endpoint**: `api.census.gov/data/timeseries/intltrade/imports/statenaics`
- **State filter**: `STATE=NC`
- **Pull date**: October 26, 2026

Textile inputs are defined as HS chapters 50–60 (fibers, yarns, and fabrics; excludes finished apparel in chapters 61–63).
