# Public Evidence

This directory contains a deliberately small, curated set of screenshots that support the main engineering claims in the project.

Portal screenshots are stored as **PNG** to preserve small UI text and avoid lossy compression artifacts.

## Published screenshot evidence

| ID | Screenshot | What it shows | What it demonstrates |
|---|---|---|---|
| GVL-03 | [`GVL-03_scan_scope_governed_only.png`](screenshots/GVL-03_scan_scope_governed_only.png) | Purview scan scope restricted to the governed data area | Discovery was intentionally limited to the assets included in the Governance MVP rather than the wider estate |
| GVL-05 | [`GVL-05_asset_glossary_and_classifications.png`](screenshots/GVL-05_asset_glossary_and_classifications.png) | Governed asset metadata with glossary association and schema classifications | Business context and technical classifications were applied to the cataloged asset |
| GVL-06 | [`GVL-06_adf_purview_lineage_connected.png`](screenshots/GVL-06_adf_purview_lineage_connected.png) | ADF connected to Microsoft Purview for lineage reporting | The orchestration service is integrated with the governance platform instead of operating as an isolated pipeline |
| GVL-08 | [`GVL-08_adf_lineage_reporting_success.png`](screenshots/GVL-08_adf_lineage_reporting_success.png) | ADF Monitor reporting lineage successfully | Runtime lineage reporting is operational from ADF into Purview |
| GVL-09 | [`GVL-09_purview_file_level_lineage.png`](screenshots/GVL-09_purview_file_level_lineage.png) | Purview lineage graph from source through the ADF process to the governed target | The platform captured automated end-to-end file-level lineage for the implemented flow |
| GVL-10 | [`GVL-10_purview_schema_aware_lineage.png`](screenshots/GVL-10_purview_schema_aware_lineage.png) | Source and target schemas visible in the Purview lineage experience | The lineage view preserves schema context in addition to asset-to-asset relationships |
| GVL-12 | [`GVL-12_metadata_persistence_after_rescan.png`](screenshots/GVL-12_metadata_persistence_after_rescan.png) | Curated description, glossary, and classifications after a subsequent scan | Business metadata persisted across re-scan activity instead of being lost during technical rediscovery |
| GVL-13 | [`GVL-13_contacts_persistence_after_rescan.png`](screenshots/GVL-13_contacts_persistence_after_rescan.png) | Owner and Expert contacts still assigned after re-scan | Stewardship metadata remains associated with the governed asset across catalog refreshes |
| GVL-14 | [`GVL-14_lineage_persistence_after_rescan.png`](screenshots/GVL-14_lineage_persistence_after_rescan.png) | ADF lineage still visible after the subsequent Purview scan | Re-scanning the governed asset did not remove the established lineage relationship |
| GVL-15 | [`GVL-15_final_data_estate.png`](screenshots/GVL-15_final_data_estate.png) | Final landing/source and governed/target data estate | The completed MVP maintains a clear separation between source/landing data and the governed target area |

## Evidence discipline

Screenshots are supporting proof, not the project itself.

The README and technical documents explain the decisions; evidence validates the claims.

Every published screenshot should:

- directly support a README or validation claim;
- avoid duplicate proof;
- preserve enough Azure/Purview context to be technically meaningful.

## Claim boundary

The lineage evidence supports:

- automated file-level lineage;
- ADF process lineage;
- schema-aware lineage visualization.

It does **not** support a claim of explicit column-to-column lineage edges.

That distinction is deliberate and is preserved throughout the repository.
