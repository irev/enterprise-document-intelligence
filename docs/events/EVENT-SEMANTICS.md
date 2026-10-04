# Event Evolution and Delivery Semantics

**Class:** Normative when EVENTS capability is claimed

## Identity and deduplication

Each event MUST have a globally unique event identity within the producer's contract scope. Redelivery of the same logical event MUST retain the same event identity.

Consumers MUST be able to deduplicate by event identity.

## Ordering

Global ordering is NOT guaranteed by the core specification. If ordering is provided, the implementation/profile MUST declare its ordering key and semantics, such as per document or per bundle.

Consumers MUST NOT infer causal order solely from arrival order.

## Causality

Correlation IDs group related activity. Causation IDs SHOULD identify the direct triggering event/operation where known.

## Delivery

Transport-specific guarantees are deployment-specific. At-least-once delivery is a supported baseline pattern; consumers MUST be idempotent when that pattern is declared.

## Replay

Replayed historical events MUST preserve original event identity and occurrence semantics. Replay transport metadata MAY differ and SHOULD make replay distinguishable operationally without changing business meaning.

## Evolution

Breaking payload/semantic changes require a new event contract version. Additive optional fields are allowed only where consumers are required to tolerate them.

## Data minimization

Events SHOULD carry references and bounded required facts rather than unrestricted document text or sensitive payload copies.
