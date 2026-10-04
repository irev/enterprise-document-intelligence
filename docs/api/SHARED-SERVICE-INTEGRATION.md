# Shared Service Integration

**Class:** Normative when the platform is exposed as a shared service to multiple consumer applications.

## Purpose

A Document Intelligence deployment MAY serve multiple applications and tenants. Consumer application identity, tenant identity, request correlation, document identity, processing identity and business identity are distinct concepts and MUST NOT be silently conflated.

## Identity model

### Tenant

A tenant is an authorization and data-isolation boundary. Tenant identity MUST propagate through authorized storage, processing, review, delivery, audit and configuration resolution.

### Consumer application

A consumer application is a registered caller/integration identity within an authorized tenant scope.

A shared-service implementation MUST authenticate the calling application independently of caller-supplied business payload fields. It MUST authorize the application for the requested tenant, capability and resource.

An application identity MAY be authorized for one or more tenants according to deployment policy. Authorization MUST NOT be inferred solely from a `tenant_id` supplied in a request body.

### Correlation

Each accepted interaction MUST have a correlation identity suitable for tracing the logical interaction across ingestion, processing and outbound integration.

A caller-supplied correlation identity MAY be accepted when policy permits. The service MUST retain an unambiguous correlation identity even when the caller omits one.

Correlation identity is operational metadata. It MUST NOT be used as document identity, idempotency identity or business authorization.

### Request and processing identity

A service SHOULD assign a request/interaction identity to each inbound attempt.

A document has stable platform document identity. Each processing/reprocessing attempt has distinct processing identity/version. Reprocessing MUST NOT replace a prior completed result.

### External business references

Consumer applications MAY attach bounded opaque business references for reconciliation with their own records. Such references MUST NOT become platform primary identity and MUST NOT grant access to a document or result.

## Inbound contract

An accepted submission MUST be attributable to:

- authenticated consumer application;
- authorized tenant scope;
- correlation identity;
- idempotency identity where the operation requires it;
- receipt time;
- applicable profile/configuration identity when known;
- resulting platform document/processing identity.

Inbound operational records SHOULD avoid storing unrestricted request payload copies when references or bounded metadata are sufficient.

## Outbound integration

A shared service MAY expose results through polling, events, callbacks/webhooks, or equivalent mechanisms.

Where push delivery is claimed, each delivery attempt MUST be attributable to:

- logical outbound message/event identity;
- destination/subscription identity;
- tenant and consumer application scope;
- correlation identity;
- document/result version;
- attempt identity or number;
- attempt time;
- outcome;
- retry state when applicable.

A failed delivery MUST NOT change a completed document result into a failed processing result. Processing state and delivery state are separate.

Retries MUST NOT create a new logical result/event merely because transport delivery failed. Receivers MUST be able to deduplicate redelivery using stable logical identity.

## Subscription and destination security

Outbound destinations MUST be registered/authorized configuration rather than unrestricted document-provided URLs.

Implementations MUST prevent document content, extracted text or model output from controlling callback destinations.

Secrets used to authenticate outbound delivery MUST NOT be exposed in document results, generic errors, telemetry or operator views.

## Control plane

A deployment MAY provide an operational/control panel. The control plane MUST obey the same tenant/resource authorization boundaries as programmatic interfaces.

An operator panel MAY expose:

- inbound interactions;
- processing lifecycle;
- document/result/evidence inspection subject to authorization;
- review queues;
- outbound delivery attempts;
- provider/component health;
- configuration/version identity;
- audit records and operational metrics.

The control plane MUST NOT convert Document Intelligence findings or model predictions into business approval authority. Payment, accounting, procurement, tax or other privileged business authorization remains owned by the consuming business system or an explicitly separate authorized decision system.

## Observability

Inbound, processing and outbound telemetry SHOULD be traceable using correlation and stable platform identities without using raw document text or sensitive extracted values as metric labels.

Operational status MUST distinguish at least:

```text
processing outcome != review state != outbound delivery outcome
```

This distinction prevents an integration outage from being represented as a document-understanding failure.

## Configuration snapshots

Processing and outbound behavior that depends on versioned profiles, policies or integration configuration MUST retain sufficient version identity to reconstruct what configuration was applied.

Completed historical results MUST NOT be silently reinterpreted when application, subscription, profile or policy configuration changes.
