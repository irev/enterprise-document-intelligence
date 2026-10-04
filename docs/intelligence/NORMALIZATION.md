# Deterministic Normalization

**Class:** Normative for normalization capability.

## Contract

Normalization converts an observed/raw field representation into a canonical typed value. The raw representation and its evidence MUST remain available.

A normalization rule MUST have stable identity and version sufficient to reproduce the conversion contract used by a completed result.

## Determinism and ambiguity

For the same input and same versioned normalization contract, normalization MUST produce the same result or the same stable failure category.

A normalizer MUST NOT silently guess materially ambiguous locale, date order, currency or identifier semantics. Ambiguity MUST be resolved by explicit profile/context, additional evidence, or a non-success/review outcome.

## Numeric safety

Financial decimal values MUST use a representation that preserves required decimal semantics. Implementations MUST NOT rely on binary floating-point where that can change the represented monetary value.

## Failure

Normalization failure MUST preserve the observed source value/evidence and MUST NOT fabricate a replacement canonical value.

## Separation

Normalization establishes canonical representation, not authenticity, authority or business validity. Business validation is a separate deterministic policy layer.
