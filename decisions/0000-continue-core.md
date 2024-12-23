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

We'll continue to develop USWDS Core and move toward semantic versioning — that is, bumping major versions more often.

### Alternatives

We've considered retiring USWDS 3 entirely in favor of USWDS Elements, but decided against for the following reasons:

1. This would be a major migration effort for all developers (including the USWDS core team).
1. Migrating existing USWDS 3 directly to USWDS Elements doesn't make the design system more modular.
1. Users wouldn't be able to fall back to USWDS Core if they need more fine-grained control over components or to build additional functionality.

<!--
Options considered (with benefits and risks/mitigations), assumptions, choice made, and reasoning.
-->

## Consequences

### Benefits

1. Teams can adopt USWDS Elements incrementally, component by component, to get easier updates and avoid costly big-bang migrations.
1. Teams can fall back to traditional HTML, CSS, and JS to support custom components or make considerable customizations.
1. Teams can support additional platforms that might not work well with W3C Web Components.
1. The USWDS Core team can experiment with newer baseline web features more quickly.

### Risks

1. Teams will have more products to track, so we'll have to be clear about documentation and updates.
1. Core team will have more releases to manage, which could affect other work.
1. Core team will have to be careful to avoid duplication and re-work when creating components in USWDS Elements.
1. Core team will have to make all relevant improvements in both USWDS Elements and USWDS Core components.
