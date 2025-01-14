# Identifier web component design

## Landscape analysis

[Identifier code samples from the landscape analysis](https://docs.google.com/document/d/1umaVv9KFNHhO1L1MQ-25ttTERxC6dlD-qrZd5vfptYE/edit?tab=t.0#heading=h.fa3sv1ray42g) (Google docs :lock:)

## Proposed component structure

### Critical content

None. Proposing that none of the content inside the identifier meets the criteria for critical content.

### Light DOM

Sample default implementation:

```html
<usa-identifier
  domainName="domain.gov"
  parentAgencyLogo="https://designsystem.digital.gov/assets/img/circle-gray-20.svg"
  parentAgencyUrl="javascipt:void(0)"
  parentAgencyName="[Parent agency]"
  parentAgencyShortname="[AAA]"
  aboutURL="javascipt:void(0)"
  accessibilityURL="javascipt:void(0)"
  foiaURL="javascipt:void(0)"
  noFearURL="javascipt:void(0)"
  oigURL="javascipt:void(0)"
  performanceURL="javascipt:void(0)"
  privacyURL="javascipt:void(0)"
>
</usa-identifier>
```

Default Spanish implementation:

```html
<usa-identifier
  lang="es"
  domainName="domain.gov"
  parentAgencyLogo="https://designsystem.digital.gov/assets/img/circle-gray-20.svg"
  parentAgencyUrl="javascipt:void(0)"
  parentAgencyName="[Parent agency]"
  parentAgencyShortname="[AAA]"
  aboutURL="javascipt:void(0)"
  accessibilityURL="javascipt:void(0)"
  foiaURL="javascipt:void(0)"
  noFearURL="javascipt:void(0)"
  oigURL="javascipt:void(0)"
  performanceURL="javascipt:void(0)"
  privacyURL="javascipt:void(0)"
>
</usa-identifier>
```

Sample complex implementation with custom language strings (French) and multiple logos:

```html
<usa-identifier
  label="Identifiant de l'agence"
  disclaimerText="Un site officiel du"
  disclaimerConjunctionText="et"
  taxpayerDisclaimer=true
  taxpayerText="Produit et publié aux frais des contribuables."
  ariaLabel="Identifiant de l'agence"
  domainName="domain.gov"
  parentAgencyLogo="https://designsystem.digital.gov/assets/img/circle-gray-20.svg"
  parentAgencyUrl="javascipt:void(0)"
  parentAgencyName="[Parent agency]"
  parentAgencyShortname="[AAA]"
  secondaryParentAgencyLogo="https://designsystem.digital.gov/assets/img/circle-gray-20.svg"
  secondaryParentAgencyUrl="javascipt:void(0)"
  secondaryParentAgencyName="[Parent agency]"
  aboutURL="javascipt:void(0)"
  aboutText="À propos"
  accessibilityURL="javascipt:void(0)"
  accessibilityText="Déclaration d'accessibilité"
  foiaURL="javascipt:void(0)"
  foiaText="Solicitud a través de FOIA"
  noFearURL="javascipt:void(0)"
  noFearText="Datos de la ley No FEAR"
  oigURL="javascipt:void(0)"
  oigText="Bureau de l'Inspecteur général"
  performanceURL="javascipt:void(0)"
  performanceText="Rapports de performances"
  privacyURL="javascipt:void(0)"
  privacyText="Politique de confidentialité"
  usagovText="Vous recherchez des informations et des services du gouvernement américain?"
  usagovLinkText="Visitez usa.gov"
  usagovUrl="https://www.usa.gov/"
>
</usa-identifier>
```

### Shadow DOM

_Same as USWDS 3, with some proposed tweaks:_

- Replace the wrapping `.usa-identifier` `<div>` with a `<section>`
    - This makes it a landmark region which should improve accessibility
- Use only one aria-label for the component  - remove aria-labels from nested sections

```html
<section class="usa-identifier" aria-label="Agency identifier">
  <section class="usa-identifier__section usa-identifier__section--masthead">
    <div class="usa-identifier__container">
      <div class="usa-identifier__logos" part="logo-wrapper">
        <a href="javascipt:void(0)" class="usa-identifier__logo" part="logo">
          <img src="https://designsystem.digital.gov/assets/img/circle-gray-20.svg" alt="[Parent agency] logo" class="usa-identifier__logo-img" part="logo-image">
        </a>
      </div>
      <section class="usa-identifier__identity">
        <p slot="domain" class="usa-identifier__identity-domain" part="domain">[domain.gov]</p>
        <p class="usa-identifier__identity-disclaimer" part="disclaimer">
          An official website of the <a agency-shortname="[Agency shortname]" href="javascipt:void(0)" part="disclaimer-link">[Parent agency]</a>
        </p>
      </section>
    </div>
  </section>

  <nav class="usa-identifier__section usa-identifier__section--required-links">
    <div class="usa-identifier__container">
      <ul class="usa-identifier__required-links-list">
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">About [Agency shortname]</a>
        </li>
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">Accessibility statement</a>
        </li>
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">FOIA requests</a>
        </li>
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">No FEAR Act data</a>
        </li>
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">Office of the Inspector General</a>
        </li>
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">Performance reports</a>
        </li>
        <li class="usa-identifier__required-links-item">
          <a class="usa-identifier__required-link usa-link" part="required-link" href="javascipt:void(0)">Privacy policy</a>
        </li>
      </ul>
    </div>
  </nav>
  <section class="usa-identifier__section usa-identifier__section--usagov">
    <div class="usa-identifier__container">
      <p class="usa-identifier__usagov-description" part="usagov">
        Looking for U.S. government information and services?
        <a class="usa-link" href="https://www.usa.gov/">Visit USA.gov</a>
      </p>
    </div>
  </section>
</section>
```

### Variants

#### Current variants
| USWDS 3 variant | Description | Defined via |
|--------|--------|--------|
| Default | | |
| Multiple parents and logos | Allows the user to name two parent agencies and two logos | `secondaryParentAgencyLogo`, `secondaryParentAgencyUrl`, `secondaryParentAgencyName` |
| No logos | Aligns content when there is no parent agency logo | Undefined/empty value for `parentAgencyLogo` |
| Taxpayer disclaimer | Adds "Produced and published at taxpayer expense" copy | `taxpayerDisclaimer: true` |
| Spanish (all variants) | Translates content for all variants into Spanish | `lang="es"` |

#### Proposed additional variants
For ease of implementation and consistency across sites, I recommend that we offer additional pre-built translations for commonly used languages. Then the user would just need to set the single `lang` attribute to automatically receive approved translations for this component. 

### Props

#### Current variants
| Property | Type | Description | Required? |
|--------|--------|--------|--------|
| `lang` | string | Set the language for the default component text. Expected values: "en", "es". Default value is "en". | No |
| `label` | string | Set a custom aria label for the identifier component. Default values: "Agency identifier" for English translations, "Descripción de la agencia" for Spanish translations | No | 
| `disclaimerText` | string | Custom text for the "official website" intro text. Default values: "An official website of the" for English translations, "Un sitio web oficial de" for Spanish translations. | No |
| `disclaimerConjunctionText` | string | Custom text for the conjunction in the "official website" intro text when there are multiple parent agencies. Default values: "and" for English translations: "y" for Spanish translations. | No |
| `taxpayerDisclaimer` | boolean | Include the taxpayer disclaimer.  A custom value can be set with `taxpayerText` attribute. | No |
| `taxpayerText` | string | Set a custom value for the taxpayer disclaimer text. Default values: "Produced and published at taxpayer expense.", "Producido y publicado con dinero de los contribuyentes de impuestos." for Spanish translations | No |
| `domainName` | string | Domain name for the website | Yes |
| `parentAgencyLogo` | string | The url for the parent agency logo image | No |
| `parentAgencyUrl` | string | The url for the parent agency's home page | Yes |
| `parentAgencyName` | string | The full name of the parent agency | Yes |
| `parentAgencyShortname` | string | The shortname or acronym of the parent agency. This will be added to the "About [Agency shortname]" link text. | No |
| `secondaryParentAgencyLogo` | string | The url for the secondary parent agency logo image | No |
| `secondaryParentAgencyUrl` | string | The url for the secondary parent agency's home page | No |
| `secondaryParentAgencyName` | string | The full name of the secondary parent agency | No |
| `aboutURL` | string | The url for the parent agency's "About" page | Yes |
| `aboutText` | string | Custom text for the "About" link. Default values: "About [Agency shortname or agency name] for English translations, "Acerca de [Agency shortname or agency name]" for Spanish translations. | No |
| `accessibilityURL` | string | The url for the parent agency's "Accesibility statement" page | Yes |
| `accessibilityText` | string | Custom text for the "Accessibility statement" link. Default values: "Accessibility statement" for English translations: "Declaración de accesibilidad" for Spanish translations. | No |
| `foiaURL` | string | The url for the parent agency's "FOIA requests" page | Yes |
| `foiaText` | string | Custom text for the "FOIA requests" link. Default values: "FOIA requests" for English translations, "Solicitud a través de FOIA" for Spanish translations. | No |
| `noFearURL` | string | The url for the parent agency's "No FEAR Act data" page | Yes |
| `noFearText` | string | Custom text for the  "No FEAR Act data" link. Default values: "No FEAR Act data" for English translations, "Datos de la ley No FEAR" for Spanish translations. | No |
| `oigURL` | string | The url for the parent agency's "Office of the inspector general" page | Yes |
| `oigText` | string | Custom text for the  "Office of the inspector general" link. Default values: "Office of the inspector general" for English translations, "Oficina del Inspector General" for Spanish translations. | No |
| `performanceURL` | string | The url for the parent agency's "Performance reports" page | Yes |
| `performanceText` | string | Custom text for the  "Performance reports"  link. Default values:  "Performance reports" for English translations, "Informes de desempeño" for Spanish translations. | No |
| `privacyURL` | string | The url for the parent agency's "Privacy policy" page | Yes |
| `privacyText` | string | Custom text for the "Privacy policy"  link. Default values: "Privacy policy" for English translations, "Política de privacidad" for Spanish translations. | No |
| `usagovText` | string | Custom text for the usa gov intro. Default values: "Looking for U.S. government information and services?" for English translations, "¿Necesita información y servicios del Gobierno?" for Spanish translations. | No |
| `usagovLinkText` | string | Custom text for "Visit USA.gov" link. Default values: "Visit USA.gov" for English translations, "Visite USAGov en Español" for Spanish translations. | No |
| `usagovUrl` | string | Custom url for usa.gov. Default values: "https://www.usa.gov/` for English translations, "https://www.usa.gov/es/" for Spanish Translations.   | No |

#### Proposed additional variants

Proposing that we build in additional translations for component content. 

### Slots

N/A

### CSS Parts

| Part name | Element |
|--------|--------|
| `base` | Component wrapper |
| `disclaimer` | The `<p>` element that wraps the "An official website of the..." disclaimer text |
| `disclaimer-link` | The `<a>` element inside the disclaimer text |
| `domain` | The `<p>` element that wraps your site's domain name |
| `logo-image` | The agency logo `<img>` element |
| `logo-wrapper` | The `<div>` element that wraps all logos |
| `logo` | The `<a>` elements that wrap each logo |
| `required-link` | The `<a>` elements in the required links list |
| `usagov` | The `<p>` element that wraps the USA.gov text |
| `usagov-link` | The `<a>` element inside the usagov text |

### CSS Variables

#### Current settings

| USWDS 3 setting | CSS custom property | Description |
|--------|--------|--------|
| `$theme-identifier-background-color` | `--usa-theme-identifier-background-color` | The background color of the identifier. ~Use a color of grade 80 or higher, darker than the section that precedes it.~ |
| `$theme-identifier-font-family` | `--usa-theme-identifier-font-family` | The font family of the identifier. |
| `$theme-identifier-identity-domain-color` | -- | The color of your domain text in the identifier masthead. This should be grade 20-30 in the same family as the $theme-identifier-background-color.|
| `$theme-identifier-max-width` | `--usa-theme-identifier-max-width` | The maximum width of the content within the identifier. Use the same max-width as your site footer. |
| `$theme-identifier-primary-link-color` | -- | The color of the links in the masthead section. Default uses either the standard or reverse link color set with `$theme-link-color` and `$theme-link-reverse-color`. |
| `$theme-identifier-secondary-link-color` |  `--usa-theme-identifier-link-list-color` | The color of the links in the required links section. ~This should be grade 20-30 in a gray family.~ |

#### Proposed additional setting

| USWDS 3 setting | CSS custom property | Description |
|--------|--------|--------|
| -- | `--usa-theme-identifier-text-color` | Text color used in the disclaimer and USA.gov statement |
| -- | `--usa-theme-identifier-secondary-text-color` | Link color used in the disclaimer and USA.gov statement |
