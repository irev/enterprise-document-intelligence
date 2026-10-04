# Calibration and Decision Policy

**Class:** Normative

A model score and an operational decision are different concepts.

## Requirements

- Confidence values MUST identify the model/component version that produced them through result provenance.
- A threshold used for automatic acceptance/review MUST belong to a versioned decision policy.
- Thresholds MUST NOT be presented as universally valid defaults merely because they appear in an example.
- High-risk fields SHOULD use evaluation/calibration evidence appropriate to their risk and deployment domain.
- Changing thresholds MUST NOT rewrite historical decision provenance.
- When confidence is not meaningfully comparable across models/releases, consumers MUST NOT assume equal numeric scores imply equal reliability.

## Calibration

Where calibration is claimed, the evaluation record SHOULD identify calibration dataset/version, method, metrics and applicable population/segment.

## Decision bands

The machine-readable decision-policy schema represents operational bands such as AUTO_ACCEPT, REVIEW, MANUAL_REQUIRED and ABSTAIN. Implementations MAY use different labels internally if externally mapped semantics remain clear.
