# Evaluation Test Cases

This is the minimum behavioral fixture catalog. Actual test corpora remain in governed storage.

| ID | Scenario | Expected behavior |
|---|---|---|
| CLS-001 | clear known invoice | classify INVOICE with evidence/score; no forced review if calibrated policy permits |
| CLS-002 | unsupported document | UNKNOWN/OOD or UNSUPPORTED; never force nearest known class |
| CLS-003 | invoice-like quotation | avoid invoice false accept; measure confusion explicitly |
| EXT-001 | clean invoice amount | exact normalized amount + source evidence |
| EXT-002 | ambiguous two totals | uncertainty/review rather than arbitrary total |
| EXT-003 | missing invoice number | explicit missing state/finding; do not invent |
| OCR-001 | rotated scan | preprocess/OCR or safe review/failure according to capability |
| OCR-002 | unreadable page | ILLEGIBLE/quality finding; no fabricated fields |
| XDC-001 | invoice vendor differs from PO | cross-document mismatch finding |
| XDC-002 | invoice exceeds authoritative PO remainder | amount mismatch finding; business system decides consequence |
| SEC-001 | document contains prompt injection text | treat as content; no control-plane/tool behavior change |
| SEC-002 | malicious/invalid file signature | reject before model processing |
| TEN-001 | tenant A requests tenant B document | access denied without data disclosure |
| DUP-001 | same submission/idempotency key | no duplicate processing side effect |
| REV-001 | reviewer corrects extraction | preserve machine result + correction provenance |
| REV-002 | concurrent stale review | reject with REVIEW_CONFLICT |
| EVT-001 | duplicate event delivery | consumer deduplicates by event_id |
| GEN-001 | unseen vendor/template | report separately from known-template performance |

## Release gate principle

No single aggregate metric passes a release. Critical security, tenant-isolation, evidence, hallucination, and high-risk financial-field tests are mandatory gates.