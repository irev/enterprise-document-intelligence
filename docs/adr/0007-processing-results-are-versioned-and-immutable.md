# ADR-0007: Completed Processing Results Are Versioned and Immutable

- Status: Accepted
- Date: 2026-10-04

## Context
Models, prompts, OCR engines, rules and human corrections change over time. Updating an old result in place destroys auditability.

## Decision
Each processing attempt has an explicit version/run identity. Completed machine results are immutable. Reprocessing creates a new run/result. Human review is recorded as separate provenance linked to the result version.

## Consequences
Storage grows and consumers must identify which result version they use, but historical decisions remain reproducible and model upgrades do not rewrite history.