# Security Hardening Profile

This checklist complements the threat model. Exact controls depend on deployment risk.

## Ingestion worker
- run untrusted parsers with least privilege and isolation;
- no ambient cloud/admin credentials;
- restrict outbound network access where feasible;
- enforce CPU/memory/time/page/decompression limits;
- use patched parser/OCR dependencies;
- quarantine rejected/suspicious files according to policy.

## Model workers
- no authority to approve payments or mutate ERP/RFP business records;
- tool/network access disabled unless explicitly required;
- outbound destinations allow-listed for managed providers;
- structured-output validation before persistence/use.

## API/review
- tenant-scoped authorization on every resource;
- object-level authorization, not only UI hiding;
- CSRF protections where cookie authentication is used;
- rate/size limits;
- optimistic concurrency for review;
- security-sensitive actions auditable.

## Storage
- encryption at rest/in transit;
- separate secret storage;
- scoped service identities;
- backup/restore tested;
- lifecycle/retention policies;
- no public buckets by default.

## Supply chain
- dependency scanning and update policy;
- pin/review CI actions and production images according to organizational policy;
- artifact provenance/checksums for models;
- protect main/release branches;
- no secrets in repository or CI output.

## Logging
Never log complete document text, credentials, authorization headers, model-provider secrets, or unrestricted prompts containing confidential content.