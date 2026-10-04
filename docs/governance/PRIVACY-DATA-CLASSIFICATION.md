# Privacy and Data Classification

## Baseline classes

- `PUBLIC`: approved for public disclosure.
- `INTERNAL`: internal operational information.
- `CONFIDENTIAL`: business/financial/personal information requiring controlled access.
- `RESTRICTED`: highest-impact information requiring explicitly limited handling.

Actual organization policy may map or extend these classes.

## Processing rules

Classification influences storage, logging, retention, model-provider eligibility, reviewer access, export, and dataset/training eligibility.

A document and its derivatives may have different technical forms but retain equivalent or higher sensitivity. OCR text is not less sensitive merely because it is derived.

## AI provider boundary

Before sending content to any external/managed model, deployment policy must establish whether the data class, tenant agreement, region, retention/training terms and security controls permit that provider.

## Minimization

Send only information required for the processing purpose. Avoid putting complete documents into prompts when a bounded page/region or deterministic parser output is sufficient.