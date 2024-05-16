# 1. The Next Version of the Design System will use Web Components

| Date       | Status   |
| ---------- | -------- |
| 2024-05-15 | Accepted |

## Context

Historically, USWDS has provided components written in HTML, (S)CSS, and JavaScript. While the styles and behavior were available in NPM packages, users have to copy component markup and templates from the documentation to integrate it into their sites and applications. This approach has the benefit of simplicity, as it doesn't require a build step or additional tooling. However, it is also error-prone, requiring many steps to be done manually. 

The popularity of JavaScript component libraries and frameworks such as React, Vue, Angular, and Svelte (among many, many others) points toward an alternative way of developing UI components. However, different federal agencies may already be using any of these libraries, or no library at all, and the Design System needs to be able to support all of these users.

[HTML Custom Elements](https://html.spec.whatwg.org/dev/custom-elements.html), commonly and colloquially called "Web Components," are a platform-native alternative to those frameworks and are [broadly supported](https://caniuse.com/custom-elementsv1) in modern browsers. Web Components provide several benefits:

- Modern component-based authoring
- Native support by browser vendors
- Interoperability with other frameworks

## Decision

New components and new versions of existing components will be built with Web Components.

## Consequences

In a sense, moving to native HTML Web Components is a natural extension of the existing design system approach of building on top of web standards. However, it is also a significant departure in at least one important respect: rendering Web Components requires JavaScript. While USWDS has always required JavaScript for important functionality, moving to Web Components takes that requirement further. That move will provide several benefits, but the USWDS team and users of the design system will need to pay careful attention to ensure that sites and applications built with the Design System are accessible to and usable by all members of the public.
