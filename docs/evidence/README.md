# Public Evidence

This directory contains a deliberately small, curated set of screenshots that support the main engineering claims in the project.

Portal screenshots are stored as **PNG** to preserve small UI text and avoid lossy compression artifacts.

## Published

| ID | Screenshot | What it proves |
|---|---|---|
| GVL-03 | [GVL-03_scan_scope_governed_only.png](screenshots/GVL-03_scan_scope_governed_only.png) | Purview discovery was intentionally scoped to the governed data area |
| GVL-05 | [GVL-05_asset_glossary_and_classifications.png](screenshots/GVL-05_asset_glossary_and_classifications.png) | Business glossary association and eight schema classifications |
| GVL-06 | [GVL-06_adf_purview_lineage_connected.png](screenshots/GVL-06_adf_purview_lineage_connected.png) | ADF ↔ Purview lineage integration was enabled |
| GVL-08 | [GVL-08_adf_lineage_reporting_success.png](screenshots/GVL-08_adf_lineage_reporting_success.png) | ADF Monitor reported lineage successfully |
| GVL-09 | [GVL-09_purview_file_level_lineage.png](screenshots/GVL-09_purview_file_level_lineage.png) | Purview captured source → ADF process → governed target lineage |
| GVL-10 | [GVL-10_purview_schema_aware_lineage.png](screenshots/GVL-10_purview_schema_aware_lineage.png) | Source and target schemas are visible in the lineage experience |
| GVL-12 | [GVL-12_metadata_persistence_after_rescan.png](screenshots/GVL-12_metadata_persistence_after_rescan.png) | Description, glossary, and classifications persisted after re-scan |
| GVL-13 | [GVL-13_contacts_persistence_after_rescan.png](screenshots/GVL-13_contacts_persistence_after_rescan.png) | Owner and Expert stewardship contacts persisted after re-scan |
| GVL-14 | [GVL-14_lineage_persistence_after_rescan.png](screenshots/GVL-14_lineage_persistence_after_rescan.png) | ADF lineage persisted after the subsequent Purview scan |
| GVL-15 | [GVL-15_final_data_estate.png](screenshots/GVL-15_final_data_estate.png) | Final landing/source and governed/target data estate |

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
