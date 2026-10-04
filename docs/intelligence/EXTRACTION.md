# Information Extraction

**Class:** Normative for extraction capability.

## Field semantics

Extraction results MUST distinguish field state, observed/raw representation, normalized/typed value, confidence and evidence.

A conforming implementation MUST NOT represent all non-values as a single null-like state. At minimum it MUST distinguish a supported present value from a missing value; implementations SHOULD also distinguish explicit source null/not-applicable and invalid observed content.

## Evidence

A field asserted as present MUST have source-bound evidence sufficient to trace the claim to the understanding result. A missing field MUST NOT carry a fabricated source or normalized value.

Evidence validation establishes traceability only. It does not make the extracted value authoritative or business-valid.

## Raw and normalized values

Normalization MUST NOT destroy the raw observed representation when a value is present. Typed/normalized values MUST identify or inherit a versioned normalization contract sufficient for reproducibility.

## Provenance

Extraction results MUST retain extractor/model identity and version plus extraction schema/profile version sufficient to reconstruct the processing decision.

## Safety boundary

Extraction is a machine claim, not authorization. Document content MUST NOT alter tenant identity, authorization, extraction schema selection, provider permission or business rules.

Confidence MUST NOT be presented as calibrated probability unless calibration evidence supports that interpretation.
