# Threat Model

## Protected assets

Corporate documents, extracted financial/identity data, tenant configuration, model/prompt configuration, credentials, audit history, and downstream business actions.

## Trust boundaries

1. uploader/source -> ingestion;
2. stored document -> parser/OCR/model runtime;
3. model output -> validation/rules;
4. platform -> human reviewer;
5. platform -> business system;
6. tenant A -> shared platform -> tenant B.

## Principal threats

| Threat | Example | Primary controls |
|---|---|---|
| Malicious file | exploit parser/PDF engine | type verification, sandboxing/isolation, patched parsers, malware controls |
| Resource exhaustion | decompression bomb / huge PDF | byte/page/time/memory limits |
| Prompt injection | document instructs model/tools | content/instruction separation, constrained output, least tool privilege |
| Cross-tenant exposure | result retrieved by wrong tenant | tenant-scoped authz and storage/query boundaries |
| Data exfiltration | sensitive text in logs | structured/redacted logging, data minimization |
| Model hallucination | invented invoice field | evidence requirement, confidence, validation, HITL |
| Poisoned feedback | malicious reviewer correction | reviewer authorization, provenance, governed training admission |
| Duplicate/replay | repeated upload/event | hashing, idempotency keys, event dedupe |
| Supply-chain compromise | model/package/parser artifact | pinned/verifiable artifacts, dependency governance |
| Privilege escalation | AI triggers payment/action | AI has no business authorization capability |

## Fail-safe rule

If integrity, tenant identity, document safety, required evidence, or processing state cannot be established, fail closed for privileged downstream actions and route to an explicit error/review state.