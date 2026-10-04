# Extension Model

**Class:** Normative

## Goal

Allow organizations and domain profiles to extend the specification without forking or weakening the core.

## Rules

An extension:
- MUST have an unambiguous owner/namespace;
- MUST NOT redefine the meaning of a core field, state, finding severity, or document type;
- MUST NOT weaken core security, audit, evidence, tenant, or decision-boundary requirements;
- MUST be ignorable when the surrounding contract declares extensions optional;
- MUST declare whether it affects interoperability or only local processing;
- SHOULD use namespaced identifiers for custom finding codes, fields, document subtypes, or metadata where collision is possible.

## Taxonomy

A tenant MAY introduce custom subtypes or metadata through an extension/profile. It SHOULD reuse a core type when semantics match. It MUST NOT create a new core-looking type solely to encode a business requirement.

## Canonical data

Vendor/provider-specific response payloads MUST remain outside canonical fields unless normalized into defined core or namespaced extension semantics.

## Policy

Custom policy operators require explicit semantics, types, error behavior, versioning and conformance tests. Arbitrary executable code is not an extension mechanism.

## Portability

A consumer that does not understand an optional extension SHOULD still be able to process the core portion when the contract permits unknown extensions.
