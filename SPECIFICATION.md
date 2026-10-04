# Enterprise Document Intelligence Specification

## Scope

This repository defines technology-neutral behavioral, interoperability, governance, security, and conformance requirements for Enterprise Document Intelligence systems.

It does **not** prescribe a programming language, framework, database, cloud, queue, OCR engine, model provider, deployment topology, or user-interface technology.

## Requirement language

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **RECOMMENDED**, **NOT RECOMMENDED**, **MAY**, and **OPTIONAL**, when written in uppercase, are to be interpreted as described by BCP 14 (RFC 2119 and RFC 8174).

Lowercase uses of these words are descriptive English unless a document explicitly states otherwise.

## Specification classes

Repository content is classified as:

- **Normative** — requirements an implementation is evaluated against.
- **Machine-readable normative** — schemas/API/event/policy contracts used for validation/interoperability.
- **Informative** — explanation, rationale, implementation guidance, examples, and reference architecture.
- **Reference profile** — optional domain/use-case specialization built on the core specification.
- **Architecture decision** — rationale and constraints governing evolution of this specification.

A document SHOULD declare its class when ambiguity is possible.

## Normative core

The normative core includes:
- architecture principles and mandatory boundaries;
- canonical document/result semantics;
- document taxonomy semantics and UNKNOWN/OOD behavior;
- evidence/provenance requirements;
- lifecycle/state semantics;
- tenant isolation and security guarantees;
- review/audit semantics;
- versioning/compatibility requirements;
- conformance requirements.

Machine-readable contracts under `schemas/`, `openapi/`, and `asyncapi/` are normative for the interfaces they describe, subject to their declared version.

## Non-normative implementation freedom

An implementation MAY use any technology stack if it satisfies applicable normative requirements and conformance tests.

Reference architecture, persistence guidance, adapter guidance, examples, and use-case profiles MUST NOT be interpreted as mandatory technology choices.

## Profiles and extensions

A profile MAY strengthen core requirements or define domain-specific fields/policies. A profile MUST NOT weaken core security, evidence, auditability, tenant isolation, or decision-boundary requirements.

Extensions MUST follow `docs/interoperability/EXTENSION-MODEL.md`.

## Conformance

Conformance is based on observable behavior and declared capabilities, not internal architecture or vendor selection. See `docs/conformance/PLATFORM-CONFORMANCE.md`.
