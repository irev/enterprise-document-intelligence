# ADR-0004: Asynchronous Processing Is the Default Contract

- Status: Accepted
- Date: 2026-10-04

## Context
OCR, layout analysis, model inference, validation and human review have variable latency and may require retries.

## Decision
Document submission returns a stable document identity and processing status. Completion is observed through status/result APIs and/or versioned events. Implementations may provide synchronous fast paths later without changing the canonical lifecycle.

## Consequences
The platform handles long-running processing and backpressure cleanly, but requires durable state, idempotency and event/status semantics.