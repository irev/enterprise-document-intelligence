# ADR-0008: Tenant Policy Language Is Restricted and Non-Arbitrary

- Status: Accepted
- Date: 2026-10-04

## Context
Tenant-specific policy must be configurable, but executing arbitrary scripts creates severe security, determinism and auditability problems.

## Decision
Policy uses a versioned, typed, allow-listed declarative expression model. It must not execute arbitrary customer code, shell commands, SQL, JavaScript, Python, C#, or unrestricted templates.

## Consequences
Some complex policies require new reviewed operators or application code, but policy remains deterministic, testable, portable and safer to host in a multi-tenant platform.