# RFP / Accounts Payable Reference Profile

This is the first reference use case. It demonstrates platform contracts without redefining generic document types as RFP-specific types.

## Typical supporting documents

Depending on configured payment type and company policy:
- invoice;
- purchase order / purchase request;
- contract or work order;
- tax document;
- delivery/goods receipt/service acceptance;
- payment proof where applicable;
- internal memo/approval.

The exact requirement matrix is **tenant business configuration**, not a universal platform invariant.

## Example reconciliation

Potential checks:
- invoice vendor matches PO/contract party;
- invoice PO reference matches the submitted PO;
- invoice currency is compatible with PO/contract;
- invoice amount does not exceed an authoritative remaining amount supplied by the business system;
- tax identifiers/amounts are structurally and semantically valid;
- required evidence is present for the configured payment profile.

## Critical boundary

The Document Intelligence platform may report:
`INVOICE_PO_AMOUNT_MISMATCH`.

The RFP/business system decides whether that finding blocks submission, requires approval, or follows another authorized policy.

## Integration inputs

Business applications may supply authoritative context such as payment-request ID, payment type, vendor master ID, PO ID, expected currency, or document-requirement profile. Model extraction must not silently replace authoritative master data.

## Reference outcome

The platform returns normalized fields, evidence, confidence, findings and review state. It does not approve or execute payment.