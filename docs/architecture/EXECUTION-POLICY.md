# Processing Capability and Execution Policy

**Class:** Normative platform architecture.

## Principle

The platform MUST define required processing capabilities and result contracts independently from any OCR, AI, model vendor, deployment topology, or network provider.

Applications and tenants MAY require different execution constraints. A deployment MAY operate with deterministic parsing only, OCR only, local models only, remote providers, hybrid providers, or human review, provided the selected path satisfies the requested capability contract.

## Capability request

A processing request/profile SHOULD be able to declare:
- required outcomes/capabilities, such as text extraction, layout, classification, field extraction, or validation;
- allowed execution classes;
- data-egress policy;
- fallback policy;
- quality/confidence requirements;
- resource and latency constraints where applicable.

Applications MUST NOT select privileged provider credentials or arbitrary executable components through document content.

## Execution classes

Portable execution classes are:
- `DETERMINISTIC`: non-model parsing/normalization/rules;
- `OCR`: optical character recognition engine;
- `LOCAL_MODEL`: model execution within the deployment's trusted local boundary;
- `REMOTE_MODEL`: model/provider requiring approved external data transfer;
- `HUMAN`: authorized human review.

These classes describe execution/security characteristics, not products.

A profile MAY declare `LOCAL_MODEL` as the only allowed model class. A conforming service MUST NOT silently fall back to `REMOTE_MODEL` when remote execution is prohibited.

## Planning versus execution

Provider selection MUST be a control-plane decision derived from versioned policy and registered capabilities. Document text MUST NOT choose a provider, relax egress restrictions, or enable a capability.

The execution plan SHOULD be recorded before provider invocation and MUST retain sufficient provenance to reconstruct:
- requested capabilities;
- selected execution class/provider;
- policy/profile version;
- fallback decision;
- provider/model/engine version used for produced claims.

An execution plan is a selection record, **not an authorization grant**. Immediately before invocation, the service MUST re-authorize the selected provider against the current trusted control-plane state. At minimum, execution MUST fail before provider code is invoked when the provider is no longer enabled or is no longer permitted for the requesting tenant or application. A stale plan MUST NOT preserve provider access that has subsequently been revoked.

Plan/provider identity MUST also remain consistent at invocation time: provider identity/version, execution class, and requested capability MUST match the planned step. Implementations MAY use different internal mechanisms, but the observable behavior MUST preserve this fail-closed property.

Application authorization MUST preserve the application's tenant scope. When application identifiers are tenant-local, authorization for one `(tenant, application)` pair MUST NOT authorize an application with the same identifier under another tenant. Implementations MUST NOT flatten tenant-scoped application authorization into a deployment-global application identifier.

## Fail closed

When no registered provider can satisfy the required capability and execution constraints, the service MUST return an explicit non-success/review outcome. It MUST NOT broaden the allowed execution classes automatically.

## Interoperability

Canonical results MUST remain provider-neutral. Replacing a local model with another local model, an OCR engine, or an approved remote provider MUST NOT require a business application to adopt provider-specific result schemas.

Provider-specific metadata MAY be retained as extension/provenance data but MUST NOT redefine canonical semantics.
