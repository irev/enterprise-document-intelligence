# Reference Implementation Readiness — v0.9

**Class:** Informative assessment  
**Assessment target:** first independent conforming implementation  
**Decision:** READY FOR REFERENCE IMPLEMENTATION

## Purpose

Determine whether the specification is sufficiently complete for an implementation team to build a conforming Document Intelligence service without selecting implementation technology in this repository.

This assessment distinguishes:

- **SPEC BLOCKER** — two reasonable implementations could produce incompatible behavior because a normative requirement is missing or ambiguous.
- **IMPLEMENTATION CHOICE** — technology/internal design may differ without affecting conformance.
- **PROFILE CONFIGURATION** — domain/customer policy belongs outside the universal core.

## Readiness decision

No unresolved architectural blocker prevents starting a reference implementation.

One policy-language ambiguity was discovered during this assessment: language 1.0 previously allowed an unspecified false/error outcome for missing comparison operands. It has been corrected so missing, null, incompatible types, Boolean composition, and evaluation failure have deterministic semantics.

Private enterprise-payment validation also produced four v2 conformance vectors covering authoritative context, requirement readability, cross-document evidence, and configuration snapshots.

## Minimum conforming vertical slice

The first implementation SHOULD prove the following end-to-end path before adding broad provider or workflow scope:

```text
Submit immutable source
        |
        v
Security / source validation
        |
        v
Parse or OCR through adapter
        |
        v
Classify known type or UNKNOWN
        |
        v
Extract profile fields
        |
        v
Normalize + attach evidence
        |
        v
Deterministic validation
        |
        +----> REVIEW_REQUIRED when unsafe to finalize
        |
        v
Immutable completed result version
```

The implementation does not need payment approval, accounting posting, tax authorization, ERP workflow, or customer-specific transaction routing to prove Document Intelligence conformance.

## Required first-slice behaviors

A useful first implementation SHOULD demonstrate:

1. tenant-scoped document identity and authorization boundary;
2. immutable source identity/integrity metadata;
3. explicit processing run/result version;
4. one known document profile plus UNKNOWN/OOD;
5. explicit field states including PRESENT, NOT_PRESENT, ILLEGIBLE and AMBIGUOUS;
6. evidence with page and canonical coordinate semantics for material extracted fields;
7. raw and normalized value preservation;
8. component/model/version provenance;
9. deterministic findings with stable codes and rule version;
10. fail-safe REVIEW_REQUIRED / FAILED / UNSUPPORTED outcomes;
11. reprocessing that creates a new version without rewriting the prior completed result;
12. human correction history if REVIEW capability is claimed;
13. execution of applicable portable conformance vectors and emission of a conformance report.

## Recommended implementation sequence

### RI-0 — Contract adapter

Implement canonical types, schema validation, version identifiers and the conformance-adapter boundary first.

Exit criterion: the implementation can consume abstract conformance inputs and map observable outputs into the conformance vocabulary.

### RI-1 — Deterministic ingestion

Implement source acceptance, integrity calculation, MIME/content checks, tenant boundary and processing identity.

Exit criterion: identical source bytes can be identified without conflating source identity with business/document identity.

### RI-2 — Document understanding adapter

Implement one parser/OCR adapter behind the provider-neutral contract.

Exit criterion: pages/text/layout/evidence coordinates are normalized without leaking provider DTOs into canonical output.

### RI-3 — Classification and extraction

Implement at least one concrete document profile plus UNKNOWN/OOD and explicit field states.

Exit criterion: material fields have evidence; unsupported/ambiguous content is not guessed.

### RI-4 — Normalization and deterministic validation

Implement the normalization registry subset needed by the chosen profile and Restricted Policy Expression Language 1.0.

Exit criterion: policy outcomes are deterministic, typed, versioned and fail explicitly on evaluation errors.

### RI-5 — Versioning and review

Implement immutable completed results, reprocessing, and optionally human-review concurrency.

Exit criterion: prior machine results remain reconstructable after reprocessing or correction.

### RI-6 — Bundle/RFP profile

Only after the document-level slice is stable, add bundles, requirement profiles, authoritative context and cross-document reconciliation.

Exit criterion: observed document values remain distinct from resolved identities and authoritative business values.

## Implementation choices intentionally left open

The implementation is free to choose:
- programming language and framework;
- relational/document/object storage;
- queue or orchestration mechanism;
- OCR/parser/model provider;
- synchronous internal calls versus asynchronous workers;
- deployment topology;
- REST/RPC/message binding unless a claimed capability/profile requires a specific contract;
- internal module/folder/class names.

These choices MUST NOT alter observable normative semantics.

## Profile configuration intentionally left open

The following are not blockers and SHOULD NOT be hard-coded into the platform core:
- customer transaction names;
- mandatory-document matrices;
- tax jurisdiction rules;
- approval thresholds and role names;
- ERP-specific fields;
- chart of accounts;
- bank/payment-channel rules;
- physical-original handling;
- customer-specific confidence thresholds.

## Conformance gate before calling an implementation compatible

An implementation SHOULD NOT be described as conforming merely because it validates JSON schemas.

At minimum:
1. declare specification and supported contract versions;
2. declare claimed capabilities;
3. execute every applicable CORE vector;
4. execute vectors for each claimed optional capability;
5. emit a machine-readable conformance report;
6. have zero FAIL results for mandatory applicable requirements;
7. treat SKIP as unresolved evidence, not PASS;
8. document deviations from SHOULD-level requirements.

## Remaining non-blocking work

The following may be refined from implementation evidence:
- portable duplicate-candidate vocabulary;
- aggregate requirement-satisfaction vocabulary;
- authenticity/signature capability;
- richer domain line-item profiles;
- additional normalization registries;
- performance/SLO profiles;
- adapter-specific interoperability fixtures.

None should delay the first reference implementation.

## Architecture guardrail

The reference implementation is a consumer of this specification, not the source of truth for it.

```text
Specification
     |
     v
Conformance vectors
     |
     v
Reference implementation
     |
     v
Observed implementation evidence
     |
     +----> specification change only when evidence exposes a real contract gap
```

Technology-specific decisions SHOULD live in the implementation repository. Only reusable behavioral/interoperability findings should flow back into this specification repository.
