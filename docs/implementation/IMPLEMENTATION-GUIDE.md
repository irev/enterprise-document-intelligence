# Implementation Guide

## Recommended module boundaries

```text
Api
Application
Domain/Contracts
Ingestion
DocumentUnderstanding
Classification
Extraction
Validation
Review
Persistence
Messaging
Observability
ProviderAdapters
```

Names may differ by language/framework; dependency direction matters more than folder naming.

## Dependency rule

Canonical contracts and domain policy must not depend on a model/OCR vendor SDK. Provider adapters depend inward on platform interfaces/contracts.

## Processing transaction model

Do not hold a database transaction open across OCR/model calls. Persist state transitions and use idempotent work units. External model calls are fallible distributed operations.

## Money and dates

Use decimal-safe money types and explicit currencies. Normalize dates without inventing timezone semantics for date-only document fields.

## Concurrency

Use optimistic concurrency/versioning for human review and mutable processing metadata. Completed result versions remain immutable.

## Testing pyramid

- schema/contract validation;
- unit tests for normalization and deterministic rules;
- adapter contract tests;
- integration tests for storage/queue/providers;
- evaluation harness against governed datasets;
- end-to-end security/tenant-isolation tests.

## Configuration

Separate platform configuration, tenant policy, secrets, and model release configuration. Never use source-code branches as the primary tenant customization mechanism.