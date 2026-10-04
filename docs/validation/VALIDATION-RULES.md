# Validation Rules

Separate four layers:
1. **Structural** — required information for a document profile exists.
2. **Semantic** — normalized values are internally valid.
3. **Cross-document** — related evidence agrees across documents.
4. **Business** — customer/process policy and authorization.

Business validation belongs in deterministic policy/rules boundaries, not opaque model behavior.

## Finding contract
```json
{
  "code":"INVOICE_PO_AMOUNT_MISMATCH",
  "severity":"ERROR",
  "documents":["DOC-INVOICE-001","DOC-PO-008"],
  "expected":12000000,
  "actual":15450000,
  "message":"Invoice amount exceeds remaining PO value.",
  "source":"RULE_ENGINE",
  "rule_version":"2.4"
}
```

Use stable machine-readable codes. Suggested severities: `INFO`, `WARNING`, `ERROR`, `BLOCKING`. Human messages may be localized.