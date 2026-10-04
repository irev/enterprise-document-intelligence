# Dataset Split Policy

Random row-level splits can leak near-identical templates into train/test and inflate metrics.

Use group-aware splits across leakage dimensions such as vendor/issuer, template family, source system, document lineage/duplicates, and time when temporal generalization matters. Duplicates and near-duplicates never cross split boundaries.

Maintain train, validation, locked test and challenge sets.

Challenge cases should include unseen vendors/templates, blurred/rotated scans, mixed languages, missing/extra pages, multi-document PDFs, duplicates, similar-looking classes, handwriting when in scope, and UNKNOWN/OOD inputs.

Report known-template and unseen-template performance separately.