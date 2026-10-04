# Enterprise Document Intelligence

Enterprise architecture and engineering standards for document classification, extraction, validation, evidence, human review, dataset governance, evaluation, security, and AI-assisted document processing.

> **Status:** Initial architecture baseline (v0.1). RFP / Accounts Payable is the first reference use case, not the platform boundary.

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

### Architecture decisions
- [ADR-0001 — AI Prediction Is Not a Business Decision](docs/adr/0001-ai-prediction-not-business-decision.md)

## Dataset policy

Do **not** commit confidential production documents or uncontrolled derived datasets to this repository. Actual corpora belong in approved governed storage. See [datasets/README.md](datasets/README.md).

## Implementation neutrality

The architecture intentionally does not mandate a specific OCR engine, VLM, LLM, classifier, programming language, cloud provider, or database. Implementations must conform to the contracts and measurable acceptance criteria rather than a specific vendor.

## Next specification milestones

The baseline still requires validation against representative corporate documents and business requirements. Expected next artifacts include machine-readable JSON Schemas, API/event contracts, document-profile definitions, threat model, data-retention policy, model lifecycle/release policy, observability/SLO specification, RFP reference profile, and executable evaluation fixtures.
