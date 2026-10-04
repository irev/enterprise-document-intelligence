# Normalization Registry

**Class:** Normative

Normalization converts observed document values into comparable canonical values without destroying source representation.

## General rules

- Raw/source values MUST remain available when a normalized material value is stored.
- Normalization MUST be identified by a stable rule identifier and version where interpretation may change.
- Normalization MUST NOT invent missing information.
- Locale assumptions MUST be explicit or derived from declared context/evidence; ambiguous values MUST NOT be silently coerced.
- Unicode text SHOULD be normalized consistently using a declared Unicode normalization form.

## Initial registry

| ID | Input concept | Canonical output |
|---|---|---|
| `text.trim.v1` | text | surrounding whitespace removed; internal content preserved |
| `identifier.basic.v1` | identifier | trimmed representation; case/separator changes only when profile explicitly permits |
| `date.iso8601.v1` | date-only | `YYYY-MM-DD`; no timezone invented |
| `datetime.rfc3339.v1` | instant/offset datetime | RFC 3339 representation preserving/normalizing offset semantics |
| `decimal.v1` | decimal number | decimal value, not binary floating-point semantics |
| `currency.iso4217.v1` | currency code/name/symbol with sufficient context | ISO 4217 alpha code |
| `unicode.nfc.v1` | Unicode text | NFC-normalized text |
| `organization.display.v1` | organization display name | conservative display normalization; not entity resolution |

## Locale-sensitive numbers

Strings such as `1.234,56` and `1,234.56` are ambiguous without locale/context. An implementation MUST preserve raw text and MUST use explicit locale/profile evidence before producing a normalized decimal when ambiguity cannot otherwise be resolved.

## Identifiers

Tax IDs, invoice numbers, PO numbers, account numbers and similar identifiers are not generic numbers. Leading zeros and meaningful punctuation MUST NOT be discarded unless the applicable profile explicitly defines that normalization.

## Extensibility

New normalization rules use stable namespaced IDs and versioned semantics. Changing semantics requires a new rule version.
