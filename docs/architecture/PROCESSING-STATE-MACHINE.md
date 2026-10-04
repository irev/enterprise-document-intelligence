# Processing State Machine

## External states

```text
RECEIVED
   |
   v
PROCESSING ----------------------> FAILED
   |                                ^
   +----------> UNSUPPORTED         |
   |                                |
   +----------> REVIEW_REQUIRED ----+
   |                 |
   |                 v
   |             PROCESSING
   |                 |
   v                 v
COMPLETED <-----------+
```

## Semantics

- `RECEIVED`: accepted and assigned stable identity; processing has not completed.
- `PROCESSING`: one or more pipeline stages are executing/retrying.
- `REVIEW_REQUIRED`: automated processing cannot safely finalize without authorized human input.
- `COMPLETED`: pipeline completed and canonical result is finalized for this processing version. This does **not** mean a business payment/request is approved.
- `FAILED`: technical or integrity failure prevents completion.
- `UNSUPPORTED`: input is validly received but outside supported capability/policy.

## Internal stages

Implementations may track `INGESTION`, `PARSING`, `OCR`, `CLASSIFICATION`, `EXTRACTION`, `VALIDATION`, `REVIEW`, `FINALIZATION`, but these must not leak into external contracts without versioning.

## Rules

- State transitions are auditable.
- Retry must be idempotent where side effects exist.
- A completed processing version is immutable; reprocessing creates a new processing/version record.
- Review actions use optimistic concurrency/version checks to avoid lost corrections.
- Partial output never masquerades as `COMPLETED`.