# Versioning and Compatibility

**Class:** Normative

## Independent version domains

The specification, canonical schemas, taxonomy, profiles, API, events, policy language, models, and tenant configurations MAY evolve independently. Their versions MUST NOT be conflated.

## Compatibility

A change is **breaking** when a previously conforming consumer/implementation using the declared contract can no longer process valid behavior without change.

Examples include:
- removing/renaming a required field;
- changing field meaning/type;
- making an optional field required without a compatible version boundary;
- removing an enum value that may already be emitted;
- changing state/event semantics;
- changing normalization semantics that alter material interpretation.

Typically non-breaking changes include documentation clarification and additive optional fields where consumers are explicitly required to tolerate them.

## Consumer robustness

Contracts MUST define whether unknown fields and unknown enum values are tolerated. Do not assume one global rule for every interface.

## Historical interpretation

Stored results/events/policies MUST retain enough version identity to be interpreted according to the contract that produced them.

## Migration

Breaking normative contract changes MUST:
- introduce an explicit new contract version;
- document migration/compatibility impact;
- update examples and conformance tests;
- avoid silently reinterpreting historical data.

## Specification maturity

Repository milestone labels such as v0.x describe specification maturity and MUST NOT be confused with individual schema/API/model versions.
