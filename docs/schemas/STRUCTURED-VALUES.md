# Structured Values and Tables

**Class:** Normative

Structured document data MUST preserve semantic structure without coupling consumers to an OCR/provider table format.

## Core reusable values

The specification defines reusable semantics for:
- money;
- identifiers;
- addresses;
- parties;
- quantities;
- line items;
- generic tables.

## Money

Money MUST carry amount and currency together when currency is known. Implementations MUST NOT infer currency from a bare symbol when context is ambiguous.

## Identifiers

Identifiers are strings even when composed only of digits. Leading zeros MUST be preserved unless a profile explicitly defines normalization.

## Parties

A document-observed party is not automatically an authoritative master-data identity. Entity resolution remains governed by the entity-resolution contract.

## Line items

Line items SHOULD use semantic fields when recognized. Provider-specific OCR cells MAY be retained as provenance but MUST NOT replace canonical semantic values.

## Tables

Generic tables use zero-based logical row/column indexes. Cell evidence SHOULD reference source evidence. Row/column spans describe logical structure, not pixel geometry.

A profile MAY define a domain-specific semantic projection of a table. It MUST preserve enough provenance to trace material values back to source evidence.

Machine contract: `schemas/structured/document-values-v2.schema.json`.
