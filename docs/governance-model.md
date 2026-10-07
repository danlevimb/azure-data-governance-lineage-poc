# Governance Model

## Governed asset

Primary asset:

`governed/customer_master.csv`

The dataset is synthetic and exists only for the portfolio POC.

## Technical metadata

Purview discovers:

- asset path
- asset type
- schema
- column names
- built-in classifications

The CSV schema contains 20 columns.

## Automatic classifications observed

| Column | Purview classification |
|---|---|
| `full_name` | All Full Names |
| `email` | Email Address |
| `birth_date` | Date of Birth |
| `city` | World Cities |
| `postal_code` | U.S. Zip Codes |
| `registration_ip` | Personal IP Address |

## Manual classifications

| Column | Steward classification |
|---|---|
| `street_address` | All Physical Addresses |
| `payment_card_number_test` | Credit Card Number |

## Human review finding

The synthetic dataset uses Mexican postal codes.

Purview classified `postal_code` as **U.S. Zip Codes**.

This result is intentionally preserved as a false-positive example because it demonstrates that:

> Classification engines identify patterns; governance still requires human context.

The `phone_number` field uses +52 values. The manual built-in options presented in the UI were EU/U.S.-specific, so an inaccurate classification was deliberately not applied.

## Stewardship

Contacts assigned to the governed asset:

- **Owner:** Dan Fabric Lab
- **Expert:** Dan Fabric Lab

For this individual POC the same lab identity serves both roles. In an enterprise implementation these responsibilities would typically be separated across people or groups.

## Business glossary

Glossary:

`Customer Data Governance`

Term:

`Customer Master`

The glossary term is associated with `customer_master.csv`.

## Asset description

The catalog description explains:

- the dataset is synthetic;
- the profile/contact/payment fields are fictitious;
- the asset exists to demonstrate discovery, classification, stewardship, glossary mapping, and lineage;
- no real personal or payment data is included.

## Governance principle

Technical discovery answers **what exists**.

Human curation answers **what it means and who is responsible for it**.

This project demonstrates both.
