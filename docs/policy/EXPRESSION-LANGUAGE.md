# Restricted Policy Expression Language 1.0

**Class:** Normative

The policy language is a small typed declarative expression tree. It is intentionally not a general-purpose programming language.

## Operands

- `path`: resolves a value from an explicitly allowed evaluation context.
- `literal`: scalar string, number, boolean or null.

Paths are logical contract paths, not SQL/JSONPath/shell expressions.

## Operators

Boolean:
- `and`
- `or`
- `not`

Presence:
- `present`
- `missing`
- `all_present`
- `any_present`

Comparison:
- `equals`
- `normalized_equals`
- `lt`, `lte`, `gt`, `gte`
- `in`

## Missing/null semantics

A missing path is distinct from a present path whose value is null.

- `present(path)` is true only when the path exists and has an applicable value according to the evaluation context.
- comparison against a missing path does not evaluate true; implementations MUST produce the same deterministic false/error outcome defined by their claimed language version.
- type-invalid comparisons MUST NOT coerce arbitrary strings into numbers/dates silently.

A future language revision MUST define any new coercion/operator semantics explicitly.

## Security

Path resolution MUST be allow-listed to the evaluation context. Operators MUST NOT invoke network, filesystem, database query text, reflection, dynamic code, model calls, or environment access.

Machine contract: `schemas/policies/expression.schema.json`.
