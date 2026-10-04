# Master Plan — Enterprise Document Intelligence

**Status:** Active master delivery plan  
**Purpose:** Define the target product and the ordered capabilities required to reach a production-grade, multi-tenant Enterprise Document Intelligence / IDP platform.

This plan is technology-neutral at the platform-contract level. Named runtimes such as PaddleOCR, Ollama, LM Studio/llmster, and vLLM are reference implementation targets, not normative vendor requirements.

## Product goal

Deliver an enterprise Document Intelligence service that can ingest untrusted documents, preserve immutable source lineage, obtain factual OCR/layout evidence, apply local or explicitly authorized remote AI, validate and reconcile extracted facts, route uncertain work to humans, and publish durable results to business systems.

The platform MUST support fully on-premise operation. A tenant/application MUST be able to operate with remote AI disabled.

## Architectural goal

```text
Sources
  |
  v
Ingestion / Security / Immutable Source Observation
  |
  v
Deterministic Parsing
  |
  v
OCR + Layout Evidence
  |
  v
Vision Understanding
  |
  v
Semantic Classification / Extraction
  |
  v
Validation / Reconciliation / Confidence
  |
  +----> Human Review
  |
  v
Durable Result / Evidence / Delivery
```

The intelligence path is layered. OCR, vision models, and semantic AI are complementary capabilities rather than mutually exclusive replacements.

## Non-negotiable invariants

1. **Evidence before assertion.** Material extracted facts remain traceable to source observation, page/region, OCR/layout evidence, model execution, and component/model version where applicable.
2. **AI prediction is not business authorization.** AI components provide observations, predictions, evidence, confidence, and decision support.
3. **Tenant/application policy controls execution.** Customer-specific routing belongs in trusted configuration; platform guarantees remain in core.
4. **No implicit remote fallback.** Failure, low confidence, timeout, unavailable local runtime, or document content MUST NOT silently move data to a remote provider.
5. **Remote execution is explicit.** Remote invocation requires an execution route that permits it plus current tenant/application authorization and applicable egress controls immediately before invocation.
6. **Document content cannot change execution policy.** Untrusted content cannot select a provider, relax egress controls, grant authorization, or trigger remote escalation.
7. **Approved local fallback is allowed only by policy.** A configured local OCR/model may transition to another approved local runtime/model when the execution profile explicitly defines that route.
8. **Readiness is not authorization.** A healthy/ready runtime or model is not automatically permitted for a tenant. An authorized model that is not ready is not executable.
9. **Execution plans are not authorization grants.** Current trusted control-plane state is re-evaluated at invocation time.
10. **UNKNOWN and safe failure remain first-class outcomes.**

## Execution classes

The platform recognizes capability classes rather than hard-coding vendors:

- `DETERMINISTIC` — parsers, hashing, media inspection, deterministic transformations.
- `OCR` — text/layout/table/geometry recognition.
- `LOCAL_MODEL` — locally controlled vision, multimodal, language, classification, or extraction models.
- `REMOTE_MODEL` — externally hosted AI/model execution requiring explicit authorization and egress permission.
- `HUMAN` — human review or intervention.

## On-premise runtime target

### OCR and document structure

PaddleOCR is a required executable reference capability, not a placeholder adapter. The reference implementation should support factual OCR output and progressively support document structure/layout processing, including text, page/region geometry, confidence, tables, and other evidence-bearing structures where supported.

### Local model runtimes

The reference implementation should support multiple local runtime adapters without coupling the business core to a runtime:

- Ollama
- LM Studio / headless server runtime
- vLLM
- future approved local runtimes through the same capability contract

A reusable OpenAI-compatible transport MAY be used where appropriate, but endpoint compatibility MUST NOT be treated as proof that an endpoint is local or trusted. Locality and egress classification come from trusted configuration.

### Remote providers

Remote AI providers remain optional. They are separate execution targets and MUST NOT become automatic fallback for local failures.

## AI/OCR control plane

The platform needs a durable control plane for:

- provider/runtime registry;
- model registry and artifact identity;
- runtime/model capabilities;
- tenant/application execution profiles;
- primary and explicitly configured fallback routes;
- local/remote execution classification;
- egress policy;
- provider and model authorization;
- version policy;
- timeout/retry policy;
- resource requirements;
- readiness requirements;
- activation/drain state;
- audit history.

A tenant execution profile determines which methods are intended for that tenant/application, but invocation-time policy and authorization remain authoritative.

## Runtime and model readiness

Readiness monitoring is a platform capability. It should distinguish at least:

```text
NOT_INSTALLED
INSTALLED
STARTING
DOWNLOADING
LOADING
READY
DEGRADED
UNHEALTHY
DRAINING
UPDATING
ROLLING_BACK
DISABLED
```

Readiness evaluation should be able to inspect:

- runtime process/API availability;
- runtime version and approved-version policy;
- required model artifact availability;
- model version/digest;
- load/warm state;
- declared capability;
- CPU/GPU/RAM/VRAM/resource sufficiency where applicable;
- smoke inference;
- operational latency/error signals;
- control-plane enablement.

`HEALTHY`, `READY`, and `AUTHORIZED` are distinct states.

## Runtime/model lifecycle

Production model/runtime lifecycle should support:

```text
DISCOVER -> INSTALL -> VERIFY -> STAGE -> SMOKE_TEST -> ACTIVATE -> READY
```

Updates should support staged activation:

```text
active version
  -> acquire candidate
  -> verify artifact/checksum
  -> compatibility check
  -> load/warm
  -> smoke test
  -> drain previous version
  -> activate candidate
```

A failed candidate should permit rollback to a retained approved version. Production auto-update is OFF by default.

For large model artifacts, “backup” means versioned artifact identity, manifest/checksum, retention, and a known rollback target; it does not require blindly duplicating every model binary.

## Delivery roadmap

### Foundation — completed or substantially established

- Core document pipeline and canonical contracts.
- Classification/extraction contracts.
- Provider-neutral execution planning.
- Local OCR/provider execution boundary.
- PostgreSQL durable control plane.
- Durable ingestion and outbox.
- Source lineage and acquisition.
- Processing ownership, leases, reclaim, and generation fencing.
- Observation identity dispatch.
- Durable lineage referential integrity.
- Canonical source observation.
- Long-running processing safety.
- Tenant-scoped provider authorization.
- Migration orchestration.
- CI lint/coverage/static-type quality baseline in progress.

### Immediate stabilization

1. Finish CI quality gate work and keep runtime tests authoritative.
2. Harden processing-claim observation digest referential integrity with an additive migration.
3. Preserve migration checksum immutability; never rewrite applied historical migrations.

### Intelligence execution foundation

4. **Executable PaddleOCR**
   - installable reference dependency/profile;
   - real OCR invocation;
   - process isolation and timeout;
   - deterministic failure semantics;
   - synthetic integration/smoke test;
   - no silent remote fallback.

5. **Structured OCR/layout evidence**
   - page and region identity;
   - text;
   - bounding geometry;
   - confidence;
   - layout/table structures where supported;
   - provenance back to the exact source observation.

6. **Local Model Runtime Contract**
   - runtime discovery;
   - model inventory;
   - capability discovery;
   - readiness;
   - inference;
   - structured output;
   - version identity;
   - lifecycle hooks.

7. **Local runtime adapters**
   - Ollama;
   - LM Studio/headless runtime;
   - vLLM;
   - extensibility contract for additional runtimes.

8. **Local-failure security tests**
   - OCR failure does not invoke remote vision;
   - local vision failure does not invoke remote model;
   - low confidence does not grant remote escalation;
   - document instructions cannot alter routing;
   - explicitly configured local fallback remains possible.

### Durable intelligence results

9. Durable ProcessingRun integration.
10. Durable result and evidence persistence.
11. Validation, reconciliation, confidence, and finding persistence.
12. Full provenance chain from result to model execution, OCR/layout evidence, source region/page, source observation, and original document reference.

### Control plane and tenant routing

13. Runtime registry.
14. Model/artifact/deployment registry.
15. Runtime/model readiness monitor.
16. Lifecycle manager for install, verify, stage, activate, drain, update, retention, and rollback.
17. Tenant/application execution profiles.
18. Policy-driven execution router using capability + readiness + authorization + egress policy.
19. Explicit local fallback chains.
20. Explicit remote routes; never implicit cloud fallback.

### Enterprise workflow

21. Human review.
22. Reliable result delivery, events, and webhooks.
23. Operations and observability.
24. Shared-service API.
25. Operations API/UI for runtime, model, GPU/resource state, tenant routing, readiness, update/rollback, and audit.

### SaaS / production hardening

26. Multi-tenant isolation hardening.
27. Quotas, concurrency, workload/resource isolation.
28. Secrets and credential lifecycle.
29. Data residency and egress controls.
30. Model/runtime supply-chain controls and artifact verification.
31. Backup/recovery and disaster-recovery procedures for durable state.
32. Production deployment profiles: fully on-premise, hybrid, and explicitly remote-enabled.

## Reference execution examples

### Fully on-premise tenant

```text
PaddleOCR
   -> approved local vision model
   -> approved local semantic model
   -> validation/reconciliation
   -> result or human review

REMOTE_MODEL = DENIED
```

### Hybrid tenant

```text
PaddleOCR
   -> local vision
   -> local semantic model
   -> explicitly authorized remote route, only when the configured
      execution policy calls for it and invocation-time authorization
      plus egress controls permit it
```

Local failure alone is never sufficient reason for the remote transition.

## Definition of target state

The master goal is reached when the platform can:

- process documents end-to-end with a fully local execution profile;
- run PaddleOCR as a real supported OCR capability;
- use approved local vision/semantic models through interchangeable runtimes;
- configure execution method per tenant/application;
- prove that local failures cannot silently exfiltrate data to remote AI;
- monitor runtime/model readiness independently from authorization;
- install, stage, update, retain, and roll back approved runtime/model versions;
- retain durable lineage, results, evidence, review state, and delivery state;
- expose operational status and audit history;
- optionally use remote AI only through explicit policy and current authorization;
- scale toward a shared multi-tenant enterprise service without moving customer-specific behavior into core code.

## Plan governance

This file is the master delivery direction. Detailed architecture specifications, ADRs, security requirements, schemas, and reference milestones may refine individual items but MUST NOT silently weaken the non-negotiable invariants above.

When implementation experience reveals a portable platform invariant, promote that invariant into the technology-neutral specification. Runtime-specific installation commands, Python/PostgreSQL implementation details, and vendor-specific behavior remain in the reference implementation or deployment documentation.
