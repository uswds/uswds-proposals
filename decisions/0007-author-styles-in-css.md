<!--
The record number and the title should be in the filename.
For example:
/decisions/0000-adr-title.md
-->

<!--
PR Title:
ADR Proposal: A brief description
-->

# 7. Author Styles in CSS

| Date       | Status   |
| ---------- | -------- |
| 2025-08-26 | Approved |

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

USWDS styles have historically been authored in Sass/SCSS and processed into vanilla CSS. This preprocessing step occurs either in a build pipeline configured by the user, such as a webpack or vite process that runs the sass executable, or using USWDS Compile, which is essentially just a set of Gulp configs optimized for processing USWDS assets. Users who don't run the build process themselves, and download the pre-built version of USWDS as a zip file, are still using styles authored originally in Sass, and compiled with Gulp as a part of the USWDS release process. 

Over time, the Sass that constitutes the bulk of the USWDS codebase has gotten complicated, and can be difficult to reason about. This presents challenges for the ongoing development and maintenance of the project and is one of the main sources of support requests.

At the same time, the state of the art in CSS has made epochal advances. CSS custom properties ("CSS Variables", colloquially) are widely supported in modern browsers, as are other key features such as `calc` functions and CSS Grid. As the web platform has moved forward, it has obviated some of the need for preprocessors like Sass.

## Decision

The USWDS team will author styles in CSS.

### Alternatives

The main alternative to this decision is to continue authoring styles in Sass. The relative merits of CSS vs. Sass are covered in the Consequences section below.

<!--
Options considered (with benefits and risks/mitigations), assumptions, choice made, and reasoning.
-->

## Consequences

### Benefits

1. A USWDS without Sass will make the project simpler to develop, maintain, and support. As a side benefit, authoring styles directly in CSS will allow the team to deprecate USWDS Compile, which is itself a source of numerous support requests as well as stubborn vulnerability warnings via `npm audit`.
2. Leveraging custom properties instead of Sass variables will introduce more power and flexibility into USWDS. One major advantage custom properties have over Sass variables is that they can be changed at runtime. Because the 3.x theme system is based on Sass, it depends on a set of variables in various configuration files that can only be read at build time. A theme leveraging custom properties can be tweaked programatically at runtime by JavaScript.
3. Custom properties are an important part of the styling story for web components. Because custom property values [ipropagate through shadown DOM](https://webcomponents.guide/learn/components/styling/#inheritance) unlike other CSS properties, they can be part of the API surface for USWDS web components.
4. Authoring styles directly in CSS rather than Sass accords with the [USWDS engineering values](https://github.com/uswds/uswds-proposals/blob/main/docs/engineering-values). In particular, using CSS hews closely to the web platform.

### Risks

1. USWDS leverages some Sass features that do not have CSS analogs. The most salient omission is the lack of custom property support in media queries. This makes it difficult or even impossible to specify custom breakpoints in the way the current design system implements them. There are workarounds for this that involve post-processors, like PostCSS or Lightning, but there are also more modern layout techniques that can reduce the importance of media queries to responsive layouts.
2. More than anything, this change represents a generational change to USWDS and the biggest risk is simply the level of effort involved in porting the existing styles from Sass/SCSS to vanilla CSS.
