# ADR-0010: Conformance Is Behavioral, Not Implementation-Specific

- Status: Accepted
- Date: 2026-10-04

## Context
The specification must be usable by implementations written with different languages, frameworks, persistence technologies and providers.

## Decision
Conformance tests target observable contract semantics. The specification publishes abstract test vectors and report schemas; each implementation supplies an adapter to its interface. Tests MUST NOT require a particular internal architecture.

## Consequences
Implementations can remain idiomatic to their stack while being compared against the same requirements. Some semantic mappings require adapter code, but the specification does not become coupled to a test framework or runtime.
