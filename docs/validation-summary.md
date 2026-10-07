# Validation Summary

**Validation date:** 2026-10-07

## Final result

```text
Functional MVP validation: PASS
```

## Validation matrix

| Capability | Result |
|---|---|
| ADLS Gen2 source registration | PASS |
| Managed Identity authentication | PASS |
| Azure RBAC authorization | PASS |
| Scoped Purview scan | PASS |
| Dataset discovery | PASS |
| 20-column schema extraction | PASS |
| Automatic classification | PASS |
| Manual classification | PASS |
| Asset description | PASS |
| Owner / Expert contacts | PASS |
| Business glossary association | PASS |
| ADF ↔ Purview integration | PASS |
| ADF Copy execution | PASS |
| ADF lineage reporting | PASS |
| Automated file-level lineage | PASS |
| Schema-aware lineage visualization | PASS |
| Re-scan after lineage creation | PASS |
| Curated metadata persistence | PASS |
| Contact persistence | PASS |
| Lineage persistence | PASS |

## Scan progression

```text
Run 1 → 2 detected / 2 ingested
Run 2 → 3 detected / 3 ingested
Run 3 → 5 detected / 5 ingested
```

The execution counts are preserved as operational evidence only.

No one-to-one business interpretation is asserted for every internal asset count without direct catalog evidence.

## Persistence test

After ADF lineage was successfully generated, Purview scanned the source again.

The following remained associated with the governed asset:

- description
- glossary term
- automatic classifications
- manual classifications
- Owner
- Expert
- ADF lineage

This proves that recurring technical discovery did not erase curated governance context.

## Lineage claim boundary

Demonstrated:

- source file → ADF Copy process → governed target file
- source and target schemas visible in lineage

Not demonstrated:

- explicit column-to-column lineage edges

That limitation is documented intentionally rather than hidden.
