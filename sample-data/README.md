# Synthetic Sample Data

The files in this directory are public-safe synthetic samples matching the schema used in the governance POC.

- `customer_master_source.csv` represents the landing/source asset.
- `customer_master.csv` represents the governed target asset.

The public repository keeps a compact representative sample rather than relying on any real personal information.

Safety notes:

- email addresses use `example.com`;
- IPv4 values use documentation-only ranges;
- payment-card values are standard test numbers;
- names, addresses, dates, account attributes, and purchase values are fictitious.

The Azure implementation used the same 20-column schema for Purview schema discovery, classification, stewardship, glossary mapping, and lineage validation.
