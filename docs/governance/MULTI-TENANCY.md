# Multi-Tenancy

## Core platform
Canonical contracts, secure processing, evidence/provenance, audit guarantees, taxonomy mechanisms, validation framework and API/event semantics.

## Tenant configuration
Enabled document profiles, field aliases/mappings, calibrated review thresholds, business requirement profiles, integration mappings and customer-specific deterministic policies.

Avoid scattering branches such as `if customer == "CompanyA"` through core code. Resolve versioned configuration/policy at controlled boundaries.

Tenant identity propagates through authorization, storage, processing, review, telemetry and dataset governance. Cross-tenant data is never implicitly reused for training, retrieval, examples or evaluation.