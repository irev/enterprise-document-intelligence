# Portable Conformance Harness Protocol

**Class:** Normative

The specification publishes technology-neutral test vectors. An implementation supplies an adapter/runner that executes those vectors against its public or test interface.

## Roles

**Specification vector** describes:
- capability;
- requirement references;
- preconditions;
- abstract input;
- expected semantic outcome;
- comparison mode.

**Implementation adapter** maps abstract input to the implementation and maps observed output back to the vector vocabulary.

**Conformance runner** executes vectors and emits a conformance report.

## Comparison modes

- `EXACT`: values must match exactly.
- `SUBSET`: required expected members must be present; additional permitted output is ignored.
- `SEMANTIC`: implementation-specific representation is mapped to the same defined semantic outcome.
- `PREDICATE`: a named assertion from the vector contract is evaluated by the runner.

A vector MUST NOT require knowledge of the implementation's database, framework, internal classes, queue or model provider.

## Result statuses

- `PASS`: applicable requirement satisfied.
- `FAIL`: applicable requirement violated.
- `SKIP`: test could not execute; does not count as passing.
- `NOT_APPLICABLE`: capability/profile legitimately not claimed.

CORE vectors MUST NOT be marked NOT_APPLICABLE by an implementation claiming core conformance.

## Reproducibility

Reports MUST identify specification version, implementation/version and declared capabilities. Test fixtures containing sensitive documents MUST follow dataset governance and MUST NOT be embedded in public reports by default.

Machine contracts:
- `schemas/conformance/test-vector.schema.json`
- `schemas/conformance/report.schema.json`
