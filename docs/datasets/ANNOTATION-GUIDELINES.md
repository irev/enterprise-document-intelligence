# Annotation Guidelines

A document (or explicitly defined bundle) is the primary annotation unit. Preserve page boundaries and evidence coordinates.

Required metadata: document ID, taxonomy version, family/type/subtype, field ground truth, source/template family where permitted, language, quality attributes, annotator/reviewer ID, annotation status/version.

Lifecycle: `DRAFT -> REVIEWED -> VERIFIED`. Only verified samples enter a gold evaluation set.

Annotators must not guess. Use explicit states: `NOT_PRESENT`, `ILLEGIBLE`, `AMBIGUOUS`, `NOT_APPLICABLE`.

Human production corrections are dataset **candidates**, not automatic ground truth. Prevent target leakage through filenames, folders, metadata or synthetic artifacts unavailable in real production inputs.