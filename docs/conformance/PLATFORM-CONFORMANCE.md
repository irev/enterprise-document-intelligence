# Platform Conformance

**Class:** Normative

## Conformance statement

An implementation claiming conformance MUST declare:
- specification version;
- supported capabilities/profiles;
- supported canonical schema versions;
- supported API/event contract versions where implemented;
- known optional capabilities not implemented.

Conformance MUST be based on externally observable behavior and contract validation. It MUST NOT require a particular language, framework, database, cloud, OCR engine, model, or vendor.

## Core requirements

A conforming implementation:

1. MUST preserve tenant isolation for all tenant-owned data and operations.
2. MUST treat document content as untrusted input and MUST NOT treat embedded document text as control instructions.
3. MUST preserve UNKNOWN/OOD or an equivalent abstention outcome rather than force unsupported content into a known class.
4. MUST keep AI/model prediction separate from privileged business authorization.
5. MUST preserve evidence/provenance for material extracted predictions according to the applicable profile.
6. MUST preserve original machine results when human corrections are recorded.
7. MUST version completed processing results and MUST NOT silently rewrite historical completed results.
8. MUST expose explicit non-success states for unsupported, failed, incomplete, or review-required processing.
9. MUST version policy/configuration used for material validation or business-requirement evaluation.
10. MUST NOT execute arbitrary tenant-provided code as policy.
11. MUST protect sensitive data in logs/errors and enforce authorization at resource boundaries.
12. MUST maintain sufficient provenance to reconstruct which processing/model/rule/configuration versions produced a material result.

## Capability conformance

Optional capabilities are tested only when claimed, for example:
- REST API;
- lifecycle events;
- human review;
- bundle/cross-document validation;
- dataset/annotation tooling;
- external managed-model integration.

Claiming an optional capability makes its applicable normative contract mandatory.

## Non-conformance examples

An implementation is non-conforming if it:
- forces every input into a known document class;
- overwrites an extracted value with a reviewer correction without preserving history;
- allows a model to approve/execute a payment merely from model output;
- uses customer-provided executable scripts as unrestricted policy;
- returns another tenant's document existence/data;
- claims a contract version while emitting payloads that violate that version.

## Conformance evidence

A conformance report SHOULD contain machine-readable test results, specification revision/version, declared capabilities, implementation identifier/version, and deviations for SHOULD-level requirements.
