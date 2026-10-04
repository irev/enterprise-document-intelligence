# Adapter Contracts

Implementations isolate replaceable technology behind explicit adapters.

## Parser/OCR adapter

Input: immutable document reference + processing options.

Output: pages, text spans, layout/table structures, quality signals, engine/version metadata.

Must not classify business meaning.

## Classifier adapter

Input: bounded document representation.

Output: family/type/subtype candidate(s), calibrated score(s), UNKNOWN/OOD signal, model/version provenance.

Must not authorize business actions.

## Extractor adapter

Input: document representation + versioned document profile.

Output: typed field candidates with raw/normalized values, confidence and evidence.

Must not silently populate missing values from unrelated master data.

## Validation adapter/engine

Input: canonical extracted result + explicit related documents/context.

Output: stable findings with codes/severity/rule version.

Deterministic business rules should be distinguishable from probabilistic checks.

## Storage adapter

Stores source references, processing versions, results and audit records while preserving tenant boundaries and retention policy.

## Event publisher

Publishes versioned lifecycle events. Consumers assume at-least-once delivery unless stronger guarantees are explicitly configured.

## Rule

Provider-specific DTOs must terminate at adapter boundaries; they must not become the canonical API contract.