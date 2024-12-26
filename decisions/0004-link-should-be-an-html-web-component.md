# 4. `usa-link` Should be an HTML Web Component

| Date       | Status   |
| ---------- | -------- |
| 2024-12-17 | Accepted |

## Context: What is an "HTML Web Component"?

Custom elements are already "HTML" inasmuch as they inherit from the `HTMLElement` class, but "HTML Web Component" is getting traction as a term of art that refers specifically to a custom element that is architected to surround non-custom-element HTML. Jeremy Keith, who [coined the term](https://adactio.com/journal/20618), describes the distinction between custom elements and HTML Web Components 

>  If your custom element is empty, it’s not an HTML web component. But if you’re using a custom element to extend existing markup, that’s an HTML web component.

As an example, one [early blog post](https://blog.jim-nielsen.com/2023/html-web-components/) explaining the concept of HTML web components illustrates the difference using the example of a user avatar component. A component like this can be a perfectly valid HTML custom element:

```html
<user-avatar
  src="https://example.com/path/to/img.jpg"
  alt="..."
></user-avatar>
```

In this instance, the `<user-avatar>` tag is empty, and the user-supplied content comes in via attributes on that tag. Presumably, the JavaScript code that implements that component imperatively creates shadow DOM markup and applies styles to control how the component renders. However, this component cannot render unless and until that JavaScript loads. In the best case, where the JS loads quickly and runs without error, there will be a brief delay while that code comes over the wire and executes. However, even in this ideal case, the component's user will need to plan ahead for the space that component will take up when it is fully rendered, otherwise there will be some degree of layout shift. Further, in this example where the avatar component is loading an image, the page's author (and of course the end-user) will miss out on the performance benefit of the browser's default behavior to prioritize loading images during the [initial blocking phase of rendering](https://web.dev/articles/fetch-priority) since the browser must run the JS before the browser even knows that there is an image that needs to load.

The solution here, as the post author suggests, is to architect the component to accept a plain HTML `img` element as a child:

```html
<user-avatar>
  <img src="https://example.com/path/to/img.jpg" alt="..." />
</user-avatar>
```

The image loads in its normal priority order, and will appear irrespective of whether the JavaScript loads. When JS does load, any additional behavior or presentational changes will happen at that time. This approach uses the avatar component to progressively enhance the `img` element with whatever else it does.

## Alternatives Considered

One approach to the link component would be to use a custom element that gets some or all of its content and functionality via properties or attributes. This is how `usa-link` is currently implemented (as of the [most recent commit](https://github.com/uswds/web-components/commit/d7f04ca1d6708931f712c6b0e2ae958c2a0fbe76) that touched the link). Usage of the link in its current state looks like:

```html
<usa-link href="https://designsystem.digital.gov">
  It's dangerous to go alone. Here, take this.
</usa-link>
```

The implementation then takes the content of the tag, creates a shadow DOM anchor element (a browser-native `<a>` tag) sets destination to the value of the `usa-link`'s `href` attribute, and copies the text content into a `slot`. Because the text content is right there in the markup, it will appear whether or not the JavaScript loads. However, until JavaScript loads and executes, the text will just be text and not a link. This works, but it may not be an ideal experience for a number of reasons:

1. It makes critical browser-native functionality dependent on JavaScript. The hyperlink is one of the most fundamental building blocks of the web, and it follows that links will be some of the most important content on USWDS users' sites. They should work no matter what.
2. It requires a lot of additional engineering just to leverage native browser functionality. Because the current implementation copies over the `href` attribute as-is into the shadow DOM `<a>` tag, anything the browser does with that attribute comes along for free. That is, the `usa-link` built this way can handle `tel:` or `file://` links (among others). Anything a browser can do with an `href` will work in a `usa-link`. However, other attributes that `<a>` can take will need to be handled separately. This includes all [global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes) that can be used on any element as well as the [9 additional attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attributes) that are specific to the anchor element. 

The current approach takes a piece of built-in web functionality and makes it brittle and error-prone, and requires careful effort to implement.

## Decision

The link component should be implemented as an HTML web component

## Consequences

The current implementation needs to be revised. As we implement more components, we should consider whether the reasoning in this ADR applies to them as well. If it does, we should consider a similar strategy for implementation.
