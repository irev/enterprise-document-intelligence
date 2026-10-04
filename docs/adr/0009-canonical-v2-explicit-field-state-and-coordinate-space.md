# ADR-0009: Canonical v2 Adds Explicit Field State and Coordinate Space

- Status: Accepted
- Date: 2026-10-04

## Context
Canonical v1 requires value/confidence/evidence for every field and does not define bounding-box coordinates. That is ambiguous for missing, illegible and uncertain fields and harms interoperability.

## Decision
Introduce canonical result schema v2 rather than silently changing v1. v2 adds explicit field states and a normalized top-left XYXY evidence coordinate convention. Source integrity also becomes an algorithm+digest descriptor rather than a SHA-256-shaped field.

## Consequences
Implementations may continue supporting v1, but v2 consumers gain portable missing/ambiguity semantics and evidence geometry. Migration is explicit and historical v1 payloads retain their original interpretation.
