# Specification Governance

**Class:** Normative for repository evolution

## Change classes

- **Editorial**: wording/format clarification with no semantic change.
- **Compatible**: additive behavior/contracts permitted by existing compatibility rules.
- **Breaking**: changes existing normative meaning or invalidates previously conforming behavior.
- **Security correction**: closes a vulnerability/unsafe ambiguity and may require accelerated migration.

## Evidence-driven core evolution

After the v0.9 stabilization candidate, a new normative core concept SHOULD be justified by at least one concrete source of evidence:
- a representative validation scenario that cannot be expressed correctly;
- an independent implementation interoperability failure;
- a security/threat review finding;
- a portability failure across providers/stacks;
- a standards/regulatory requirement applicable to the declared profile.

A single customer's local field/workflow preference is normally a profile/configuration concern, not evidence for expanding core.

## Required change artifacts

Normative changes MUST update affected:
- specification text;
- machine-readable contracts where applicable;
- examples/fixtures;
- conformance tests/vectors;
- compatibility notes.

Architecturally significant decisions SHOULD add or supersede an ADR.

## Deprecation

Deprecated normative behavior MUST identify:
- what is deprecated;
- replacement/migration path;
- affected contract version;
- removal target or condition when known.

Deprecation does not silently change historical interpretation.

## ADR lifecycle

ADR status values:
- Proposed
- Accepted
- Superseded
- Deprecated
- Rejected

A superseded ADR MUST reference its replacement. Historical ADRs remain in the repository.

## Releases

Specification maturity version, individual contract versions, taxonomy versions, model versions and tenant policy versions are independent identifiers.

A release SHOULD publish a manifest identifying the normative contract versions included.

## Security

Security-sensitive changes SHOULD favor fail-safe behavior and explicit migration over preserving unsafe ambiguity.
