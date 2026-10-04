# Entity Resolution Boundary

**Class:** Normative

Document extraction and authoritative identity resolution are distinct operations.

Example:

```text
Observed document text: "PT Contoh Abadi"
             |
             v
Extracted party candidate
             |
             v
Resolver / master-data lookup
             |
       +-----+------+
       |            |
   unresolved    resolved
                    |
                    v
       ERP/vendor authority + ID
```

## Requirements

- Extracted names/identifiers MUST remain traceable to document evidence.
- A resolved entity MUST identify the authoritative namespace/source and entity ID.
- Model similarity alone MUST NOT silently establish an authoritative identity when deployment policy requires deterministic/master-data confirmation.
- Ambiguous candidates MUST remain distinguishable from a resolved identity.
- Resolution provenance MUST identify the resolver/component version.
- Reconciliation rules MUST distinguish observed document values from authoritative business/master values.

The core specification does not mandate ERP, MDM, database, matching algorithm, or provider.
