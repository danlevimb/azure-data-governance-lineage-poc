<p align="center">
  <img src="diagrams/banner.jpg" width="1000"/>
</p>

<h1 align="center">Azure Data Governance & Lineage POC</h1>

<p align="center">
  Making data discoverable, understandable, owned, classified, and traceable.
</p>

<p align="center">
  <a href="docs/architecture.md">Architecture</a> |
  <a href="docs/README.md">Documentation</a> |
  <a href="docs/evidence/README.md">Evidence</a> |
  <a href="docs/governance-model.md">Governance Model</a> |
  <a href="docs/validation-summary.md">Validation</a>
</p>

---

## The problem

A technically valid dataset is not fully trustworthy if consumers cannot answer:

- What is this asset?
- Where did it come from?
- Who owns it?
- Which fields may contain sensitive information?
- Which business concept does it represent?
- What process produced it?

The challenge is not simply to store or move data.

The challenge is to make **data discoverable, understandable, owned, classified, and traceable**.

---

## The idea

This project uses a deliberately small Azure data estate to demonstrate practical governance mechanics with:

- Microsoft Purview
- Azure Data Lake Storage Gen2
- Azure Data Factory
- Managed Identity
- Azure RBAC
- metadata discovery
- classification
- stewardship
- business glossary
- automated lineage

The scope is intentionally compact. The goal is not to simulate an enterprise-wide governance program; it is to prove the reasoning and implementation patterns behind a defensible governance MVP.

---

## What this project demonstrates

- Microsoft Purview registration and scoped ADLS Gen2 scanning
- Managed Identity and Azure RBAC
- Schema discovery for CSV assets
- Automatic and manual data classification
- Human review of classifier false positives
- Asset descriptions and stewardship contacts
- Business glossary association
- Azure Data Factory → Microsoft Purview lineage integration
- Automated file-level lineage from source to governed target
- Schema-aware lineage visualization
- Re-scan validation proving curated governance metadata persists

## Architecture

> Visual diagrams are being finalized to match the portfolio's established Azure project style.

### Visual technical guides

- End-to-end governance architecture — planned
- Discovery → stewardship → lineage flow — planned
- Governance controls & persistence validation — planned

```mermaid
flowchart LR
    S["ADLS Gen2<br/>landing/customer_master_source.csv"]
    A["Azure Data Factory<br/>pl_customer_master_lineage<br/>Copy_CustomerMaster_To_Governed"]
    T["ADLS Gen2<br/>governed/customer_master.csv"]
    P["Microsoft Purview<br/>Data Map / Catalog"]

    S --> A --> T
    S -. metadata / lineage .-> P
    A -. lineage .-> P
    T -. scan / metadata .-> P
```

### Data estate

```text
stdatagovernancedan02
├── landing
│   └── customer_master_source.csv
└── governed
    └── customer_master.csv
```

The sample data is fully synthetic.

## Governance flow

```mermaid
flowchart TD
    R["Register ADLS Gen2 source"]
    S["Scoped Purview scan"]
    D["Discover asset + schema"]
    C["Automatic classification"]
    H["Human review / manual classification"]
    B["Description + Owner + Expert + Glossary"]
    L["ADF automated lineage"]
    V["Re-scan persistence validation"]

    R --> S --> D --> C --> H --> B --> L --> V
```

## Key implementation decisions

### 1. Least-privilege identities

Purview uses its Managed Identity with **Storage Blob Data Reader** at storage-account scope.

ADF uses its Managed Identity with **Storage Blob Data Contributor** because the pipeline writes the governed target.

Authorization scope and discovery scope are intentionally separate controls: Purview can authenticate to the storage account, while the scan itself is deliberately limited to `governed`.

### 2. Small but believable governed asset

The main governed asset is:

`governed/customer_master.csv`

Purview extracted a 20-column schema and identified several built-in classifications.

### 3. Human review matters

Automatic classifications observed included:

| Column | Classification |
|---|---|
| `full_name` | All Full Names |
| `email` | Email Address |
| `birth_date` | Date of Birth |
| `city` | World Cities |
| `postal_code` | U.S. Zip Codes |
| `registration_ip` | Personal IP Address |

Manual classifications added:

| Column | Classification |
|---|---|
| `street_address` | All Physical Addresses |
| `payment_card_number_test` | Credit Card Number |

The `postal_code` field contains synthetic Mexican postal codes, but Purview classified it as **U.S. Zip Codes**. That false positive is deliberately retained because it demonstrates an important governance principle:

> Automated classification accelerates discovery, but human stewardship is still required to validate business context.

The synthetic `phone_number` values use +52. The available built-in manual choices shown in the UI were EU/U.S.-specific, so no incorrect classifier was forced onto the field.

## Business metadata

The governed asset includes:

- a business-facing description
- Owner: `Dan Fabric Lab`
- Expert: `Dan Fabric Lab`
- Business glossary:
  - `Customer Data Governance`
  - `Customer Master`

## Automated lineage

ADF writes the governed asset through:

`pl_customer_master_lineage`

with activity:

`Copy_CustomerMaster_To_Governed`

Purview captured the file-level lineage:

```text
customer_master_source.csv
        ↓
Copy_CustomerMaster_To_Governed
        ↓
customer_master.csv
```

Source and target schemas are visible in the lineage experience.

### Claim boundary

This project demonstrates:

- automated file-level lineage
- ADF process lineage
- schema-aware lineage visualization

It does **not** claim explicit column-to-column lineage edges because those were not demonstrated in the UI.

## Persistence validation

After lineage was established, the Purview scan was executed again.

The re-scan successfully refreshed technical metadata while preserving:

- asset description
- business glossary association
- automatic classifications
- manual classifications
- Owner / Expert contacts
- ADF lineage

This is one of the strongest validations in the project: technical rediscovery did not erase curated governance context.

## Evidence

Selected public evidence is available under:

`docs/evidence/screenshots/`

Core proof points include:

- scoped Purview scan
- business glossary and classifications
- ADF ↔ Purview integration
- successful lineage reporting in ADF Monitor
- source → process → target lineage in Purview
- schema-aware lineage visualization
- metadata persistence after re-scan
- lineage persistence after re-scan

See [docs/evidence/README.md](docs/evidence/README.md).

## Repository structure

```text
.
├── README.md
├── adf/
│   └── README.md
├── docs/
│   ├── architecture.md
│   ├── governance-model.md
│   ├── validation-summary.md
│   ├── troubleshooting.md
│   └── evidence/
│       ├── README.md
│       └── screenshots/
├── sample-data/
│   ├── customer_master_source.csv
│   └── customer_master.csv
└── .gitignore
```

## Validation result

```text
Functional MVP validation: PASS
```

Validated areas:

- source registration
- identity / RBAC
- scoped scanning
- schema extraction
- classification
- business metadata
- stewardship
- glossary
- ADF integration
- lineage reporting
- file-level lineage
- schema-aware lineage
- metadata persistence
- contact persistence
- lineage persistence

## Known MVP exclusions

This project intentionally does not implement:

- enterprise approval workflows
- organization-wide stewardship
- private endpoint network isolation
- policy enforcement
- scheduled production scans
- enterprise-scale domain / collection hierarchy
- custom Mexican phone classifier
- explicit column-to-column lineage claim

These are scope boundaries, not hidden gaps.

## Why this matters

The portfolio already demonstrates how to ingest, transform, serve, monitor, and operate data on Azure.

This project adds the next professional question:

> Can the data be understood, trusted, owned, discovered, and traced?

That is the role of governance.

## Status

**Functional MVP validated — public packaging and final QA in progress.**
