<!--
PR Title:
ADR Proposal: Migrate Web Component CSS to Native Files with LightningCSS and vite-plugin-lit-css
-->

# 9. Use LightningCSS for Web Component CSS

| Date       | Status   |
| ---------- |----------|
| 2025-10-14 | Approved |

## Context

Previously, the styling for web components in the project was handled through a CSS-in-JS approach where styles were embedded within JavaScript files. This method required the use of a plugin, postcss-lit, to allow stylelint to parse and lint the CSS correctly. However, this setup added complexity both to the build process and to developers' workflow. Moreover, styles had to be written in legacy CSS formats, lacking support for newer, more expressive CSS syntax features such as modern media queries and nested rules. This constrained the ability to take advantage of evolving web platform capabilities.

The desire was to enable writing modern, maintainable CSS while still producing a build output compatible with a broad range of browsers, ensuring progressive enhancement without sacrificing backward compatibility. Simplifying CSS management and embracing modern tooling were therefore key priorities.

## Decision
The project adopted a new approach for styling web components using a native `.css` file with LightningCSS and vite-plugin-lit-css to support the build process and developers' productivity.

### Alternatives

There were two alternative approaches considered for styling web components. The first was to continue using the CSS-in-JS approach with postcss-lit. This approach would have allowed the use of modern CSS features, but would have required additional configuration and tooling to support stylelint and other linting tools, with the added complexity of setting up other plugins in the postcss ecosystem.

The second alternative approach was to keep writing the styles in legacy CSS formats and then migrate to the modern syntax once browser support hit a critical mass. 

## Consequences

### Benefits
- This decision simplifies CSS management by leveraging native `.css` files, allowing styles to be authored in a natural, modern style without embedding them in JavaScript code. 
- It improves developer experience by enabling writing CSS with nesting and modern media queries, which are then automatically transformed to maintain compatibility.
- LightningCSS is shipped with comprehensive defaults and is faster than the postcss approach.

## Tradeoffs
- Migration requires adjusting developer workflows to import native CSS files instead of using CSS-in-JS.
- LightningCSS is not compatible with CSS-in-JS, which precludes hybrid approaches relying on CSS-in-JS for styling.
- Build-time CSS transformation adds a build step dependency that must be maintained.
- Possible minor breakages in styles during transition if media queries or CSS features are not transformed correctly (mitigated by thorough testing and visual regressions).

Overall, this decision simplifies styling for web components, improves performance, and future-proofs the project's CSS strategy, superseding the previous CSS-in-JS approach.
