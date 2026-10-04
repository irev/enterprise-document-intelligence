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
