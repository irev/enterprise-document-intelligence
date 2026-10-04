# Provider Adapter Conformance

Any OCR/parser/model provider adapter must satisfy the platform contract rather than redefine it.

## Common tests

- reports stable provider/model/version identity;
- maps timeout/rate-limit/provider failures into platform error categories;
- does not leak provider DTOs into canonical contracts;
- respects cancellation/time budgets;
- emits no secrets or document contents to logs by default;
- preserves tenant/correlation context without using it as model instruction;
- supports deterministic fixtures/mocks for CI.

## OCR/parser

Test page ordering, text/layout coordinate convention, empty/scan-only input, rotation, tables where supported, and malformed input.

## Classifier

Test known classes, UNKNOWN/OOD, score range, class mapping, unsupported output and malformed provider response.

## Extractor

Test missing fields, multiple candidates, raw vs normalized value, evidence mapping, malformed structured output, and high-risk field behavior.

## Managed AI providers

A provider is deployable only when data classification, tenant agreement, region/residency, retention/training terms, authentication, rate limits, and incident controls meet deployment policy.

Passing adapter tests does not imply the model passes business evaluation gates.