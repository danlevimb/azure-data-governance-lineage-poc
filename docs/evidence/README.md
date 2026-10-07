# Public Evidence

This directory contains a deliberately small, curated set of screenshots that support the main engineering claims in the project.

The evidence pack is being published in stages during final packaging. Portal screenshots are stored as PNG to preserve small UI text and avoid lossy compression artifacts.

## Published

| ID | Screenshot | What it proves |
|---|---|---|
| GVL-03 | [GVL-03_scan_scope_governed_only.png](screenshots/GVL-03_scan_scope_governed_only.webp) | Purview discovery was intentionally scoped to the governed data area |
| GVL-05 | [GVL-05_asset_glossary_and_classifications.png](screenshots/GVL-05_asset_glossary_and_classifications.webp) | Business glossary association and eight schema classifications |

## Curated next

The following screenshots have already been reviewed as valid project evidence and are queued for public-safe packaging:

| ID | Evidence | Claim |
|---|---|---|
| GVL-06 | ADF ↔ Purview connection | Pipeline lineage integration enabled |
| GVL-08 | ADF Monitor lineage status | ADF successfully reported lineage |
| GVL-09 | Purview file-level lineage | Source → process → governed target |
| GVL-10 | Schema-aware lineage | Source and target schemas visible in lineage |
| GVL-12 | Metadata persistence after re-scan | Description, glossary, and classifications persisted |
| GVL-13 | Contact persistence after re-scan | Owner / Expert persisted |
| GVL-14 | Lineage persistence after re-scan | ADF lineage persisted |
| GVL-15 | Final data estate | landing/source + governed/target final estate |

## Evidence discipline

Screenshots are supporting proof, not the project itself.

The README and technical documents explain the decisions; evidence validates the claims.

Every public screenshot should satisfy all of the following:

- directly supports a README or validation claim;
- contains no unnecessary account-identifying information;
- avoids duplicate proof;
- preserves enough Azure/Purview context to be technically meaningful.

## Claim boundary

The lineage evidence supports:

- automated file-level lineage;
- ADF process lineage;
- schema-aware lineage visualization.

It does **not** support a claim of explicit column-to-column lineage edges.

That distinction is deliberate and is preserved throughout the repository.
