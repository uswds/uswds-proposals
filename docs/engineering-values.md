# USWDS engineering values

Our engineering values support our product values and guide us as we make decisions about USWDS. As shared in the [October 2024 USWDS monthly call](https://designsystem.digital.gov/about/monthly-calls/#october-2024-engineering-values).

## Embrace the platform

We favor choices that work with the grain of the web.

**Help the platform do its job**. Use each part of the platform for its intended purpose. HTML should be semantic and tags should describe the content they contain to the largest practicable extent.

**Use progressive enhancement.** HTML web components containing relatively simple markup will enable teams to deliver critical content no matter what. Building components that way will ensure that content is available before JavaScript runs or even if it never does. But it also allows those components to apply all of the design and behavior customizations that CSS and JavaScript allow if and when they become available.

**Avoid lock-in.** Building with the web platform, and using its native idioms, is a way to keep USWDS from being tied to any particular framework. Picking tools that aren't the most popular, but most portable. By keeping our reliance on dependencies as low as possible, we’ll be well-positioned to move on from them if they stop working the way we need them to or if a better alternative comes along. 

**Support open standards.** Every site built with web standard technologies makes the entire web work a little bit better. By preferring open standards over proprietary frameworks, we can support a better, more interoperable web for our users and for the public.  

## Support UX with developer experience

We favor choices that prioritize the end user experience.

**User experience shapes the tools.** We need to make sure that we're building tools that make it easier for developers to build the kinds of sites and services that work for the person using the site or service, wherever they're coming from. 

**Performance matters.** It can be easy to lose track of the performance costs when we're using devices powerful enough to make it easy to build sites and services. But performance can have a real usability impact, a cost impact, and an energy impact. We have to work to keep that impact visible. We have to work to keep performance costs low. 

**Make accessibility easier, not invisible.** It can be amazing and powerful to build accessible decisions into the tools we ship and the components we use. We have to work to make sure that delivering and using accessible tools doesn't result in accessibility disappearing from view. 

**Support repairability.** We want teams to have the ability to repair and improve our work — first for their project, but hopefully also later for an improvement we can incorporate.

## We’re a layer

We favor choices that are thoughtful about our impact. 

**Be a dependency not a fork.** We want to make it easier for teams to add USWDS to their projects in a way that maintains the connection between our work and theirs over time. 

**Our opinions cascade.** We need to be thoughtful about the impact that USWDS has on downstream teams. Recognize that choices made at the Design System level establish the floor for performance and accessibility. Developers should be able to make their own choices about what point they hand control of the page over to scripts.

**Use semantic versioning.** Be clear when things change. Semantic versioning is a kind of contract between developers and users. This contract gives users confidence that the code they’re consuming isn’t going to break anything in their code if they install it - unless the upstream team tells them ahead of time that the update contains a breaking change. USWDS will adopt semantic versioning for the web components package first, and then down the line revisit versioning for other parts of the design system.

**Support different tech stacks.** If USWDS uses only one set of technologies, it may sound great to teams already using those tools, but it imposes significant costs on everyone else. But since we’re all building for the web, the closer we stick to web standard technologies, the easier it will be for every team that wants to use USWDS to do so.

## Write plain-language code

We favor choices that open our code to more contributors. 

**Write for reading.** Recognize that all code we write has to be read by others, as well as by our future selves.

**Embrace the idiom.** Write with the convention of the language. Be cautious about how you introduce new abstractions, idiosyncrasies, or concepts. 

**Documentation first.** Integrate documentation tightly into the development process, and make sure our docs are oriented toward helping developers get things done in their sites and apps. 

**Support other developers.** We use plain language so that others can follow along and contribute.
