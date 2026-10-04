# Calibration and Release Gates

**Class:** Normative when calibrated confidence or model release gating is claimed

## Calibration

Calibration MUST be evaluated on governed representative data for the population where the score will be used. A single global calibration metric SHOULD NOT hide materially different behavior across document type, template/vendor family, language, scan quality or high-risk fields.

Implementations SHOULD report appropriate calibration metrics such as expected calibration error, Brier score or negative log-likelihood when meaningful for the model/output.

A confidence score MUST NOT be described as a probability of correctness unless the evaluation supports that interpretation.

## Release comparison

Candidate releases MUST be compared against an approved baseline on the same governed evaluation definition when release gating is claimed.

Aggregate improvement MUST NOT automatically override a critical regression. Release policy MAY define critical metrics/segments such as:
- false acceptance of high-risk amount/identity fields;
- UNKNOWN/OOD rejection;
- unseen template performance;
- cross-document validation;
- security/challenge cases.

The release decision and policy/version used MUST be recorded.

Machine contracts:
- `schemas/evaluation/calibration-report.schema.json`
- `schemas/evaluation/release-comparison.schema.json`
