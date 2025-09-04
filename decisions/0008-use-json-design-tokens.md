<!--
PR Title:
ADR Proposal: A brief description
-->

# 8. The Source of Truth for Design Tokens will be JSON

| Date       | Status   |
| ---------- | -------- |
| 2025-09-04 | Approved |

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

When USWDS styles were authored in Sass/SCSS, the tokens were SCSS variables (or more precisely, SCSS variables in conjunction with Sass functions). Since USWDS is no longer authoring styles in Sass/SCSS, a new solution is necessary.

## Decision

The source of truth for USWDS tokens will be JSON formatted according to the W3C DTCG draft specification. 

### Alternatives

The two primary alternatives to this approach would be to use CSS variables directly as the source of truth for tokens or to keep token values in a design tool, such as Figma. The main reasons for choosing JSON as the source of truth over these alternatives are its flexibility and the existence of the draft spec.

<!--
Options considered (with benefits and risks/mitigations), assumptions, choice made, and reasoning.
-->

## Consequences

### Benefits

Using JSON-formatted tokens allows those tokens to be converted into multiple output formats. Because USWDS styles are authored in CSS, the output format of first-resort will be CSS variables. However Sass users can also generate SCSS variables as well to suit their needs. JSON-formatted tokens can also connect to design tools such as Figma, allowing designers and engineers to share the same primitive values across tools.

The existence of a [draft spec](https://www.designtokens.org/tr/drafts/format/) for JSON-formatted tokens also supports this approach. Standards help ensure the consistency and interoperability of this approach which in turn will support its viability in the long term.

### Risks

This approach does require tooling in order to convert the JSON-formatted tokens into CSS, and introducing new tools does carry some degree of risk. However, there is already an industry-standard tool for this process ([Style Dictionary](https://styledictionary.com/)). Further, the standardization effort for this format also lowers the risk of being dependent on any particular tool.

the other main risk here is the level of effort in converting from the existing tokens to the new format. However, as this work can happen in parallel with the work to convert the existing styles from Sass to CSS, the marginal cost of this work is lower.

