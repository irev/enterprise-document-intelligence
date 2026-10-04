# Evaluation Harness Specification

## Objective

Provide reproducible offline evaluation independent of a particular model provider.

## Inputs

- immutable dataset manifest/version;
- annotations;
- document/profile/taxonomy versions;
- candidate adapter/model configuration;
- confidence/decision policy.

## Outputs

Machine-readable report containing:
- run ID and timestamp;
- source revision;
- dataset manifest hash/version;
- model/provider/version;
- taxonomy/profile versions;
- per-class classification metrics;
- per-field extraction metrics;
- UNKNOWN/OOD metrics;
- calibration metrics where applicable;
- known-vs-unseen template segments;
- challenge-set results;
- latency/cost measurements where collected;
- failed/unsupported sample IDs;
- threshold configuration.

## Reproducibility

Evaluation code must not mutate the gold dataset. Cache/provider nondeterminism must be declared. Where a generative model is nondeterministic, report inference settings and consider repeated-run stability for high-risk fields.

## Release comparison

Compare candidate vs currently approved release and fail gates on critical regressions even when aggregate metrics improve.

## No production leakage

Evaluation credentials and fixtures must not cause governed production documents to be copied into CI artifacts or public logs.