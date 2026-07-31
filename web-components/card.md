## Landscape analysis

[Card code samples from the landscape analysis](https://docs.google.com/document/d/1QypArbGQk71ChswCjjAPLNKp__D2WWVHuQEo9DUZ_xs/edit?tab=t.0#heading=h.fa3sv1ray42g) (Google docs :lock:)

## Proposed component structure

### Critical content

A card is a container for whatever content the user decides to pass into it. Some examples of elements that we may expect users to pass in based on our current card use cases may include:

| Element | Required attributes | Content |
| --- | --- | --- |
| `img`  | `alt`  | N/A |
| `h1-6` | none | Descriptive and logical heading |
| `p` | none | Text content for card body |
| `a`  | `href` | Descriptive link text for CTA button |

### Light DOM

Sample default implementation:

```html
      <usa-card>
        <div slot="card-header">
          <h2 part="card-heading">Heading</h2>
        </div> 
          <p>
            Text content. Hello world.
          </p>
        </div>
        <div slot="card-footer">
          <a href="#">CTA Button</a>
        </div>
      </usa-card>
```

### Shadow DOM

*Provide a code sample of how the component will be built in the shadow DOM. Provide a default example and a complex example (when applicable).*

```html
<!-- #shadow-root -->
<div class="usa-card">
  <div class="usa-card__container">
		<div class="usa-card__header">
		  <slot name="card-header">
			  <h2>Heading</h2>
		  </slot>
		</div>
		<div class="usa-card__body">
		  <slot part="body"></slot>
		</div>
		<div class="usa-card__footer   ">
		  <slot name="card-footer"></slot>
		</div>
  </div>
</div>
```

### Variants

*In a table, list the current and proposed variants for the component.*

### Current variants

| USWDS 3 variant | Web components variant | Description | Related prop |
| --- | --- | --- | --- |
| Card | (default) | Default card variant with content | -- |
| Card with Media |  | Card with an image at the top. |  |
| Media with header first |  |  | `header-first` |
| Inset media |  |  | `inset` |
| Exdent media |  |  | `exdent` |
| Flag |  | Card with flag layout | `layout` |

### Proposed additional variants

*N/A*

## Props

### Current variants

| Property | Description | Expected values |
| --- | --- | --- |
| `header-first` | When added to the `usa-card` element, the header will display before card media | `boolean` | `true` |
| `inset` | When added to the `usa-card` element, each slotted section of the card will take the inset styles.<br> Alternatively, `inset` can be added to individual slots to only add inset styles to that slot | `boolean` | `true` |
| `exdent` | When added to the `usa-card` element, each slotted section of the card will take the exdent styles.<br> Alternatively, `exdent` can be added to individual slots to only add exdent styles to that slot | `boolean` | `true` |
| `layout`  | When added to the `usa-card` element, users can choose to display flag or flag-alt layouts.<br> Flag will display with media on the left.<br> Flag-alt will display with media on the right. | `flag`, `flag-alt` |

### Proposed additional variants

N/A

### Slots

| Slot | Element | Description |
| --- | --- | --- |
| `generic`  | — | Used to wrap card content <br>Any content not passed to a slot will appear in this generic slot. |
| `card-media` | `img` | Used to wrap card media with `.usa-card__media` markup |
| `card-heading` | `div` | Used as a container for any header content |
| `card-footer` | `div` |  |

### CSS Parts

| Part name | Element |
| --- | --- |
| `body` | `slot` |

## CSS Variables

### Current settings

| USWDS 3 setting | CSS custom property | Description |
| --- | --- | --- |
| `$theme-card-border-color`  | `--usa-theme-card-border-color` | Stroke color of card. |
| `$theme-card-border-radius` | `--usa-theme-card-border-radius` | Border radius of card. |
| `$theme-card-border-width` | `--usa-theme-card-border-width` | Stroke thickness of card. |
|  `$theme-card-gap`  | `--usa-theme-card-gap`  | Gap between cards in a card group. |
|  `$theme-card-flag-min-width`  | `--usa-theme-card-flag-min-width` | Width at which flag cards change to horizontal layout. _Media queries do not currently work with css props_ |
| `$theme-card-flag-image-width` | `--usa-theme-card-flag-image-width` | Fixed image width in the card flag variant. |
|  `$theme-card-font-family`  | `--usa-theme-card-font-family` | Font family for card body. |
| `$theme-card-header-typeset` | `--usa-theme-card-header-font-family` | Family, size, and line height of the heading. |
| `$theme-card-margin-bottom` | `--usa-theme-card-margin-bottom` | Bottom margin for card. |
| `$theme-card-padding-perimeter` | `--usa-theme-card-padding-perimeter` | Padding between card elements and card border. |
|  `$theme-card-padding-y`  | `--usa-theme-card-padding-y:` | Vertical padding between card elements. |

### Proposed additional setting

_N/A_

### Translatable content

All content in the card element will be passed directly by the suer into slots. This should make it easy to be flexible and take provided translations without an issue. Users could potentially also set up their cards to take in data via JSON, so providing translated JSON data would allow for easy content switches.
