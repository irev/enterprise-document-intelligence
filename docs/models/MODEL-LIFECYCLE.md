# Model Lifecycle

## Stages

`EXPERIMENT -> CANDIDATE -> VALIDATED -> APPROVED -> DEPLOYED -> RETIRED`

## Release record

Every candidate records:
- model/artifact identifier and checksum;
- base model/provider where applicable;
- code/preprocessing version;
- training dataset manifest/version;
- taxonomy and schema versions;
- training configuration;
- evaluation dataset/version;
- per-segment metrics and calibration;
- known limitations;
- security/privacy review status;
- approval and deployment history.

## Gates

A candidate must not be promoted solely because aggregate accuracy improved. Check critical-class regressions, unseen-template performance, OOD behavior, calibration, false accepts, latency/cost and security/privacy implications.

## Rollback

Keep previous approved artifacts/configuration deployable. Model, prompt, threshold and rules changes must be independently identifiable so incidents can be attributed and rolled back with minimal scope.

## Drift

Monitor input distribution, UNKNOWN rate, confidence/review distributions and verified error rates. Drift signals trigger investigation; they do not automatically retrain or deploy a model.

## Feedback

Production corrections enter a governed candidate pool. Dataset admission requires provenance, eligibility and quality review.