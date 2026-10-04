# Optional API Capability Contracts

**Class:** Normative semantics; transport bindings are optional

The core specification defines operations semantically. REST, RPC and messaging implementations MAY expose equivalent operations differently unless a profile requires a binding.

## DOCUMENT capability

Operations:
- submit document;
- read lifecycle/status;
- read a specific result version;
- request reprocessing.

Reprocessing MUST create a distinct processing run/result version. It MUST NOT overwrite a completed result.

## REVIEW capability

Operations:
- create/read review;
- submit review action;
- detect stale concurrent mutation.

A mutation MUST identify the reviewed result version and expected review version/ETag or equivalent concurrency token.

## BUNDLE capability

Operations:
- create/update a bundle version;
- associate explicit document result versions;
- evaluate bundle requirements/reconciliation;
- read findings/evaluation version.

Updating membership or authoritative context MUST create or identify a new evaluation/bundle version rather than rewrite historical evaluation provenance.

## POLICY capability

Operations:
- identify active policy/ruleset version for a context;
- evaluate supported deterministic policy;
- retrieve evaluation provenance where authorized.

Policy publication/administration is deployment-specific and need not be exposed through the document-processing API.

## Version selection

When multiple completed processing results exist, an API MUST make selection semantics explicit. A consumer MUST be able to request or identify the exact result version it consumed.

## Idempotency

Mutation operations SHOULD support an idempotency mechanism appropriate to the transport. Reusing an idempotency identity with materially different input MUST fail explicitly.

## Authorization

Every operation MUST enforce tenant/resource authorization independent of UI visibility or caller-supplied tenant labels.
