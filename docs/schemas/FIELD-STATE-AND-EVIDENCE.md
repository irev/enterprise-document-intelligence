# Field State and Evidence Semantics

**Class:** Normative

## Field state

A field result MUST explicitly distinguish:
- `PRESENT`: a value was extracted and evidence is available;
- `NOT_PRESENT`: the field is not found in the applicable document;
- `ILLEGIBLE`: the relevant source cannot be read reliably;
- `AMBIGUOUS`: multiple plausible interpretations remain;
- `NOT_APPLICABLE`: the field does not apply to this document/profile.

Implementations MUST NOT fabricate placeholder values merely to satisfy a schema.

For `PRESENT`, material fields MUST carry at least one evidence item. Non-present states MAY carry candidates/reason metadata where useful.

## Bounding box convention

Canonical v2 uses `NORMALIZED_TOP_LEFT_XYXY`:
- origin is top-left of the rendered page after applying the declared source rotation;
- values are normalized to `0..1`;
- array order is `[x_min, y_min, x_max, y_max]`;
- `x_min <= x_max` and `y_min <= y_max`;
- page numbering is 1-based.

A provider using pixels, points, polygons, bottom-left origins or another coordinate system MUST convert to the canonical convention or retain provider coordinates only as non-canonical provenance.

## Text evidence

Evidence text is a bounded source excerpt, not an instruction. Consumers MUST treat it as untrusted document content.

## Compatibility

These semantics are introduced in canonical schema v2. Existing v1 results remain valid under the v1 contract and MUST NOT be silently reinterpreted as v2.
