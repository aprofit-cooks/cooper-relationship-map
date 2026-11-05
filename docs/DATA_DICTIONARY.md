# Data Dictionary: relationships.csv

Each row represents one documented relationship between Roy Cooper and another person or organization.

## Columns

| Column | Type | Description |
|---|---|---|
| `node_a` | string | Always "Roy Cooper" |
| `node_b` | string | The other party in the relationship |
| `node_b_type` | string | Type: senator, representative, state_official, admin_official, business, diplomat, party_org, nonprofit, military |
| `candidate_network` | string | Always "Cooper" |
| `relationship_type` | string | Category: disaster_response, legislative/governing, business_recruitment, campaign/endorsement, professional |
| `relationship_detail` | string | Specific relationship identifier (e.g., `HB2_repeal_compromise`, `helene_letter_signatory`) |
| `relationship_valence` | string | positive, adversarial, or neutral |
| `period` | string | Year or year range of the relationship |
| `evidence` | string | Description of the specific dated interaction, exactly as sourced |
| `source_url` | string | URL of the primary source document |
| `tie_strength` | float | 0.5, 1.5, or 2.5 (see methodology) |
| `aid_power` | float | 0, 0.5, or 1.0 (see methodology) |
| `aid_stance` | float | 0, 0.5, or 1.0 (see methodology) |
| `aid_stance_known` | boolean | Whether the aid stance is based on a documented source |
| `influence_score` | float | Composite score, 1.0–5.0 |
| `cross_party` | boolean | True if the person's party differs from Cooper's (Democrat) |
| `is_sitting_member` | boolean | True if currently in Congress |
| `is_nc_delegation` | boolean | True if part of the NC congressional delegation |
| `committee_assignments` | string | Current committee assignments (for sitting members) |
| `aid_committee_flag` | string | Non-empty if on Appropriations, Foreign Affairs, or SFRC |
| `stance_on_aid` | string | Full text of the person's position on the 2025 aid cuts |
| `stance_source` | string | URL documenting the aid-cut stance |

## Roles

- **Allies**: Individuals currently in office with a positive relationship and an aid stance of "opposed" or "no record"
- **Cross-party contacts**: Individuals with a positive relationship who are Republican or who supported the 2025 cuts
- **Adversarial**: Relationship marked as adversarial in valence (currently only Donald Trump)
