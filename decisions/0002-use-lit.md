# 2. Use Lit to build USWDS components

| Date       | Status   |
| ---------- | -------- |
| 2024-05-15 | Proposed |

## Context

New USWDS components will be built using web components. However, the custom element APIs were [largely developed for framework authors](https://daverupert.com/2023/07/why-not-webcomponents/) and may be too low-level to productively use in building out Design System components. As such, it would be helpful to use a library in order to ease the transition to this new technology.

There are several frameworks on offer that leverage the browser custom element APIs, any of which would be a strong choice as a basis for the next version of the design system, but there are two primary choices the team has been evaluating for this purpose:

1. Stencil - Stencil is an all-in-one web framework that supports React-like component authoring. Stencil components are written using JSX and transpiled to native JavaScript web components. Further, Stencil provides custom tooling such as a [test runner](https://stenciljs.com/docs/testing/stencil-testrunner/overview), as well as tools for static site generation and server-side rendering functionality among others. Because it has its own integrated build system, it also makes it easy to incorporate other tools, like Sass/SCSS, with little or no additional configuration. Additionally, some agencies are already using Stencil to build web component implementations of and extensions to the Design System.
2. Lit - As with Stencil, there are existing USWDS-based federal website projects that leverage Lit.

Either would provide a solid foundation for future development, but there are a handful of reasons why Lit may be a better fit at this time. 

1. **Lit is closer to the platform.** Lit provides some syntactic sugar around templating event handling and other complexities, but is otherwise written directly in JavaScript. Because there is no additional transpilation step for Lit, the code you write is the code that runs in the browser. The component author just writes markup and styles directly as HTML and CSS inside template tags in the class that implements a component. This makes troubleshooting and getting help easier as well. Working closer to the browser and the relevant standards simplifies search queries and makes it easier to find relevant documentation. As an example, a search query like `shadow dom styling` will provide more results than `stencil js styling`. Using the platform more directly also makes it easier to bring everything a developer already knows about the web to bear in building components without the additional effort of translating that knowledge into a framework context.
2. **Stencil is a monolith.** Stencil's batteries-included approach is great for teams shipping sites or applications directly to end users. However, Stencil's  bespoke tooling makes it harder to use it with different tools that may be a better fit for particular project needs. For instance, if a separate test runner is a better choice for testing USWDS than the one Stencil provides, it may make sense to decouple the component framework from the testing library. The same argument applies to other parts of the toolchain. Stencil's all-in-one approach may increase velocity up front, but could potentially increase the cost of switching away if it no longer met the project's needs at some point in the future. By contrast, while Lit does provide some tooling support for functionality like SSG/SSR and integration with other frameworks, it is primarily oriented towards creating web components, and leaves additional tasks to purpose-built third party tools. If Lit were no longer a good fit for the project, it should take less effort to adapt our tests, build process, and other tasks to another library.
3. **Lit Components may be more extensible by USWDS users.** Related to (1) and (2), because Lit is closer to vanilla JavaScript code, it is easier for Design System users to take USWDS components and build on top of them without having to buy into Stencil and its ecosystem.

## Decision

USWDS will move forward using Lit

## Consequences

This is not to say that Lit doesn't raise any concerns. In some ways, Stencil's story for SSG/SSR may be better than Lit's. Lit's SSR library remains in "Lit Labs," and its [documentation](https://lit.dev/docs/ssr/overview/) warns of potential breaking changes in the future. However, this appears to be due to the fact that the library was released before Declarative Shadow DOM had full support across the major browsers, so that may be less of a concern at this point. Other tools have adopted `lit-ssr`. For instance, [Astro's Lit integration](https://docs.astro.build/en/guides/integrations-guide/lit/) is based on `lit-ssr`.

However, even if it turns out that another library becomes a better fit at some point in the future, moving forward with Lit will allow USWDS to use it for as long as it is helpful without tightly coupling the components to a particular idiosyncratic implementation.