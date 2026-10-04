# Durable Persistence Requirements

**Class:** Normative platform architecture.

## Principle

A conforming implementation MUST provide durable persistence for state whose loss or stale reconstruction could violate platform guarantees. The specification defines persistence behavior, isolation and consistency requirements; it does not mandate a database product, storage engine, ORM or cloud service.

## Control-plane state

When the corresponding capability is implemented, durable state MUST cover:
- tenants and consuming applications;
- provider registration/configuration and current enablement;
- tenant/application provider authorization;
- versioned execution policies, profiles and other security-relevant configuration;
- configuration/audit history sufficient to explain material decisions.

An execution plan is not an authorization snapshot. Invocation-time authorization MUST evaluate current trusted control-plane state as required by the execution-policy contract.

## Processing and integration state

Durable state MUST be used where required to preserve:
- inbound request identity and scoped idempotency;
- source references, acquisitions and observations;
- processing runs, claims/leases and fencing state;
- immutable/versioned completed results and provenance;
- human-review state and concurrency control;
- transactional outbox/inbox or an equivalent reliable-delivery mechanism;
- outbound delivery attempts and retry state;
- security and operational audit records.

## Consistency requirements

Implementations MUST provide atomicity or equivalent concurrency guarantees for operations where partial success could violate an invariant. This includes, where applicable:
- scoped idempotency-key uniqueness;
- accepted inbound state plus reliable processing dispatch;
- processing claim/reclaim fencing;
- immutable result publication/version creation;
- review optimistic/pessimistic concurrency;
- authorization/configuration changes that affect subsequent execution.

A process-local in-memory store MAY be used for tests, demonstrations or stateless derived caches, but MUST NOT be represented as satisfying durable production guarantees.

## Document payloads

The platform does not require original document binaries to reside in the same durable database. A deployment MAY retain originals in the source system, an object/document store, or another authorized repository. Temporary processing copies MUST follow retention and secure-cleanup policy.

Large model artifacts, OCR models and runtime binaries SHOULD be managed outside transactional application tables.

## Secrets

Credentials and provider secrets MUST NOT be stored as ordinary configuration values. Durable records SHOULD contain opaque secret references resolved through an authorized secret-management boundary.

## Technology neutrality

Relational databases, distributed databases, durable queues, object stores and other persistence technologies MAY be used individually or in combination provided the observable guarantees above are preserved.
