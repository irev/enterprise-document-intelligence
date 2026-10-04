# Event Contract

Events decouple long-running document processing from business applications.

## Envelope

Every event carries `event_id`, `event_type`, `event_version`, `occurred_at`, `tenant_id`, `document_id`, `correlation_id`, optional `causation_id`, and typed `data`.

See `schemas/events/document-events.schema.json`.

## Baseline lifecycle

```text
document.received
 -> document.processing_started
 -> document.classified
 -> document.extracted
 -> document.validated
 -> [document.review_requested -> document.review_completed]
 -> document.completed

Any stage may emit document.processing_failed.
```

## Delivery semantics

Assume at-least-once delivery unless an implementation explicitly guarantees otherwise. Consumers must be idempotent by `event_id`. Ordering must not be inferred across unrelated documents. Use document/correlation identity to reconstruct one processing flow.

Events contain references and minimal necessary data; avoid broadcasting full sensitive document content.