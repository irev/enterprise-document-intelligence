# Normative Map

This map prevents guidance/examples from accidentally becoming mandatory architecture.

## Normative foundation

- `SPECIFICATION.md`
- `docs/PRINCIPLES.md` where stated as architecture invariants
- `docs/conformance/*`
- `docs/interoperability/*`
- applicable security/tenant/audit invariants
- applicable ADR constraints

## Machine-readable normative contracts

- `schemas/**`
- `openapi/**` when REST capability is claimed
- `asyncapi/**` when EVENTS capability is claimed

## Reference profiles

- `profiles/**`
- `docs/reference/**`
- `examples/rfp/**`

These specialize or demonstrate the core and do not make RFP/AP a platform requirement.

## Informative implementation guidance

- `docs/implementation/**`
- `docs/architecture/REFERENCE-DEPLOYMENT.md`
- `docs/domain/PERSISTENCE-MODEL.md`
- `docs/providers/CONFORMANCE.md` except requirements explicitly incorporated by a claimed capability/profile
- examples and diagrams unless explicitly marked normative

Implementations MAY use different internal architecture while preserving observable normative behavior.

## Architecture decisions

`docs/adr/**` explains why specification constraints exist. Accepted ADRs govern specification evolution; machine-readable contracts and explicit normative requirements remain the interoperability surface.
