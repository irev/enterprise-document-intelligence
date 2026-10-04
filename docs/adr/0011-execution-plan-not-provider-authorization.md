# ADR 0011: Execution Plans Do Not Confer Provider Authorization

**Status:** Accepted

## Context

Reference implementation work established an important security boundary that was only implicit in the execution-policy specification.

Provider planning and provider invocation occur at different times. Between those operations, trusted control-plane configuration can change: a provider can be disabled, or its tenant/application authorization can be revoked. Treating the earlier plan as sufficient authorization would allow stale authorization state to survive revocation.

This is a platform behavior, not a Python-specific implementation detail.

## Decision

An execution plan records selection and provenance. It MUST NOT be treated as an authorization grant.

Immediately before a planned provider is invoked, the implementation MUST evaluate that provider against current trusted control-plane authorization.

Invocation MUST fail closed before provider code executes when:
- the selected provider is no longer enabled;
- the requesting tenant is no longer authorized for that provider;
- the requesting application is no longer authorized for that provider; or
- the planned provider identity/version, execution class, or capability no longer matches the provider being invoked.

Document content and stale plan data MUST NOT restore, broaden, or override revoked provider authorization.

The exact storage, registry, authorization service, transaction mechanism, or programming language is implementation-defined.

## Consequences

- Provider revocation takes effect at the invocation boundary rather than waiting for plans to expire.
- Plans remain useful for provenance and reproducibility without becoming security credentials.
- Implementations need an invocation-time control-plane authorization check.
- Conformance tests can verify that provider code is not called after authorization has been revoked.
- Lower-level provider adapters remain policy-free and must not decide tenant/application authorization themselves.
