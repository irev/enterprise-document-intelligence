# Document Classification

**Class:** Normative for classification capability.

## Scope

Classification assigns a generic document type to a SourceObservation-derived understanding result. Business domain/process context is a separate dimension and MUST NOT be encoded into customer-specific document classes.

## UNKNOWN and abstention

A conforming classifier MUST support `UNKNOWN` or an equivalent explicit abstention state.

An implementation MUST NOT force a known class when available evidence is insufficient or materially ambiguous. Acceptance thresholds, ambiguity margins and calibration policy are configuration/versioned decision inputs, not universal platform constants.

Raw model confidence MUST NOT be represented as calibrated probability unless calibration evidence supports that interpretation.

## Provenance

A classification result MUST retain sufficient provenance to identify the classifier/model version and taxonomy version used. Accepted evidence references MUST remain resolvable to the exact source observation/understanding result.

## Safety boundary

Classification is a prediction. It MUST NOT itself authorize payment, approval, workflow privilege, external transmission or another business action.

Document content is untrusted classifier input and MUST NOT be interpreted as system policy, tenant identity, tool authorization or provider-routing instruction.
