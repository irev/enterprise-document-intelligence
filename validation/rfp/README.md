# RFP Validation Pack

This pack validates the v0.9 specification against representative synthetic Request-for-Payment / Accounts-Payable scenarios.

**It is not a normative RFP product specification.** RFP is used as a demanding reference domain to discover missing or ambiguous core contracts.

## Rules

- All examples are synthetic.
- Business authorization remains outside Document Intelligence.
- Expected outcomes reference observable semantics, not implementation technology.
- A failed scenario may reveal an implementation defect, profile defect, or specification gap; these must be distinguished.
- No new core requirement is introduced merely because one RFP customer might need it.

## Scenario set

| ID | Scenario | Primary stress |
|---|---|---|
| RFP-001 | Clean PO-backed invoice | happy path |
| RFP-002 | Invoice/PO reference mismatch | cross-document reconciliation |
| RFP-003 | Missing conditional tax invoice | requirement policy |
| RFP-004 | Blurred total amount | field state + review |
| RFP-005 | Multi-document PDF | segmentation |
| RFP-006 | Duplicate invoice resubmission | identity vs business duplicate |
| RFP-007 | Vendor name ambiguity | entity resolution |
| RFP-008 | Prompt injection in invoice notes | trust boundary |
| RFP-009 | Reprocessing after better OCR/model | immutability/versioning |
| RFP-010 | Concurrent reviewer correction | review concurrency |
| RFP-011 | Locale-ambiguous monetary number | normalization |
| RFP-012 | Unknown supporting document | abstention/UNKNOWN |
| RFP-013 | Invoice amount exceeds authoritative PO remaining | authoritative context |
| RFP-014 | One invoice contains many line items/table | structured values |
| RFP-015 | Encrypted supporting PDF | inaccessible content |
| RFP-016 | Same bytes uploaded for different RFP submissions | source vs logical identity |

See `scenarios.synthetic.json` and `VALIDATION-REPORT.md`.
