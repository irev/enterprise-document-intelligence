# Error Taxonomy

Errors are stable machine contracts. Human messages may change/localize.

## Categories

### Request / input
- `INVALID_REQUEST`
- `UNSUPPORTED_MEDIA_TYPE`
- `DOCUMENT_TOO_LARGE`
- `PAGE_LIMIT_EXCEEDED`
- `ENCRYPTED_DOCUMENT_UNSUPPORTED`
- `DOCUMENT_CORRUPT`

### Security / authorization
- `AUTHENTICATION_REQUIRED`
- `TENANT_ACCESS_DENIED`
- `MALWARE_DETECTED`
- `CONTENT_POLICY_REJECTED`

### Processing
- `PARSER_FAILED`
- `OCR_FAILED`
- `CLASSIFICATION_FAILED`
- `EXTRACTION_FAILED`
- `VALIDATION_FAILED`
- `PROCESSING_TIMEOUT`
- `PROCESSING_FAILED`

### Resource / state
- `DOCUMENT_NOT_FOUND`
- `RESULT_NOT_READY`
- `REVIEW_CONFLICT`
- `IDEMPOTENCY_CONFLICT`
- `UNSUPPORTED_DOCUMENT`

## Error representation

Prefer RFC 9457-style Problem Details with an additional stable `code` and `correlation_id`.

Do not expose stack traces, prompts, credentials, internal storage paths, or sensitive extracted values in generic error bodies.

## Retryability

Retryability is explicit per error/category in implementation policy. Authentication, validation, malware and unsupported-document failures are not fixed by blind retries. Transient infrastructure failures may be retryable with bounded exponential backoff and jitter.