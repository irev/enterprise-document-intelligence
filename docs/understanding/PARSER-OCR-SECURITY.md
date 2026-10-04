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


## Quality assessment and OCR routing

OCR routing SHOULD be explainable and page-scoped. Implementations SHOULD retain the observable quality signals and reason codes that led to an OCR decision.

A document MAY contain native-text, OCR-derived and mixed pages. OCR output MUST NOT silently replace higher-quality native text without retaining origin/provenance.

Automatic OCR selection SHOULD use multiple relevant quality signals rather than treating a single provider confidence or text-count threshold as universal truth. Borderline/ambiguous quality MUST have an explicit safe outcome such as review or deployment policy fallback.

OCR thresholds are configuration subject to empirical calibration; they are not platform invariants. Document content MUST NOT be able to select an unauthorized OCR provider or override data-egress policy.


## Evidence references

Machine claims that rely on document content SHOULD reference canonical evidence locators rather than only copying extracted strings.

An evidence locator MUST remain bound to the SourceObservation identity and content digest used to produce the understanding result. It MUST NOT be silently rebound to a later source version.

Evidence MAY reference a canonical text block, table cell or bounded page region. If a source quote is retained, it is supplemental validation/display data and does not replace the structural locator.

Evidence access MUST follow the authorization scope of the parent document/result. Observation IDs, content digests, block IDs and coordinates MUST NOT be treated as bearer capabilities.

Evidence provenance establishes traceability, not authenticity or business validity.
