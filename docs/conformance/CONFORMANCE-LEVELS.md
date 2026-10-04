# Conformance Levels

**Class:** Normative

Conformance uses **capabilities**, not technology tiers.

## CORE

Mandatory for every conforming implementation:
- secure ingestion boundary;
- document lifecycle;
- classification with abstention/UNKNOWN semantics;
- extraction/result representation;
- evidence/provenance;
- explicit validation/findings;
- versioned immutable completed results;
- tenant/security boundaries.

## REVIEW

Claimed when human review is supported:
- review actions;
- immutable correction history;
- optimistic conflict detection or equivalent lost-update protection;
- actor/result-version provenance.

## BUNDLE

Claimed when multi-document processing is supported:
- versioned document bundles;
- cross-document findings;
- explicit authoritative business-context boundary.

## POLICY

Claimed when configurable deterministic policies are supported:
- versioned rule/policy identity;
- restricted declarative policy semantics;
- deterministic evaluation;
- audit provenance.

## EVENTS

Claimed when lifecycle events are exposed:
- versioned event envelope;
- stable event identity;
- duplicate-delivery-safe semantics expected from consumers where at-least-once delivery applies.

## DATASET

Claimed when dataset/annotation lifecycle is implemented:
- governed eligibility;
- annotation provenance;
- split/leakage controls;
- separation of production data from training eligibility.

An implementation MAY claim any applicable optional capability in addition to CORE. Profiles MAY require specific capabilities.
