# Persistence Model

This is a logical model; storage technology is implementation-specific.

## Core aggregates / records

### Document
Stable identity and tenant ownership. References immutable source object/hash and current lifecycle.

### ProcessingRun
One processing attempt/version for a document. Records status, pipeline/component versions, timestamps, correlation ID and failure state. Completed runs are immutable.

### DocumentResult
Canonical result bound to one ProcessingRun.

### Evidence
Source page/span/region references used by extracted fields/findings. Large binary crops should normally be stored by reference, not duplicated in relational rows.

### DocumentBundle
Versioned collection of document processing results associated with one business context/reference.

### Finding
Stable code/severity/source/rule version plus references to documents/fields/evidence.

### Review
Optimistically versioned review session/history containing explicit actions and actor provenance.

### PolicySnapshot
Reference or immutable snapshot/hash of tenant policy/configuration used for an evaluation.

### OutboxEvent
Durable integration event written atomically with relevant state change and later published.

## Important constraints

- Every tenant-owned row/object carries or inherits an enforceable tenant boundary.
- Source document hash is not globally exposed across tenants.
- Completed result versions are immutable.
- Reprocessing creates a new ProcessingRun/result version.
- Business system IDs are references, not the platform's primary identity.
- Use an outbox/inbox or equivalent pattern for reliable state/event integration.
- Avoid distributed transactions across model providers, object storage and business systems.

## Suggested uniqueness

Examples, subject to implementation:
- `(tenant_id, document_id)`;
- `(document_id, processing_version)`;
- `(tenant_id, idempotency_key)` for submission scope;
- `event_id` for inbox/outbox deduplication.