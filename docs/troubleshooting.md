# Troubleshooting Notes

This document captures the useful engineering lessons from the implementation without reproducing every exploratory step.

## 1. Purview Test Connection returned 403

### Symptom

The Purview scan connection test returned `Forbidden`.

### Investigation

The storage account had public network access enabled, so network reachability was not the primary blocker.

RBAC and identity assignments were reviewed.

### Final access model

- Purview Managed Identity → `Storage Blob Data Reader`
- ADF Managed Identity → `Storage Blob Data Contributor`

The Purview role is intentionally read-only in the final configuration.

### Lesson

Do not immediately widen permissions permanently because a connection test fails.

Validate network reachability, identity, role scope, inheritance, and propagation before accepting broader privileges as the final design.

---

## 2. Duplicate RBAC assignment

A direct role assignment was initially visible on the `governed` container in addition to the role inherited from the storage account.

The direct assignment was removed.

Final state:

```text
Storage account role assignment
        ↓
Inherited by governed
```

### Lesson

Inherited RBAC is sufficient when the parent scope is intentionally selected. Duplicate child assignments create noise without adding value.

---

## 3. Classification false positive

`postal_code` contains synthetic Mexican postal codes but Purview classified the column as `U.S. Zip Codes`.

### Decision

The result was retained and documented instead of hidden.

### Lesson

Automated classification is a discovery accelerator, not an infallible business truth.

---

## 4. No suitable phone classifier

The synthetic phone data uses +52.

The manual classification options shown in the UI were EU/U.S.-specific.

### Decision

No incorrect classification was forced onto the field.

### Lesson

An unclassified field is better than knowingly incorrect governance metadata.

---

## 5. Lineage did not appear immediately

ADF Monitor reported lineage successfully, but the Purview lineage view initially appeared empty.

### Resolution

Refresh the asset / lineage view after propagation.

### Lesson

Successful lineage reporting and catalog visualization are asynchronous steps.

---

## 6. Column-level claim discipline

Purview displayed source and target schemas inside the lineage graph.

However, individual column-to-column edges were not shown.

### Decision

The project claims:

- file-level automated lineage;
- schema-aware lineage visualization.

It does not claim explicit column-level lineage.
