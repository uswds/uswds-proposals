# Web components pre-alpha documents

This directory is designed to capture decisions about the design and code structure of USWDS Elements, the [upcoming version based on web components](https://github.com/uswds/uswds-proposals/blob/al-pre-alpha-wc/decisions/0001-use-web-components.md). 

These decisions are part of the pre-alpha stage of web component development, which happens before we build out any web component code.

> [!Important]
> Only USWDS core team members can create pre-alpha documents at this time. We will close any pre-alpha pull request that does not come from the USWDS core team. If you'd like to help make the case for a new USWDS web component or have another comment, use the [USWDS discussion board](https://github.com/uswds/uswds/discussions) instead.

## Goals of the pre-alpha phase
- Understand how this component fits into the landscape
- Get consensus on:
  - The markup structure for the light and shadow DOM
  - The component's current and future variants, props, parts, slots, and variables

## How to create a pre-alpha document
1. Create a branch for the web component pre-alpha using the following naming structure: `[component-name]-pre-alpha`
1. Make a copy of the template in the web-components directory and rename it `[component-name].md`
1. Fill out the template with the designated information
2. Open a PR with your new branch
