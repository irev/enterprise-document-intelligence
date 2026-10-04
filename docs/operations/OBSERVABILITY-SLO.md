# Observability and SLO

## Telemetry dimensions

Prefer bounded dimensions: tenant (subject to policy), document type, pipeline stage, model/rules version, outcome, review state. Never use raw document text or unbounded document IDs as metric labels.

## Core metrics

- documents received/completed/failed;
- stage latency and end-to-end latency percentiles;
- parser/OCR failure rate;
- classification distribution and UNKNOWN rate;
- extraction failure/missing-field rate;
- confidence distribution;
- review-request and correction rate;
- false-accept/false-reject metrics from labeled feedback;
- queue depth/backlog;
- retries/timeouts;
- cost per document where measurable.

## Tracing

A correlation ID should connect ingestion, processing stages, review and outbound integration without placing sensitive content in span names/attributes.

## SLO policy

Do not invent production SLO numbers before workload and business criticality are known. Define measurable SLOs for:
- availability of submission/result APIs;
- successful processing rate for supported documents;
- end-to-end latency by document-size/profile class;
- review-queue service targets where owned by the platform.

Accuracy/model quality is governed by the evaluation protocol and release gates, not hidden inside infrastructure availability SLOs.

## Alerting

Alert on user-impacting symptoms and sustained error-budget burn, plus security/integrity conditions requiring immediate attention. Avoid alerting directly on noisy individual model scores.