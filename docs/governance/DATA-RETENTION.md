# Data Retention

Retention is policy/configuration driven and must satisfy legal, contractual and business requirements for each deployment.

Define separate retention for:
- original documents;
- derived text/OCR;
- extracted structured data;
- evidence crops/regions;
- temporary processing files;
- review history;
- audit/security logs;
- dataset candidates and approved corpora;
- backups.

Deletion must account for derived copies and indexes, not only the original object. Legal hold or audit obligations may override normal deletion only through an explicit authorized process.

Do not set universal retention periods in core code. Store policy/version provenance so the system can explain which retention rule applied.