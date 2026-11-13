# JSON Schema Draft 2020-12 Status Record

**Recorded:** 2026-11-12  
**Status of this record:** Corrected verification finding. Working rule applied. Not a locked standard.

## Corrected Status

- **2020-12 is the current published JSON Schema dialect** identified by the official project site (json-schema.org). The specification page states the current version is 2020-12. The meta-schema URI remains `https://json-schema.org/draft/2020-12/schema`.
- A separate IETF standardization effort is underway: `draft-ietf-jsonschema-json-schema-04` (published 14 October 2026). Intended status: Proposed Standard. Current state: Internet-Draft (I-D Exists), WG Document. Expires 17 April 2027. Not an RFC.
- The IETF draft consolidates and revises material from 2020-12. It still references the 2020-12 meta-schema URI as the current default dialect in its text. The JSON Schema TSC has described the draft as based on 2020-12 and is monitoring/participating while treating 2020-12 as the published baseline.

## Distinction

- 2020-12 remains the current published dialect per the official project.
- The 2026 IETF draft is an active working document toward a Proposed Standard. It is not a released replacement for 2020-12.
- Treating the IETF draft as an adopted successor would be incorrect.

## Technical Migration Summary (2020-12 relative to 2019-09)

Unchanged by the status correction. Primary changes:

- Array/tuple: `items` (array form) + `additionalItems` replaced by `prefixItems` + `items` (single schema).
- `$recursiveRef` / `$recursiveAnchor` replaced by `$dynamicRef` / `$dynamicAnchor`.
- Clarification that items satisfying `contains` are considered evaluated for `unevaluatedItems`.
- Format vocabulary split; Unicode regex expectation; Compound Schema Document bundling guidance.

## Residual Unknowns

- Whether or when the IETF draft will reach RFC status, and what final keyword or meta-schema changes will be present if it does.
- Exact degree of future divergence or convergence between the official project’s next published dialect and the IETF track.
- Implementation plans by major validators for the IETF draft while it remains an I-D.

## Methodology Note

This record demonstrates the Operator Pages AI working rule applied to research:

- State the original claim.
- Identify the discrepancy.
- Check authoritative sources.
- Correct the claim without overcorrecting.
- Preserve unresolved questions as unresolved.

Confidence is not evidence. A completion claim is not completion.

PROOF NOT PROMISE.
