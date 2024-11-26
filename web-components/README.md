# Summary

This directory is designed to capture decisions about the design and code structure for USWDS web components. This is the pre-alpha stage for the component, which will happen before any development work starts. 

## Goals
- Understand how this component fits into the landscape
- Get consensus on:
  - The markup structure for the light and shadow DOM
  - The component's current and future variants, props, parts, slots, and variables

## How to create a pre-alpha document
1. Create a pre-alpha branch for the web component with the following naming structure: `[component-name]-pre-alpha`
1. Make a copy of the web-components template and rename it `[component-name].md`
1. Fill out the template with the designated information
2. Open a PR with your new branch

## Task list
- [ ] Gather code samples from the landscape
    - Note: Use the [Landscape analysis code samples template](https://docs.google.com/document/d/1xVJeipLr79PvPdZz6Hf0SQDowbJBmQiKrVWUOs6wsLM/edit) to collect relevant code samples from across the landscape
- [ ] Identify and document the component’s  critical content
   - Document the component content that is critical for end-user understanding. Note: This critical content should always appear on the page, even in non-JS environments.
- [ ] Design and document the structure for the light DOM
- [ ] Design and document the structure for the shadow DOM
- [ ] Design and document the expected component customization methods
    - [ ] List and define the proposed component variants
    - [ ] List and define props
    - [ ] List and define slots
    - [ ] List and define CSS Parts
    - [ ] List and define CSS Variables
    - [ ] List any component content that will need to be translated into other languages
