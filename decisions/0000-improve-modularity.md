<!--
The record number and the title should be in the filename.
For example:
/decisions/0000-adr-title.md
-->

<!--
PR Title:
ADR Proposal: A brief description
-->

# 0000-adr-title

| Date       | Status |
| ---------- | ------ |
| 2024-12-19 | Draft  |

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

USWDS is becoming a set of tools and targets. To improve performance and allow further flexibility to teams we should make USWDS more modular by offering products such as:

- USWDS Core features (SASS variables, mixins, functions)
- Utilities
- Components
- Tokens

## Decision

We'll create additional resources that teams can use individually, such as: utilities, tokens, SASS helpers, and HTML components.

### Alternatives

Staying on the monolithic repo. This has been proven difficult for maintenance, increases dependencies, and doesn't allow us to quickly make changes and ship features.

## Consequences

### Benefits

- All teams will have improved reusability. For example, we can use tokens in both USWDS Core and Elements repo. Other teams will also be able to use tokens for their custom products.
- Teams will be able to prototype quicker with utilities without having to compile SASS.
- USWDS Core team will be able to test code and manage dependencies more easily.
- USWDS Core team will be able to ship features faster.

### Risks

- Teams may be unsure which products to use.
- USWDS Core team will have additional overhead maintaining many more products, including documentation and testing.
- USWDS Core team will need to take extra care to make sure there aren't interdependence issues or conflicts with new code.
