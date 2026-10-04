# RFP ↔ Document Intelligence Lifecycle

## 1. RFP establishes authoritative context

The RFP system creates/owns the payment request and supplies allowed context such as tenant, request reference, payment category, vendor/master references, procurement references, currency and requirement-profile identity.

## 2. Documents are submitted

Each file receives an independent Document Intelligence identity. RFP stores references; it does not infer processing completion from upload success.

## 3. Document processing

The platform performs ingestion, understanding, classification, extraction and document validation asynchronously.

## 4. Bundle assembly

RFP or an integration service associates relevant completed processing versions into a versioned document bundle.

## 5. Requirement and reconciliation evaluation

The platform/rules layer evaluates configured document requirements and cross-document consistency using the bundle plus explicitly supplied authoritative context.

## 6. Human review

Uncertain extraction/classification is reviewed. Corrections are tied to the exact processing result version.

## 7. Result consumption

RFP consumes:
- document identities/types;
- normalized extracted fields;
- evidence;
- findings;
- confidence/review state;
- requirement satisfaction status.

## 8. Business workflow

RFP applies its own authorization/workflow policy. A clean AI/document result is **not** payment approval.

## Change handling

Adding/replacing a supporting document creates a new bundle version/evaluation. Historical bundle and finding provenance remains reconstructable.