# ADR-0001: AI Prediction Is Not a Business Decision

- Status: Accepted
- Date: 2026-10-04

## Context
Document AI is probabilistic while RFP and corporate workflows can have financial, compliance and audit consequences.

## Decision
AI may classify, extract, normalize, estimate confidence and produce evidence-backed findings. AI output alone must not authorize payment, bypass approval, alter accounting records, or establish privileged business decisions. Those decisions use deterministic business rules/workflow controls and authorized humans where required.

## Consequences
Safer failure modes, testable invariants, independent model upgrades, clearer audit responsibility and cleaner multi-tenant configuration; at the cost of additional integration/rules architecture and retained human review for some workflows.

## Rejected
Embedding customer business policy entirely in prompts/model behavior is rejected because it is difficult to guarantee, version, test and audit.