# Specification Governance

**Class:** Normative for repository evolution

## Change classes

- **Editorial**: wording/format clarification with no semantic change.
- **Compatible**: additive behavior/contracts permitted by existing compatibility rules.
- **Breaking**: changes existing normative meaning or invalidates previously conforming behavior.
- **Security correction**: closes a vulnerability/unsafe ambiguity and may require accelerated migration.

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
