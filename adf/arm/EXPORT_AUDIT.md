# ADF ARM Export Audit

Source: Azure Data Factory ARM template export reviewed on 2026-10-07.

## Public packaging decision

The raw export contained one unrelated Self-Hosted Integration Runtime (`shir-governance-sql-dev`) from the factory. It is not part of this governance POC and was removed from the public project-scoped snapshot.

The public snapshot preserves the exported resources used by this project:

- linked service: `ls_adls_governance_dan_dev`
- source dataset: `ds_customer_master_source_csv`
- target dataset: `ds_customer_master_governed_csv`
- pipeline: `pl_customer_master_lineage`
- activity: `Copy_CustomerMaster_To_Governed`
- explicit 20-column 1:1 mapping

## Security review

No passwords, account keys, SAS signatures, connection strings, client secrets, access tokens, subscription IDs, user emails, or personal credentials are present in the published project-scoped template.

The storage endpoint and Azure resource names are intentionally retained because they are already part of the public project narrative and are parameterized in the ARM template.

The factory-level export under the original ZIP was not published because it contained tenant/principal identifiers and unrelated factory configuration that do not improve the portfolio narrative.
