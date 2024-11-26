# Text input web component design

## Landscape analysis
[Text input code samples from the landscape analysis](https://docs.google.com/document/d/196iN8pSayb-vMNAupD_1hrnzKeHgHCI9P4xSqK2b-tE/edit#heading=h.fa3sv1ray42g) (Google docs :lock:)

## Proposed component structure

### Critical content
The `<input>` and `<label>` elements contain critical content that should always be included on the page, even in non-JS environments. For this reason, users should be expected to add a complete, accessible input component inside of the custom element tags:

| Element | Required attributes | Content |
|--------|--------|--------|
| `<input>` | `id`, `name` | N/A |
| `<label>` | `for` (Note: The `for` attribute should match the `id` of the related `input` element) | Informational label text |

> [!note]
> This solution deviates from the implementations we saw [across the landscape](https://docs.google.com/document/d/196iN8pSayb-vMNAupD_1hrnzKeHgHCI9P4xSqK2b-tE/edit#heading=h.fa3sv1ray42g). Almost universally, the other design systems in our sample pool opted to build a fully prop-driven component. We decided to go a different path so that the page builds a fully functional and accessible component, even when JavaScript fails or is slow.
>
> More information: [Conversation about opting for progressive enhancement for text input](https://docs.google.com/document/d/1Wqy29Ujm9xPlDq-VE_uiZs_JBMNgdlkNbIBLpXH9270/edit#heading=h.f4t562n12qjg) (Google docs :lock:)
### Light DOM

Sample default implementation:
```html
<usa-text-input>
    <label for="input-type-text">Text input label</label>
    <input id="input-type-text" name="input-type-text" />
</usa-text-input>
```

Sample complex variant implementation:
```html
<usa-text-input state="error" width="lg">
    <label for="input-type-text">Text input label</label>
    <div class="usa-hint" id="inputHint">Hint text</div>
    <input type="tel" id="input-type-text" name="input-type-text" ariadescribedby="inputHint" />
</usa-text-input>
```

### Shadow DOM
_Same as [USWDS 3](https://federalist-3b6ba08e-0df4-44c9-ac73-6fc193b0e19c.sites.pages.cloud.gov/preview/uswds/uswds/develop/?path=/story/components-form-inputs-text-input--input)_

```html
<label for="input-type-text" class="usa-label">Text input label</label>
<input id="input-type-text" name="input-type-text" class="usa-input">
```

### Variants

#### Current variants
| USWDS 3 variant | Web components variant | Description | Defined via |
|--------|--------|--------|--------|
| Error state | Error state | Styles for the error state | `state` prop |
| Success state | Success state |  Styles for the success state | `state` prop |
| Disabled state | Disabled state |  Styles for the disabled state | `state` prop |
| aria-disabled state | aria-disabled state |  Styles for the aria-disabled state | `state` prop |
| Focused state | Focused state  |  Styles for the focused state | `state` prop |
| Input width | Width | Set the width of the input | `width` prop |

#### Proposed additional variants
| USWDS 3 variant | Web components variant | Description | Defined via |
|:--------:|--------|--------|--------|
| -- | Prefix | Add custom text or icon to the input prefix  | `prefix` or `prefix-icon` prop |
| -- | Suffix | Add custom text or icon to the input suffix | `suffix` or `suffix-icon` prop |
| -- | Required | Add indicator that field is required| `required` prop |

> [!note]
> Textarea is currently bundled with the text input in USWDS 3. Because its html structure requires the `<textarea>` tag instead of the `<input>` tag, I propose that we create a separate custom element for `<usa-textarea>`.

> [!note]
> We could consider including some custom styles for common text input types, like `tel`, `email`, etc. I imagine we could add an icon prefix for these types when appropriate. However, this might be too opinionated and we can instead let users choose to add a prefix with the `prefix-icon` prop.

### Props

#### Current variants
| Property | Description | Expected values
|--------|--------|--------|
| `state` | Sets the state of the component | `error`, `success`, `disabled`, `focus` (?) |
| `width` |  Set the width of the input element and label | `2xs`, `xs`, `sm`, `small`, `md`, `medium`, `lg`, `xl`, 2xl`  |

#### Proposed additional variants
| Property | Description | Expected values
|--------|--------|--------|
| `prefix` |  Add content for an input prefix | `string` |
| `prefix-icon` |  Add icon for an input prefix | Name of icon |
| `suffix` |  Add content for an input suffix | `string` |
| `suffix-icon` |  Add content for an input suffix | Name of icon |
| `required` | Add indicator for required field | `boolean` |

### Slots
Unnamed slot

### CSS Parts
| Part name | Element |
|--------|--------|
| `input` | `<input>` |
| `label` | `<label>` |

### CSS Variables

#### Current settings
| USWDS 3 setting | CSS custom property | Description |
|--------|--------|--------|
| `$theme-input-line-height` | `--theme-input-line-height` | Line-height of input element |
| `$theme-input-max-width` | `--theme-input-max-width` | Max width of the input element |
| `$theme-input-state-border-width` | `--theme-input-state-border-width` | Border width of special state inputs (like error state) |

#### Proposed additional setting
| USWDS 3 setting | CSS custom property | Description |
|--------|--------|--------|
| -- | `--theme-input-state-border-negative-margin` | Size of the negative margin between the left border and input elements |
| -- | `--theme-form-disabled-background-color` | The background color of disabled form elements |
| -- |  `--theme-form-disabled-text-color` | The text color of disabled form elements |

### Translatable content
N/A