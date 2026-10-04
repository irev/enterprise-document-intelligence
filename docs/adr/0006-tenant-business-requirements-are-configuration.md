# ADR-0006: Tenant Business Requirements Are Versioned Configuration

- Status: Accepted
- Date: 2026-10-04

## Context
Different customers and payment scenarios require different supporting documents and thresholds. Encoding those differences in taxonomy or customer-name branches would couple the platform to individual deployments.

## Decision
Document identity/taxonomy remains generic. RFP and other business requirement matrices are deterministic, versioned tenant configuration/policy evaluated using authoritative business context.

## Consequences
The same document intelligence platform can support multiple customers/processes without redefining document classes. Configuration governance and historical policy-version provenance become mandatory.