# Containers and Document Segmentation

**Class:** Normative

A submitted file is not necessarily one business document.

Examples include a PDF containing invoice + tax invoice + delivery order, email with attachments, archive files, and scans containing multiple documents.

## Terms

- **Source object**: bytes submitted to ingestion.
- **Container**: source capable of containing child objects/documents.
- **Segment**: bounded portion of a source document treated as a candidate logical document.
- **Logical document**: unit classified/extracted under a document profile.

## Requirements

- Implementations MUST NOT assume one uploaded file equals one logical business document when segmentation capability is claimed.
- Segment provenance MUST preserve source identity and page/range mapping.
- Splitting/merging MUST NOT destroy the ability to reconstruct source provenance.
- Classification of a segment MUST NOT silently become classification of the entire source container.

## Encrypted/password-protected input

An implementation MUST surface an explicit unsupported/requires-input/failure state; it MUST NOT report successful extraction from inaccessible content.

## Archives and office containers

Archive expansion, embedded objects and macro-capable documents are security-sensitive optional capabilities. Implementations MUST enforce bounded expansion/resource limits and MUST NOT execute embedded macros/code as part of document understanding.

## Digitally signed documents

Presence of a digital signature is separate from verification. Signature verification, if supported, is an optional capability with explicit result semantics.
