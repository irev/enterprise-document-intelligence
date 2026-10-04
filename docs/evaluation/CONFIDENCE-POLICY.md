# Confidence Policy

Confidence must be calibrated on representative data. Do not copy arbitrary thresholds into production.

A deployment profile may map calibrated results to `AUTO_ACCEPT`, `REVIEW_REQUIRED`, `MANUAL_REQUIRED`, or `REJECTED/UNSUPPORTED`.

Maintain confidence at the level decisions occur: classification, individual fields, probabilistic reconciliation and document-quality signals. Do not average unrelated scores into a misleading single number.

High-impact fields such as amounts, beneficiary/bank details and tax identity may require stricter verification independent of general document confidence.

Monitor confidence distributions and review outcomes for drift.