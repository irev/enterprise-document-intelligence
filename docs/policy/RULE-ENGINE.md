# Rule Engine and Policy Contract

## Purpose

The rule engine evaluates deterministic document, bundle and business-requirement policies. It is deliberately separate from probabilistic model inference.

## Safety requirement

Rules are **data**, not executable source code. Never evaluate tenant-provided JavaScript, Python, SQL, C#, shell, template expressions, or arbitrary reflection.

Use a small typed allow-listed AST/operator set such as:
- boolean: `and`, `or`, `not`;
- presence: `present`, `all_present`;
- comparison: `equals`, `normalized_equals`, `lt/lte/gt/gte`;
- membership: `in`;
- controlled date/decimal operations.

Every operator has deterministic type/error semantics.

## Inputs

Rules consume explicitly named sources:
- canonical document fields;
- document/bundle metadata;
- authoritative business context;
- approved master-data lookups exposed through controlled interfaces.

A model prediction must never be silently promoted to authoritative business context.

## Output

A rule emits a stable finding code, severity, ruleset/rule version and evidence/input references sufficient for audit.

## Governance

Rule changes require versioning, tests, effective-date/deployment control, and tenant authorization. Historical evaluations retain the exact ruleset version used.

See `schemas/policies/rule-set.schema.json`.