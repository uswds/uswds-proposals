<!--
The record number and the title should be in the filename.
For example:
/decisions/0000-adr-title.md
-->

<!--
PR Title:
ADR Proposal: A brief description
-->

# 0006 Improve modularity in USWDS

| Date       | Status   |
| ---------- | -------- |
| 2024-12-19 | Proposed |

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

USWDS is becoming a set of products, in the form of tools and targets. To improve performance and provide flexibility to teams we should make USWDS more modular by offering products such as:

- USWDS Core (our current HTML/CSS with SASS variables, mixins, functions)
- USWDS Elements (a new HTML Web Components-based version of USWDS Core)
- USWDS Utilities
- USWDS Components
- USWDS Tokens
- USWDS design kit

## Decision

We'll create additional products and resources that teams can use individually, such as: utilities, tokens, SASS helpers, and HTML components.

### Alternatives

Staying on the monolithic repo. This has proven difficult to maintain both centrally and for teams that implement the system, increases dependencies, and doesn't allow us to quickly make changes and ship features.

## Consequences

### Benefits

- This improves reusability for all teams. For example, we can use tokens in both USWDS Core and Elements repo. Other teams will also be able to use tokens for their custom products.
- Increased modularity will improve overall performance and reduce bundle size.
- Teams will be able to prototype quicker with utilities without having to compile SASS.
- This allows teams to choose among these products, or even choose portions within these products, considering the tradeoffs that might come with each. This interchangeability can lead to reduced maintenance time and costs, simplify code dependencies, and/or allow further flexibility.
- Teams will be able to make USWDS product choices that will make their work easier to get started and stay up to date.
- USWDS Core team will be able to test code and manage dependencies more easily.
- USWDS Core team will be able to ship features faster, with less risk of downstream breaks.

### Risks

- Teams may be unsure which products to use, or how to use them together.
- USWDS Core team will have additional overhead maintaining many more products, including documentation and testing.
- USWDS Core team will need to take extra care to make sure there aren't interdependence issues or conflicts with new code.

## Supporting information

- This decision was driven by significant research in 2024.
- A cross-agency working group which includes teams and individuals from VA, SSA, DHS, IRS, and NIH, among others, provided feedback.
