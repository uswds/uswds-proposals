<!--
The record number and the title should be in the filename.
For example:
/decisions/0000-adr-title.md
-->

<!--
PR Title:
ADR Proposal: A brief description
-->

# 6. Develop Components in TypeScript

| Date       | Status   |
| ---------- | -------- |
| 2025-07-08 | Approved |

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

Historically, we've written USWDS components in HTML, (S)CSS, and vanilla JavaScript. Even with our recent adoption of Lit and HTML Web Components, we've continued to develop USWDS components in JavaScript. However, much of the industry has adopted TypeScript for component development in order to help catch errors sooner, provide better documentation, and improve integration with modern development tooling.

## Decision

We'll author new components in TypeScript, but continue to deliver them in platform-native ("vanilla") JavaScript.

### Alternatives

The main alternative to this decision is to continue developing components in vanilla JavaScript. However, the benefits to adopting TypeScript outweigh the risks for the following reasons:

1. Given the other changes to our tooling (particularly our adoption of Lit and Vite), the additional overhead from adopting TypeScript is minimal.
2. Continuing to deliver TypeScript-authored components in vanilla JavaScript will let the USWDS team benefit from the improved tooling without passing additional complexity on to design system users.

Another alternative would be to ship components in TypeScript, but this would increase complexity for design system users as well as moving the code we ship further away from the web platform. We've committed to staying closer to the web platform as one of our engineering principles.

<!--
Options considered (with benefits and risks/mitigations), assumptions, choice made, and reasoning.
-->

## Consequences

### Benefits

1. Lit has great TypeScript support, which will help speed up component development.
2. TypeScript catches some potential bugs during development that may otherwise not be discovered until testing or, in the worst case, by users in production. For a small, resource-constrained team, ["shifting left"](https://www.drdobbs.com/shift-left-testing/184404768) in this way will help produce better, more reliable code.
3. Authoring in TypeScript will help us ship better type definitions along with our components, and these will help any users of those components whose tooling can read type information, whether or not they are using TypeScript themselves.

### Risks

1. Developing USWDS components in TypeScript creates a burden to potential contributors who may not be familiar with the language and its tooling.
2. TypeScript includes language features that are not part of JavaScript. The more the project leverages such features, the greater the costs to switch back to vanilla JavaScript become.
