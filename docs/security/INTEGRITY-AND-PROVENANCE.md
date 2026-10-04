# Integrity and Provenance

**Class:** Normative

## Digest semantics

A digest identifies bytes or a declared canonical representation; it does not by itself prove who created the content.

Every material digest MUST identify:
- algorithm;
- digest value;
- scope of bytes/representation hashed.

For structured payloads, a canonicalization method MUST be declared before a digest can be interpreted portably.

## Algorithm agility

The specification MUST NOT hard-code one hash algorithm forever. Profiles/deployments MAY restrict allowed algorithms. Weak/deprecated algorithms MUST NOT be introduced merely for compatibility.

## Source identity

Byte identity, logical document identity and business-document identity are distinct:
- same bytes may have different logical submissions;
- different bytes may represent the same business invoice;
- near-duplicate similarity is not cryptographic identity.

## Signatures

Digital-signature verification is an optional capability/profile. A signature result MUST distinguish cryptographic validity, certificate/trust status, signing time claims and document business validity; these are not equivalent.

## Provenance

Material derived artifacts SHOULD be linkable to their source document/version and producing component/version. Provenance MUST NOT be fabricated when unavailable.
