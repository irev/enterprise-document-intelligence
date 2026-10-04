# Privacy and Regulatory Control Hooks

**Class:** Normative hooks; legal policy remains deployment-specific

The core specification does not define jurisdiction-specific legal conclusions. It defines the control points an implementation/profile can bind to applicable law, contract and organizational policy.

## Required hooks

Where applicable to the deployment, the system MUST be able to associate governed data with:
- tenant/owner boundary;
- sensitivity classification;
- retention policy/reference;
- processing purpose or policy reference;
- region/residency constraint where required;
- training/evaluation eligibility;
- legal/retention hold state;
- deletion/disposition state.

## Provider eligibility

External model/provider use MUST be gated by deployment policy considering data class, tenant agreement, region/residency, retention/training terms and approved processing purpose.

## Deletion

Deletion workflows MUST account for derived artifacts, indexes, caches and dataset candidates according to applicable retention/hold policy. Audit records MAY require separate retention and SHOULD minimize copied sensitive content.

## Subject/data rights

Where legal or contractual rights apply, implementations SHOULD provide profile-specific mechanisms to locate, export, restrict or delete relevant data without weakening audit/integrity requirements.

This document intentionally does not prescribe GDPR, Indonesian PDP, HIPAA, PCI DSS, or another regime as universally applicable.
