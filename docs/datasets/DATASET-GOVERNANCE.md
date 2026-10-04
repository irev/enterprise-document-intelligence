# Dataset Governance

Possession of a corporate document does not imply permission to train on it.

Record where applicable: provenance, tenant, template family, language, quality, annotation version/status, sensitive-data class, retention class, training eligibility, evaluation eligibility, legal/contractual usage basis and de-identification status.

Separate:
1. production documents;
2. review/correction records;
3. training candidates;
4. approved training corpus;
5. validation set;
6. locked test/gold sets.

Apply least privilege, tenant isolation, encryption, retention/deletion controls and auditable dataset changes. Never commit secrets or confidential production documents here.

Model releases should reference immutable dataset manifests/snapshots plus preprocessing, taxonomy/schema and training configuration versions.