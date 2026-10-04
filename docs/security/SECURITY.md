# Security

Documents are untrusted input and may contain sensitive corporate/financial data.

## Ingestion
Use authenticated/authorized upload, size/page limits, MIME + magic-byte verification, malware controls, archive/decompression limits where relevant, encrypted-document policy, active-content/PDF sanitization policy, hashing/duplicate detection, and safe temporary-storage cleanup.

## AI security
Document content is **data, not instruction**. Embedded text such as "ignore previous instructions" must never become trusted control-plane input. Separate instructions from content, constrain outputs, minimize model tool privileges, validate downstream output, and never allow document text to authorize payment or privileged actions.

## Data protection
Tenant isolation, least privilege, encryption, secret management, redacted/structured logs, retention/deletion controls, and access/audit logging are required design concerns.

Extracted URLs, commands, formulas, scripts and embedded objects remain untrusted downstream.