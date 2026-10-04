# Duplicate Detection and Idempotency

These solve different problems.

## Submission idempotency

An `Idempotency-Key` prevents accidental repeat side effects for the same tenant/request scope. Reusing a key with materially different input returns `IDEMPOTENCY_CONFLICT`.

## Exact content duplicate

A cryptographic content hash can identify byte-identical input. Deduplication remains tenant/policy scoped; never disclose that another tenant possesses the same document.

## Near duplicate

Visually/textually similar documents may be detected using optional fingerprints/embeddings/perceptual hashes. A near-duplicate score is probabilistic evidence, not identity.

## Business duplicate

"Same invoice submitted twice" is a business concept and may require normalized issuer, invoice number, amount/date, authoritative vendor identity, and historical context. It belongs to deterministic/probabilistic duplicate findings plus business policy, not raw SHA-256 alone.

## Storage

Deduplication may reuse safe internal processing artifacts where isolation and policy permit, but logical document identities and audit trails remain distinct.