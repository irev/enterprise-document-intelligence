# Source Acquisition

**Class:** Normative semantics for externally owned source documents.

## Ownership

The Document Intelligence service processes documents and need not become the authoritative document repository. A deployment MUST declare which system owns original-document retention and versioning.

## Model

These concepts are distinct:

- **SourceReference**: identifies the source resource and acquisition method.
- **SourceAcquisition**: one attempt to obtain document bytes.
- **SourceObservation**: immutable facts about the exact bytes observed.
- **ProcessingRun**: one processing attempt bound to a SourceObservation.

A SourceObservation does not imply permanent storage of source bytes.

## Acquisition methods

A deployment MAY support direct upload/stream, temporary HTTPS retrieval, managed SFTP/object-storage/file-share/application connectors, or other adapters preserving these semantics. The processing core MUST NOT depend on one protocol.

Durable source metadata MUST NOT contain access secrets. Managed connections SHOULD refer to separately protected connection configuration.

## Observation

Every successful acquisition MUST compute a cryptographic content digest over the exact bytes supplied to processing.

An observation SHOULD record the digest, byte length, detected media type, acquisition time and, when available, external version, ETag, source modification metadata and connector configuration version.

External version metadata does not replace the content digest as evidence of the bytes observed.

## REPROCESS

REPROCESS targets a previously observed source revision. If the service does not retain the bytes, it MAY acquire the resource again, but MUST verify the new digest against the targeted observation before processing. A mismatch MUST return `SOURCE_CHANGED` and MUST NOT silently process different bytes as the same revision.

## REFETCH

REFETCH obtains the current source and establishes its observation without requiring processing. An unchanged digest MAY reuse the existing logical observation, but the acquisition attempt and unchanged outcome MUST remain auditable.

## REFETCH_AND_REPROCESS

REFETCH_AND_REPROCESS obtains the current source, establishes the observed content identity, and creates a new ProcessingRun against that observation. Changed content MUST remain distinguishable from prior observations and results.

## Temporary bytes

Temporary document bytes are sensitive untrusted data. Temporary copies MUST have a bounded lifetime, MUST be purged after processing or failure according to policy, and MUST NOT be exposed as durable source locations or generic telemetry.

## Evidence

Evidence MUST identify the SourceObservation/result context from which it was derived and MUST NOT depend solely on an ephemeral filesystem path.

If the service does not retain original bytes, historical visual reproduction depends on the source owner retaining the corresponding source revision. Deployment and audit policy MUST make that responsibility explicit.


## Reliable processing dispatch

Acceptance persistence and creation of the durable processing intent MUST be atomic, or an implementation MUST provide equivalent semantics that cannot lose an accepted processing request after a crash.

Dispatch MAY be at-least-once. When it is, processing consumers MUST deduplicate using a stable message/processing identity. Queue or event payloads MUST NOT contain source credentials and SHOULD carry references/content identity rather than document bytes.

## Network acquisition security

A managed connector endpoint is control-plane configuration. A data-plane caller MUST NOT be able to turn an authorized connector identifier into an arbitrary network endpoint.

Network acquisition implementations MUST apply destination policy at connection time, including resolution/redirect checks where applicable, bounded transfer size and timeouts. Validation of URL syntax alone is insufficient.

Sensitive URL components, credentials, raw source bytes and provider exception details MUST NOT be emitted to generic logs or audit records.


## Processing consumer reliability

When dispatch is at-least-once, redelivery of the same logical processing message MUST NOT create duplicate completed processing results.

The implementation MUST use stable message identity and an atomic claim/deduplication mechanism. If processing leases are used, active leases MUST prevent concurrent execution and expired leases MAY be reclaimed without silently changing the logical processing identity.

Messages received from an internal broker MUST still be validated as transport input. Message types and content-reference forms MUST be allow-listed/validated before processing.

Provider exception details MUST NOT become durable public failure messages. Stable failure codes SHOULD be used for operational state while sensitive diagnostics remain access-controlled.


## Observation authorization and lineage

A SourceObservation identifier MUST NOT be treated as an authorization capability. Every read, reprocess, refetch and processing-run binding MUST enforce the authorized tenant/resource scope.

Each ProcessingRun MUST remain bound to the exact SourceObservation it processed. Historical runs MUST NOT be rebound when an external resource changes.

Implementations MUST prevent content digests from becoming cross-tenant existence or deduplication oracles. Digest lookup and duplicate handling MUST preserve tenant isolation.

REFETCH with unchanged content MAY reuse the same logical observation while retaining a separate acquisition audit record. Changed content MUST resolve to a distinct observation identity for that logical document before new processing is created.

External version identifiers, ETags and timestamps are provenance metadata; they MUST NOT override a mismatch in cryptographic content identity.
