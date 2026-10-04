# RFP Validation Report — v0.9

**Validation type:** specification walkthrough against synthetic enterprise RFP/AP scenarios  
**Implementation under test:** none  
**Result:** specification-level validation only

## Summary

Sixteen representative scenarios were mapped against the v0.9 contracts. The core architecture covers the tested happy path and failure modes without requiring stack-specific behavior.

No scenario required moving payment approval/authorization into the Document Intelligence core.

## Findings

### VAL-001 — Business duplicate semantics need one explicit vocabulary

**Severity:** LOW  
**Status:** clarification recommended, not architectural gap

The deduplication document correctly separates exact, near and business duplicates, but a portable result vocabulary for `duplicate candidate` versus `confirmed duplicate` is not yet machine-readable.

Recommendation: add this only when an implementation/API needs to exchange duplicate findings across systems. Until then, stable finding codes are sufficient.

### VAL-002 — Line-item semantic profiles remain domain-specific

**Severity:** INFO  
**Status:** expected extension point

The generic structured-value schema can represent invoice line items, but fields such as tax rate, discount, SKU, GL/account assignment, cost center and withholding treatment vary by profile/domain.

Recommendation: do not move these into core. Define them in invoice/RFP profiles when validated against real requirements.

### VAL-003 — Password acquisition workflow is intentionally outside core

**Severity:** INFO  
**Status:** no change

The core correctly requires an explicit inaccessible/unsupported state. How a password is requested, stored or supplied is an application/security workflow concern.

### VAL-004 — Requirement satisfaction aggregate is semantically useful but not yet canonical

**Severity:** LOW  
**Status:** candidate profile contract

RFP consumers may benefit from a machine-readable aggregate such as SATISFIED / UNSATISFIED / REVIEW_REQUIRED for a requirement profile. Existing findings are sufficient to derive it, so this is not required in core yet.

## Architecture validation

The scenarios support the current separations:

```text
Source bytes
   != logical document
   != document classification
   != extracted observed value
   != authoritative master identity
   != business requirement
   != business authorization
```

They also validate:

```text
Model confidence
   != calibrated reliability
   != operational decision policy
   != payment approval
```

## Decision

v0.9 remains a stabilization candidate. Do not expand the normative core based only on these synthetic scenarios.

Next evidence should come from:
1. representative real/redacted corporate document structures;
2. an independent implementation attempt;
3. security/threat review;
4. interoperability between at least two implementation adapters/providers.

Any resulting specification change should cite the failing scenario/evidence.
