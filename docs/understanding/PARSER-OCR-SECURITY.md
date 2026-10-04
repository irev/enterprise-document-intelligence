# Parser and OCR Security

**Class:** Normative for document-understanding implementations.

## Trust boundary

Source bytes, embedded objects, metadata and extracted text are untrusted content.

A parser/OCR implementation MUST prevent document content from becoming executable control instructions. Embedded scripts, macros, actions or attachments MUST NOT execute as part of ordinary document understanding.

## Resource controls

Implementations MUST enforce bounded processing resources appropriate to their deployment, including document/page/output limits and bounded execution time. Temporary processing material MUST follow the source-acquisition cleanup policy.

Recursive/container expansion and decompression amplification MUST be bounded. Resource exhaustion MUST fail explicitly rather than silently producing a completed result.

## Isolation

Parser/OCR components SHOULD execute with the minimum privileges and isolation appropriate to the component risk. Local parsing SHOULD NOT require outbound network access.

Remote OCR/model processing is a data-egress boundary and MUST be explicitly authorized by tenant/deployment policy. Provider identity/version and applicable processing provenance MUST be retained.

## Failure semantics

Implementations MUST distinguish security/reliability relevant non-success states using stable machine codes. Provider exceptions, local filesystem paths, commands, credentials and sensitive diagnostics MUST NOT be returned as generic consumer-visible failures.

## Provenance

Document-understanding output MUST remain bound to the exact SourceObservation processed. Parser/OCR component identity and version MUST be reconstructable.

Canonical page output MUST have stable page identity/order suitable for later evidence references.

## Prompt-injection boundary

Extracted text is evidence/content, not instruction. Text contained in a document MUST NOT alter system policy, tool authorization, destination selection, tenant scope, validation policy or business authorization.


## Canonical structure and coordinates

Document-understanding implementations SHOULD expose evidence-grade page structure rather than only a concatenated text stream when the source/provider can supply layout.

Canonical region coordinates MUST use a declared coordinate system. The reference canonical convention is normalized page coordinates with top-left origin and ordered bounds `0 <= x0 <= x1 <= 1`, `0 <= y0 <= y1 <= 1`.

Page/block identifiers and reading order MUST be deterministic within a completed understanding result. Evidence references MUST remain resolvable to the SourceObservation and page/region from which they were derived.

Layout/table structure and confidence remain observations produced by parsing/OCR; their structural validity MUST NOT be interpreted as authenticity or business validity.
