# Evaluation Protocol

## Classification
Per-class precision/recall/F1, macro-F1, confusion matrix, UNKNOWN/OOD performance, and calibration when confidence controls automation. Overall accuracy alone is insufficient.

## Extraction
Per-field exact/normalized exact match and precision/recall/F1. Numeric/date tolerance is allowed only when semantically justified and documented. OCR CER/WER does not substitute for end-to-end extraction metrics.

## Operational
Track STP rate, manual-review rate, false-accept rate, false-reject/review rate, latency percentiles, review time, failures/retries, and cost/document where applicable.

Financial workflows should weight false automatic acceptance more heavily than unnecessary review. Releases record dataset/test version, taxonomy/schema, model, thresholds, segment metrics, regressions and limitations.