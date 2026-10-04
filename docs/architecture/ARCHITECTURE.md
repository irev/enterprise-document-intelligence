# Architecture

```text
Sources: PDF / Image / Office / API / Email
  -> Ingestion & Security
  -> Native Parsing / OCR / Layout / Tables
  -> Classification + UNKNOWN/OOD
  -> Extraction + Normalization
  -> Structural / Semantic / Cross-document Validation
  -> Evidence + Confidence + Findings
  -> Human Review when required
  -> Business Systems: RFP / AP / Procurement / ERP / Audit
```

## Boundaries
**Ingestion:** verify MIME/magic bytes, limits, hash/duplicates and security controls. Preserve immutable source identity.

**Understanding:** prefer reliable native extraction; use OCR when required. OCR output is not ground truth.

**Classification:** return family/type/subtype, confidence and model version. UNKNOWN is valid.

**Extraction:** material fields preserve raw value, normalized value, confidence and evidence.

**Validation:** separate structural, semantic, cross-document and business validation. Business authorization stays outside probabilistic model behavior.

**Review:** preserve original prediction and human correction; never silently overwrite history.

## Integration
Consumers use stable APIs/events and canonical schemas, never direct dependencies on a particular OCR engine, VLM, LLM or prompt.

## Versioning
Preserve schema, taxonomy, parser/OCR, model, prompt (when applicable), ruleset and tenant-configuration versions.