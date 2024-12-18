<!--
The record number and the title should be in the filename.
For example:
/decisions/0000-adr-title.md
-->

<!--
PR Title:
ADR Proposal: A brief description
-->

# 0000 Continue developing USWDS Core

| Date       | Status |
| ---------- | ------ |
| 2024-12-06 | Draft  |

<!--
Status options:
- Draft
- Proposed
- Approved
- Rejected
- Deprecated
- Superseded
-->

## Context

Continuing development of the current HTML/CSS-based version of USWDS, which we're now calling USWDS Core, means teams will be able to rely on the current major version with confidence that they won't need to undertake a big migration as USWDS Elements components are released.

Additionally, continuing support of USWDS Core will then allow the ability to "eject" from potential constraints in USWDS Elements (W3C Web Components-based) components and fall back to traditional HTML and CSS to support completely new components that might not be available or make more customizations in an equivalent USWDS Core component.

## Decision

Options considered (with benefits and risks/mitigations), assumptions, choice made, and reasoning.

## Consequences

Pros and cons of this decision, including potential trade-offs.
