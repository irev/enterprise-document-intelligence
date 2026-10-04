# ADR-0002: Separate Canonical, Dataset, and Prompt Contracts

- Status: Accepted
- Date: 2026-10-04

## Context
Production document representation, training annotations and model-specific serialization serve different purposes. Coupling them makes model/provider changes expensive and can cause metadata to be mistaken for actual training signal.

## Decision
Maintain separate versioned contracts for:
1. canonical production document/result;
2. dataset annotation/manifest;
3. model-specific input/output serialization or prompt.

Adapters may translate between contracts, but no contract is defined as an incidental serialization of another.

## Consequences
Model experimentation remains isolated from business integrations; datasets can contain richer governance/annotation metadata; production APIs stay stable across model changes. The cost is explicit adapter/version management.