# ADR-0003: UNKNOWN Is a First-Class Classification Outcome

- Status: Accepted
- Date: 2026-10-04

## Context
A closed-set classifier forced to choose a known type can confidently misclassify unsupported corporate documents.

## Decision
Classification contracts include an explicit UNKNOWN/OOD path. Automation thresholds and review policy are calibrated using representative unknown/novel inputs.

## Consequences
Some documents require manual handling, but the platform avoids converting uncertainty into false certainty and obtains measurable OOD behavior.