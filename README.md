# Enterprise Document Intelligence

Enterprise architecture and engineering standards for document classification, extraction, validation, evidence, human review, dataset governance, evaluation, security, and AI-assisted document processing.

> **Status:** Technology-neutral specification and conformance baseline (v0.6). RFP / Accounts Payable is the first reference use case, not the platform boundary.

## Core principles

1. Document evidence > model assertion.
2. AI prediction is not a business decision.
3. Dataset schema, production schema, and model prompt are separate contracts.
4. Customer-specific behavior belongs in configuration; platform guarantees belong in core.
5. Every material prediction must be traceable to evidence and component/version provenance.
6. Low confidence must fail safely rather than guess.
7. Documents are untrusted input.
8. UNKNOWN / out-of-distribution is a first-class outcome.

## Processing model

```text
PDF / Image / Office / API / Email
        |
        v
Ingestion & Security
        |
        v
Parsing / OCR / Layout / Tables
        |
        v
Classification + UNKNOWN/OOD
        |
        v
Extraction + Normalization
        |
        v
Structural / Semantic / Cross-document Validation
        |
        v
Evidence + Confidence + Findings
        |
        +------> Human Review
        |
        v
RFP / AP / Procurement / ERP / Audit / other consumers
```

AI components provide predictions and evidence. Payment authorization, approval policy, accounting actions, and other privileged business decisions remain deterministic responsibilities of consuming business systems.

## Specification status

This repository is a **technology-neutral specification**, not a reference application. Start with:
- [Specification scope and requirement language](SPECIFICATION.md)
- [Normative map](docs/specification/NORMATIVE-MAP.md)
- [Platform conformance](docs/conformance/PLATFORM-CONFORMANCE.md)
- [Conformance levels](docs/conformance/CONFORMANCE-LEVELS.md)
- [Conformance test matrix](docs/conformance/TEST-MATRIX.md)
- [Versioning & compatibility](docs/interoperability/VERSIONING-AND-COMPATIBILITY.md)
- [Extension model](docs/interoperability/EXTENSION-MODEL.md)
- [v0.6 gap analysis](docs/specification/GAP-ANALYSIS-v0.6.md)

## Specification map

### Foundation
- [Vision](docs/VISION.md)
- [Architecture Principles](docs/PRINCIPLES.md)
- [Glossary](docs/GLOSSARY.md)
- [Architecture](docs/architecture/ARCHITECTURE.md)

### Document contracts
- [Document Taxonomy](docs/taxonomy/DOCUMENT-TAXONOMY.md)
- [Canonical Document Schema](docs/schemas/CANONICAL-DOCUMENT-SCHEMA.md)
- [Field Schemas](docs/schemas/FIELD-SCHEMAS.md)
- [Validation Rules](docs/validation/VALIDATION-RULES.md)

### Dataset & evaluation
- [Annotation Guidelines](docs/datasets/ANNOTATION-GUIDELINES.md)
- [Dataset Governance](docs/datasets/DATASET-GOVERNANCE.md)
- [Dataset Split Policy](docs/datasets/DATASET-SPLIT-POLICY.md)
- [Evaluation Protocol](docs/evaluation/EVALUATION-PROTOCOL.md)
- [Confidence Policy](docs/evaluation/CONFIDENCE-POLICY.md)

### Enterprise controls
- [Human Review](docs/human-review/HUMAN-REVIEW.md)
- [Security](docs/security/SECURITY.md)
- [Auditability](docs/governance/AUDITABILITY.md)
- [Multi-Tenancy](docs/governance/MULTI-TENANCY.md)

### API, events & processing contracts
- [OpenAPI 3.1 specification](openapi/openapi.yaml)
- [API Contract](docs/api/API-CONTRACT.md)
- [Event Contract](docs/api/EVENT-CONTRACT.md)
- [Error Taxonomy](docs/api/ERROR-TAXONOMY.md)
- [Processing State Machine](docs/architecture/PROCESSING-STATE-MACHINE.md)
- [RFP / Accounts Payable Reference Profile](docs/reference/RFP-REFERENCE-PROFILE.md)
- [RFP Requirement Matrix](docs/reference/RFP-REQUIREMENT-MATRIX.md)
- [AsyncAPI 3.0 specification](asyncapi/asyncapi.yaml)
- [Machine-readable canonical schema](schemas/canonical/document-result.schema.json)
- [Machine-readable event schema](schemas/events/document-events.schema.json)
- [Document profile schema](schemas/profiles/document-profile.schema.json)
- [Dataset manifest schema](schemas/datasets/dataset-manifest.schema.json)
- [Annotation schema](schemas/annotations/document-annotation.schema.json)
- [RFP requirement-profile schema](schemas/business/rfp-requirement-profile.schema.json)
- [Document bundle schema](schemas/bundles/document-bundle.schema.json)
- [Deterministic rule-set schema](schemas/policies/rule-set.schema.json)
- Concrete profiles: [Invoice](profiles/invoice.profile.json), [Purchase Order](profiles/purchase-order.profile.json), [Contract](profiles/contract.profile.json), [Tax Invoice](profiles/tax-invoice.profile.json)

### Operations & model governance
- [Threat Model](docs/security/THREAT-MODEL.md)
- [Observability & SLO](docs/operations/OBSERVABILITY-SLO.md)
- [Model Lifecycle](docs/models/MODEL-LIFECYCLE.md)
- [Data Retention](docs/governance/DATA-RETENTION.md)
- [Privacy & Data Classification](docs/governance/PRIVACY-DATA-CLASSIFICATION.md)
- [Reference Deployment](docs/architecture/REFERENCE-DEPLOYMENT.md)
- [Evaluation Test Cases](docs/evaluation/TEST-CASES.md)
- [Implementation Guide](docs/implementation/IMPLEMENTATION-GUIDE.md)
- [Persistence Model](docs/domain/PERSISTENCE-MODEL.md)
- [Rule Engine](docs/policy/RULE-ENGINE.md)
- [Review Concurrency](docs/human-review/REVIEW-CONCURRENCY.md)
- [Deduplication & Idempotency](docs/ingestion/DEDUPLICATION.md)
- [Provider Conformance](docs/providers/CONFORMANCE.md)
- [Evaluation Harness](docs/evaluation/HARNESS.md)
- [RFP Integration Lifecycle](docs/reference/RFP-INTEGRATION-LIFECYCLE.md)
- [Security Hardening Profile](docs/security/SECURITY-HARDENING-PROFILE.md)
- [Adapter Contracts](docs/implementation/ADAPTER-CONTRACTS.md)

### Architecture decisions
- [ADR-0001 — AI Prediction Is Not a Business Decision](docs/adr/0001-ai-prediction-not-business-decision.md)
- [ADR-0002 — Separate Canonical, Dataset, and Prompt Contracts](docs/adr/0002-separate-canonical-dataset-and-prompt-contracts.md)
- [ADR-0003 — UNKNOWN Is a First-Class Classification Outcome](docs/adr/0003-unknown-is-first-class-classification.md)
- [ADR-0004 — Asynchronous Processing Is the Default Contract](docs/adr/0004-asynchronous-processing-contract.md)
- [ADR-0005 — Evidence Is Required for Material Extraction](docs/adr/0005-evidence-required-for-material-extraction.md)
- [ADR-0006 — Tenant Business Requirements Are Versioned Configuration](docs/adr/0006-tenant-business-requirements-are-configuration.md)
- [ADR-0007 — Completed Processing Results Are Versioned and Immutable](docs/adr/0007-processing-results-are-versioned-and-immutable.md)
- [ADR-0008 — Tenant Policy Language Is Restricted and Non-Arbitrary](docs/adr/0008-policy-language-is-non-turing-complete.md)

## Dataset policy

Do **not** commit confidential production documents or uncontrolled derived datasets to this repository. Actual corpora belong in approved governed storage. See [datasets/README.md](datasets/README.md).

## Implementation neutrality

The architecture intentionally does not mandate a specific OCR engine, VLM, LLM, classifier, programming language, cloud provider, or database. Implementations must conform to the contracts and measurable acceptance criteria rather than a specific vendor.

## Next specification milestones

The v0.6 audit identifies the remaining specification gaps explicitly. The next milestone should prioritize the typed policy AST, canonical field-state/evidence-coordinate semantics, reusable structured fields, identity-resolution boundaries, and technology-neutral conformance vectors. Stack-specific reference implementations belong in separate repositories or clearly non-normative profiles.


## AI coding agents

[AGENTS.md](AGENTS.md) defines mandatory architecture constraints for coding agents. Agents must treat the schemas, API/event specifications, principles, and ADRs as source-of-truth contracts.

## Contract validation

[Contract Validation](.github/workflows/contracts.yml) validates JSON/JSON Schema, concrete profiles, the synthetic RFP requirement profile, OpenAPI, and baseline AsyncAPI structure on relevant pushes and pull requests.
