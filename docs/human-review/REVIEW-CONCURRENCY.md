# Review Concurrency Contract

## Problem

Two reviewers or a reviewer and automated reprocessing can otherwise overwrite each other's work.

## Contract

A review target exposes a monotonically increasing `review_version` (or equivalent ETag). Review submissions include the version observed by the reviewer.

If the current version differs, reject the mutation with `REVIEW_CONFLICT` and return enough non-sensitive metadata for the client to reload.

## Immutable history

Do not update the original model prediction in place. Record:
- machine result/version;
- review action;
- previous value/state;
- corrected value/state;
- actor identity;
- timestamp;
- reason/comment where required;
- resulting review version.

## Reprocessing

A new ProcessingRun does not silently invalidate a completed review. The system must explicitly relate a review to the processing/result version it reviewed.

## Dual control

Where policy requires maker-checker/four-eyes approval, model it as deterministic workflow authorization outside the extraction model.