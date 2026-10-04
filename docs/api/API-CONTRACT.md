# API Contract

This document defines transport-neutral semantics. An implementation may expose REST, messaging, or both.

## Core operations

### Submit document
`POST /v1/documents`

Accept a document plus controlled business context. Return a stable `document_id` and processing status. Submission should support idempotency keys.

### Get document
`GET /v1/documents/{document_id}`

Return metadata and lifecycle status, subject to tenant authorization.

### Get result
`GET /v1/documents/{document_id}/result`

Return the canonical document result when available. A partially processed document must be explicitly marked; never represent partial output as completed validation.

### Submit review
`POST /v1/documents/{document_id}/reviews`

Record a human review action without silently overwriting the original machine result.

## Status vocabulary

`RECEIVED`, `PROCESSING`, `REVIEW_REQUIRED`, `COMPLETED`, `FAILED`, `UNSUPPORTED`.

## Required API properties

- tenant-scoped authorization;
- request/correlation IDs;
- idempotent submission semantics;
- explicit error codes;
- bounded upload limits;
- asynchronous processing support;
- versioned contracts;
- no model-provider details required by consumers.

## Errors

Use stable machine codes, for example:
- `UNSUPPORTED_MEDIA_TYPE`
- `DOCUMENT_TOO_LARGE`
- `ENCRYPTED_DOCUMENT_UNSUPPORTED`
- `MALWARE_DETECTED`
- `PROCESSING_FAILED`
- `DOCUMENT_NOT_FOUND`
- `TENANT_ACCESS_DENIED`
- `REVIEW_CONFLICT`

Do not expose internal prompts, secrets, stack traces, or sensitive extracted content in generic error responses.