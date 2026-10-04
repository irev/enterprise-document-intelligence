# Auditability

For material results preserve as appropriate: immutable document ID/source hash, timestamps, schema/taxonomy version, parser/OCR version, classifier/extractor version, prompt version when applicable, validation ruleset, tenant configuration version, evidence, confidence, findings and human-review history.

The system should answer: **What did it observe, which component/version produced the result, which rules were applied, and was it later changed by a human?**

Audit logs must not become uncontrolled copies of sensitive document content.