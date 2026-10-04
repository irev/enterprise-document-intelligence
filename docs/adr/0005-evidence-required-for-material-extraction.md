# ADR-0005: Evidence Is Required for Material Extraction

- Status: Accepted
- Date: 2026-10-04

## Context
A normalized value without provenance is difficult to review, debug or audit and makes hallucinated extraction harder to detect.

## Decision
Material extracted fields support source evidence such as page, text span and/or layout region. High-impact fields should not qualify for automatic acceptance when required evidence cannot be established.

## Consequences
Storage and extraction contracts are richer, but human review, evaluation, auditability and model replacement become substantially safer.