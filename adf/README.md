# Azure Data Factory Assets

The ADF implementation is intentionally small and exists to produce a traceable source-to-governed flow.

## Linked service

`ls_adls_governance_dan_dev`

Type:

`Azure Data Lake Storage Gen2`

Authentication:

`System-assigned Managed Identity`

## Source dataset

`ds_customer_master_source_csv`

Path:

```text
landing/customer_master_source.csv
```

Format:

`DelimitedText / CSV`

The schema was imported from the storage connection.

## Target dataset

`ds_customer_master_governed_csv`

Path:

```text
governed/customer_master.csv
```

Format:

`DelimitedText / CSV`

## Pipeline

`pl_customer_master_lineage`

Activity:

`Copy_CustomerMaster_To_Governed`

The activity uses explicit 1:1 source-to-target column mapping.

## Purview integration

ADF is connected to the Microsoft Purview account and pipeline lineage reporting is enabled.

ADF Monitor validated:

```text
Copy activity: Succeeded
Lineage reporting: Succeeded
```

Purview subsequently displayed:

```text
customer_master_source.csv
        ↓
Copy_CustomerMaster_To_Governed
        ↓
customer_master.csv
```

The repository documents the implementation rather than publishing fabricated ADF export JSON. Native ADF artifacts can be added later if the project is connected to Git source control or explicitly exported.


## Versioned ARM snapshot

A project-scoped ARM snapshot derived from the real Azure Data Factory export is versioned under:

```text
adf/arm/
├── ARMTemplateForFactory.project.json
├── ARMTemplateParametersForFactory.project.json
└── EXPORT_AUDIT.md
```

The published snapshot contains only the resources used by this POC:

- `ls_adls_governance_dan_dev`
- `ds_customer_master_source_csv`
- `ds_customer_master_governed_csv`
- `pl_customer_master_lineage`
- `Copy_CustomerMaster_To_Governed`
- explicit 20-column 1:1 mapping

The raw ADF export also contained an unrelated Self-Hosted Integration Runtime and factory-level identity identifiers. Those were intentionally excluded from the public snapshot. See [arm/EXPORT_AUDIT.md](arm/EXPORT_AUDIT.md).
