# Conformance Test Matrix

**Class:** Normative test inventory

| ID | Capability | Requirement | Expected result |
|---|---|---|---|
| CORE-001 | CORE | unknown/unsupported input | abstain/UNKNOWN/UNSUPPORTED; no forced known class |
| CORE-002 | CORE | material extraction | value includes required evidence/provenance |
| CORE-003 | CORE | failed/incomplete processing | never represented as successful completed validation |
| CORE-004 | CORE | completed result reprocessing | new version/run; prior completed result preserved |
| CORE-005 | CORE | document prompt injection | content cannot alter control-plane/system policy |
| SEC-001 | CORE | cross-tenant object request | deny without sensitive existence/data disclosure |
| SEC-002 | CORE | malformed/unsafe input | bounded safe failure before privileged downstream action |
| SEC-003 | CORE | planned provider disabled after planning but before invocation | fail closed before provider code executes |
| SEC-004 | CORE | tenant/application provider authorization revoked after planning | fail closed before provider code executes |
| SEC-005 | CORE | planned provider identity/version, execution class, or capability differs at invocation | reject invocation; do not substitute or broaden execution |
| SEC-006 | CORE | final authorization entry removed from a restricted provider scope | access remains denied; empty authorization MUST NOT become unrestricted |
| REV-001 | REVIEW | reviewer correction | machine prediction preserved; correction appended with provenance |
| REV-002 | REVIEW | stale concurrent review | lost update prevented/conflict surfaced |
| BND-001 | BUNDLE | bundle changes | new bundle version/evaluation; historical provenance preserved |
| BND-002 | BUNDLE | cross-document mismatch | stable finding references involved inputs |
| POL-001 | POLICY | policy execution | only supported declarative operators execute |
| POL-002 | POLICY | arbitrary executable content | rejected as policy |
| POL-003 | POLICY | historical evaluation | exact policy/ruleset version recoverable |
| EVT-001 | EVENTS | event emission | envelope validates against claimed event contract |
| EVT-002 | EVENTS | duplicate delivery | duplicate event identity can be recognized |
| DAT-001 | DATASET | production sample | not training eligible by default solely because it exists in production |
| DAT-002 | DATASET | dataset split | declared grouping prevents prohibited leakage across splits |

Executable tests MAY be implemented in any language. The normative assertion is the expected observable behavior, not the test framework.
