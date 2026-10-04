# Specification Gap Analysis — v0.6

## Purpose

Audit the repository as a technology-neutral specification rather than an implementation blueprint.

## Corrected now

1. **Normative ambiguity** — added BCP 14 requirement language and a normative/informative map.
2. **Conformance definition missing** — added CORE and optional capability conformance.
3. **Compatibility/versioning missing** — separated specification maturity from API/schema/model/policy versions.
4. **Extension semantics missing** — added safe namespaced extension rules.
5. **Implementation guidance risk** — explicitly classified persistence/reference deployment/module guidance as informative.

## High-priority remaining gaps

### G1 — Policy AST is underspecified — ADDRESSED IN v0.7
Current rule schema accepts generic objects for `when` and `assert`. This validates shape poorly and cannot guarantee portable deterministic semantics.

Required next: define typed operator AST, operand/value types, missing/null/error semantics, and conformance fixtures.

### G2 — Canonical field model lacks explicit field state — ADDRESSED IN v0.7
The canonical field currently requires raw/normalized/confidence/evidence even when a field is missing/illegible/ambiguous, while annotation schema already has states.

Required next: align production field-result states such as PRESENT / NOT_PRESENT / ILLEGIBLE / AMBIGUOUS / NOT_APPLICABLE without forcing fake values/confidence.

### G3 — Evidence coordinate system is undefined — ADDRESSED IN v0.7
A four-number bounding box is present but units/origin/rotation/page-coordinate semantics are not normative.

Required next: define normalized coordinate convention or explicit coordinate-space metadata.

### G4 — Nested structured fields are weak — PARTIALLY ADDRESSED IN v0.7
Invoice line items, parties, addresses, bank/tax identity and table cells are typed only as generic array/object in profiles.

Required next: reusable structured-value schemas and evidence semantics for nested/table values.

### G5 — Identity/entity resolution boundary needs specification — ADDRESSED IN v0.7
Extracted vendor text and authoritative vendor/master identity are different concepts.

Required next: candidate identity, resolved identity, resolver provenance, match confidence and authoritative-source boundary.

### G6 — API capability is incomplete
OpenAPI covers individual document submission/result/review but not bundle lifecycle, requirement evaluation, reprocessing/version selection, or richer review concurrency.

Required next: extend only as optional capability contracts, not mandatory REST architecture.

### G7 — Event compatibility semantics need strengthening — ADDRESSED IN v0.8
Event schema exists, but evolution rules, ordering scope, replay, deduplication window/identity, and payload minimization need explicit normative semantics.

### G8 — Privacy/legal governance is generic — ADDRESSED AT CORE-HOOK LEVEL IN v0.8
Data classification exists but consent/legal basis, residency, subject rights, retention holds and tenant-specific regulatory obligations cannot be universalized.

Required next: define hooks/metadata obligations and leave legal policy to deployment profiles.

### G9 — Cryptographic/integrity semantics are incomplete — ADDRESSED IN v0.8
SHA-256 is used, but source identity vs integrity, algorithm agility, evidence artifact integrity and signed provenance are not specified.

Required next: hash descriptor structure and algorithm/version semantics; signatures remain optional profile capability.

### G10 — Document/container edge cases — ADDRESSED IN v0.8
Need normative behavior/profile hooks for multi-document PDFs, attachments, password-protected files, digitally signed PDFs, office macros, archives, page splitting/merging, and document segmentation.

### G11 — Localization and normalization registry — ADDRESSED IN v0.8
Currency/date exist conceptually, but locale-dependent numbers, identifiers, Unicode normalization, language/script and timezone/date-only semantics need a registry.

### G12 — Quality and confidence contracts are too open — PARTIALLY ADDRESSED IN v0.8
`quality` and provenance are generic objects; confidence calibration is documented but machine-readable calibration/decision-policy identity is absent.

### G13 — Conformance tests are inventory, not executable — PARTIALLY ADDRESSED IN v0.7
Current CI validates schema syntax/examples but does not test implementation behavior.

Required next: technology-neutral test vectors with request/input + expected semantic outcome; implementations provide their own runner/adaptor.

### G14 — Specification governance is incomplete — ADDRESSED IN v0.8
Need contribution/change process, deprecation lifecycle, release process, contract registry and ADR supersession rules.

## Lower-priority / profile-specific gaps

- electronic/digital signature verification;
- handwriting-specific quality/evaluation;
- multilingual benchmark profiles;
- table reconstruction benchmark;
- jurisdiction-specific tax validation;
- industry-specific retention;
- model cost/carbon reporting;
- UI accessibility requirements for reviewer applications.

These SHOULD remain optional profiles unless the core interoperability contract genuinely requires them.


## v0.7 audit update

v0.7 introduced restricted policy expression schemas, canonical result v2 with explicit field states and evidence coordinates, common structured values, an entity-resolution contract, and initial technology-neutral conformance vectors.

Remaining priority after v0.7: API/event capability completion, privacy/integrity/container edge-case contracts, normalization registry, quality/calibration contracts, richer executable semantic vectors, and specification governance.


## v0.8 audit update

v0.8 added normalization semantics, machine-readable quality and confidence-decision contracts, algorithm-agile integrity semantics, source/container/segment distinctions, event evolution/delivery rules, privacy/regulatory control hooks, specification governance, and additional conformance vectors.

Highest-priority remaining gaps after v0.8:
- G4 richer nested/table structures remain partial;
- G6 optional REST/API capability is incomplete for bundles, reprocessing/version selection and review concurrency;
- G12 calibration/quality semantics need deeper test vectors and registry discipline;
- G13 conformance vectors remain data fixtures rather than a portable executable harness protocol.
