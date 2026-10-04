# Human Review

Review is triggered by calibrated uncertainty, UNKNOWN/OOD, poor quality, conflicting evidence, high-risk fields, or deterministic policy.

Reviewer UI should expose the original page, highlighted evidence, raw/normalized values, confidence, findings, related-document evidence, and diagnostic versions where appropriate.

Prefer explicit actions: `CONFIRM`, `CORRECT`, `MARK_NOT_PRESENT`, `MARK_ILLEGIBLE`, `RECLASSIFY`, `ESCALATE`.

Never silently overwrite machine results. Preserve prediction, correction, actor, timestamp and reason where required.

Learning loop: human correction -> governed candidate -> quality review -> approved dataset -> future release. There is no direct correction-to-training shortcut.