# RFP Document Requirement Matrix

This specification defines **how** RFP document requirements are represented. It intentionally does not declare one universal matrix because required documents depend on tenant policy, payment category, procurement path, tax treatment, amount thresholds, and other authoritative business attributes.

## Separation of concerns

```text
Document taxonomy:
  "This file is a TAX_INVOICE."

RFP requirement policy:
  "For this payment context, a TAX_INVOICE is required."

Workflow decision:
  "Submission cannot proceed until the required evidence is satisfied."
```

These are separate responsibilities.

## Requirement values

- `REQUIRED`: at least the configured minimum count must be satisfied.
- `OPTIONAL`: accepted but absence is not a requirement failure.
- `CONDITIONAL`: resolved using an explicitly named deterministic condition.
- `NOT_ALLOWED`: document should not satisfy this profile and may be flagged.

## Authoritative context

Conditions must use business attributes supplied/resolved by the RFP/rules layer. The AI must not infer an approval threshold, tax applicability, vendor entitlement, or payment category and then treat that inference as authoritative policy.

## Example

See `examples/rfp/requirement-profile.synthetic.json`.

## Versioning

Every evaluation of requirements records the profile ID/version and the business-context snapshot/reference used. A changed policy must not rewrite historical evaluation provenance.