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

## Evaluation outcomes

Language 1.0 has two expression outcomes plus an evaluation failure:

- `TRUE`
- `FALSE`
- `EVALUATION_ERROR` — the expression could not be evaluated according to the language contract.

`EVALUATION_ERROR` is not a Boolean value and MUST NOT be coerced to `TRUE`.

For a rule:
- if `when` evaluates `FALSE`, the rule is not applicable and its assertion is not evaluated;
- if `when` evaluates `TRUE`, `assert` is evaluated;
- if `assert` evaluates `FALSE`, the configured finding is emitted;
- if either evaluated expression produces `EVALUATION_ERROR`, the rule evaluation MUST fail explicitly and MUST NOT be reported as a passed rule.

A deployment MAY map an evaluation error to a review/failure workflow, but it MUST preserve that the policy evaluation itself did not succeed.

## Missing and null semantics

A missing path is distinct from a present path whose value is null.

- `present(path)` is `TRUE` only when the path exists and has an applicable value according to the evaluation context.
- `missing(path)` is the logical complement of `present(path)` for the same evaluation context.
- a comparison operator whose required operand path is missing evaluates `FALSE`; it is not an evaluation error;
- an explicit null literal or present null value participates only in operators whose operand contract permits null;
- ordered comparisons `lt`, `lte`, `gt`, and `gte` with null are type-invalid and produce `EVALUATION_ERROR`.

## Type semantics

Implementations MUST NOT silently coerce arbitrary strings into numbers, dates, booleans, identifiers, or other semantic types.

- `equals` compares values only under their declared/evaluation-context types.
- `normalized_equals` MAY compare normalized representations only when the applicable profile identifies the normalization semantics.
- ordered comparisons require compatible ordered types.
- `in` uses the same equality/type rules as `equals` for each candidate member.
- incompatible operand types produce `EVALUATION_ERROR`.

If a profile requires decimal, date, currency, identifier, or other domain-aware comparison, normalization/type identity MUST be established before policy evaluation according to the applicable versioned contract.

## Boolean composition and errors

Boolean operators use fail-safe error propagation:

- `not(EVALUATION_ERROR)` → `EVALUATION_ERROR`;
- `and` returns `FALSE` if any evaluated argument is `FALSE`; otherwise it returns `EVALUATION_ERROR` if any argument errors; otherwise `TRUE`;
- `or` returns `TRUE` if any evaluated argument is `TRUE`; otherwise it returns `EVALUATION_ERROR` if any argument errors; otherwise `FALSE`.

Implementations MAY short-circuit once the outcome is determined, but short-circuiting MUST NOT change the semantic result.

## Security

Path resolution MUST be allow-listed to the evaluation context. Operators MUST NOT invoke network, filesystem, database query text, reflection, dynamic code, model calls, or environment access.

Machine contract: `schemas/policies/expression.schema.json`.
