# Tabs proposal

## 1. About this component

### 1.1 Component name

Tabs

### 1.2 Description

Tabs are a common way to allow users to alternate between groups of content within the same page.

### 1.3 Design system need

#### What key functionality does this component support?

Tabs allow users to progressively show and hide digestible sections of related content while staying in place on a page.

#### What gap does this fill in the Design System?

USWDS currently offers an accordion component, which also gives users the ability to show and hide groups of content. However tabs would address the following gaps not covered by the accordion:

- **Tabs allow for horizontal grouping of information.** While the accordion offers vertical grouping of content that allows more than one group of content to be opened at once, a tabs component can offer horizontal grouping.
- **Tabs allow users to stay in place while navigating sections of content.** Unlike accordion, tabs offer users the ability to stay fully in place while alternating between two or more groups of related content.
- **Tabs are familiar.** User familiarity and expectations of a tab functionality is not present within any other component.

#### What problem does this component solve?

Tabs are a very common and familiar user pattern that are used on a range of existing digital experiences. Jakob’s Law of UX states: “Users spend most of their time on other sites. This means that users prefer your site to work the same way as all the other sites they already know.” Offering a USWDS tabs component would provide the following benefits:

- **Providing a common tabs component will save time and money across projects.** By providing a readily available tabs component within the USWDS, builders will no longer need to spend time to seek out third-party open-source design system components that will fulfill their user needs and expectations. Additionally, an available tabs component will eliminate the costs accrued to design, develop, test, and implement a custom component. [Need to validate that federal agencies are pursuing tabs components]
- **USWDS can provide guidance for this common pattern.** Additionally, USWDS will be able to provide guidance on when builders should use tabs, when to consider something else, and additional support by including a component overview page as seen with other components within the library. To help facilitate the introduction of this tabs component, we have included a draft of what may be included in a tabs overview page in this proposal. (See [Tabs – Component overview.jpg.zip](https://github.com/uswds/uswds/files/8861616/Tabs.Component.overview.jpg.zip_)). The details are also added to the sections below.

### 1.4 Component design

#### 1.4.1 Core functionality

- The tabs component toggles visibility of content in a display frame
- Tabs should contain at least two items
- Tabs open on the same page
- Only one tab can be opened at a time
- Tabs should be navigable by click, keyboard, and voice command
- The active tab should be clearly indicated (both visually and in assistive technologies)
- The tabs content should all be visible at narrow screen widths

#### 1.4.2 Interactive states

The tab-style CSS class has three states:

1. **Unselected/Inactive:** The state a tab displays when it is not selected, or showing content.
  ```
  .tab-style {
    @include u-text("base", "!important");
    background-color: transparent !important;
  }
  ```
1. **Selected/Active:** The state displayed after a user has clicked or tapped a tab which displays only the content belonging to the tab selected.
  ```
  .tab-style-active {
    @include u-text("base", "!important");
      background-color: transparent !important;
      border-bottom: 3px solid color("base-dark") !important;
  }
  ```
1. **Hover:** Displayed when a user is hovering over the selection area.
  ```
  .tab-style:hover {
    @include u-text("base-dark", "!important");
    background-color: transparent !important;
  }
  ```

#### 1.4.3 Possible variants

- Scrollable
- Tabs to the side
- Tabs on top

#### 1.4.4 Demonstration

The Government Transformation Team (GTT) at Amazon Web Services (AWS) uses USWDS as the principal design system in our open-source application, [Performance Dashboard on AWS](https://aws.amazon.com/solutions/implementations/performance-dashboard-on-aws/). In lieu of a tabs component included within USWDS, we have designed and developed a tabs component by embracing the inclusive design principles and visual guidance from USWDS to meet the needs and expectations of our public sector customers.

We provide the design of our tabs component; including code, a working demo environment, and research that supports the validity of its design.

The constructed design file can be found in the following file: [Tabs – Design Demo.fig.zip](https://github.com/uswds/uswds/files/8861618/Tabs.Design.Demo.fig.zip).

To preview the proposed tabs component live in any browser, visit: [https://demo.badger.wwps.aws.dev/fire-safety-and-emergency-medical-services](https://demo.badger.wwps.aws.dev/fire-safety-and-emergency-medical-services).

##### Accessibility note:
Flows that use our tab component were audited and accessed against WCAG 2.1 guidelines. These audits identified accessibility barriers for users with cognitive disabilities, low vision users, and keyboard only users. The results of these tests have concluded the application and tabs component to be WCAG 2.1 compliant.

Our demo environment now reflects all accessibility enhancements and has been independently certified as WCAG 2.1 AA conforming via LevelAccess.

Accessible design included in component:
- Tabbing to highlight active state
- Aria-label for screen reader to indicate each tab is a ‘tab panel’, and its name
- Aria-label indicates if currently selected is the ‘active tab panel’
- Keyboard interaction: Pressing Enter select the active, highlighted tab panel
- Arrow key tab functionality
- Hover state used as a signifier

##### Tests and supporting evidence

- Accessibility tests conducted by both an internal and external accessibility team (AWS & Digital Accessibility Centre, respectively) gave us advise on how to design the component to be more accessible to our users. In both instances, flows involving the use of our tabs component were given to users for specific task completion. Those who completed these tasks included people with cognitive disabilities, people with visual impairments, people who use voice activation, and people who only use a keyboard to navigate. Our WCAG level goal is [AAA]. Currently, we recognize our tabs as being WCAG [AA] compliant.
- Our accessibility audits indicated that our initial use of semantic HTML provided an inconsistent experience when addressing accessibility needs of some users. For low-vision users who require a zoom up to 400%, some tabs would appear off-screen even at large viewports, rendering the component unusable. To address this, we implemented a horizontal scroll and ultimately wrapped tab items in divs top to bottom to provide an experience that was more consistent than what we were able to achieve using list items within lists.

  We recognize the trade-off. Using semantic HTML provides predictable use for many users, and can tell them what is in the list – but has inconsistencies when being able to scroll horizontally. We can foresee a tabs component with a horizontal scroll tab list with a more predictable semantic markup to close the gap on the accessibility trade-off while addressing the needs for all of our users.

##### Sample component code

```html
<div
  role="tab"
  class="tab-style display-inline-block padding-x-2 padding-y-105
         text-bold font-sans-md"
  tabindex="0"
  aria-label="Active Section Tab label"
  style="cursor: pointer; white-space: nowrap;"
>
  Tab label
</div>
```

### 1.5 Implementation examples

- [GOV.UK design system tabs component](https://design-system.service.gov.uk/components/tabs/)
- [State.gov home page](https://www.state.gov/)
- [Login.gov sign-in page](https://secure.login.gov/)


### 1.6 Related USWDS components

N/A

### 1.7 Key audiences

N/A

## 2. Usage

### 2.1 When to use this component

- **If you want to group together two or more sections of related information.**
- **If your users would benefit from digesting smaller amounts of information at a time.**
- **If your sections are content-driven.** In general, tabs should be paired with content-driven components like text, images, or data visualizations.

### 2.2 When to consider a different component

- **If you are organizing a large amount of unrelated content.**
- **If your content is highly interactive.** It is not recommended to place other highly interactive components within a tab, or components that are task-driven like forms, data entry, or page-level alerts.
- **If your content is nested.** Avoid combining tabs with other components that nest content.  For instance, adding an accordion inside of a tab’s content should be avoided.
- **If you need site navigation.** Avoid using tabs as navigation to other pages. The purpose of tabs is to allow viewing related content without leaving the current page. Instead, use the header component.
- **If more than three tabs are needed.** Consider using an accordion when more than a few tabs will be required. This eliminates the need for horizontal scrolling, which can lead to a poor experience for uses of assistive technologies.
- **If you need more than one group of hidden content on a page.** In this scenario, consider the accordion component instead.
- **If you need to show more than one section at a time.** Instead, use the accordion component.
- **If your section labels require long strings of text.** Accordions are a better choice if you want to include a lot of text in your section label (Think: FAQs).

## 3. Usability and accessibility

### 3.1 Usability considerations

#### Usability guidance

- **Be strategic when grouping content.** Only use tabs that are similar when it comes to the meaning of the page.
- **Limit label text to a few words.** Tab labels should allude to content nested within tab as concisely as possible.
- **Allow the entire tab area to be selectable.** Allow users to click or tap anywhere in the label area to open a tab and view its content.
- **Enable horizontal scrolling.** This allows content to be accessible in limited horizontal viewports. [Need source/research]
- **Use similar punctuation between each tab.** [Need source/research]
- **Do not use favicon or icons in tabs.** [Need source/research]
- **Do not use all caps for tabs labels.** Using caps will shorten your available horizontal space and will demand too much attention from the user. [Need source/research]
- **Place tabs at the top of the module or element where the content is being grouped.** Fix to the top of the viewport as necessary. [Need source/research]
- **If the number of content items inside a tab is relevant, indicate the number with parentheses.** If tabs are being used to display content that is grouped into numerical data sets, it may be helpful to indicate to the user the number of data sets within each tab. [Need source/research]
- **Limit grouping to seven tabs in a single element.** Using a long grouping of tabs requires significant horizontal scrolling in a smaller viewport, and increases cognitive load for users. [Need source/research]
- **Write informative tab labels.** Help users understand what content is inside the tabs.

#### Usability risks

- **Searching for content can be difficult.** While content nested within tabs can be found in most search engine results, finding this content within a page using keyboard find functionality can prove difficult for some users. This complexity can be alleviated with an in-page search present on pages with tabs that users can use to search for content that may be behind components like an ‘accordion’ or ‘tab’.
- **Users might not find content inside of tabs.** Tabs hide content from users, which introduces the risk that users might not notice or read all of the included content.
- **A team may mistakenly use tabs as a means to compare content between tabs.** [Need source/research]
- **A team may mistakenly use tabs as a means of site-level navigation.** Tabs should be used only for relating relative content within a page or module.
- **Label text might not be sufficiently descriptive.** Users might not think the tab content is relevant to them.
- **Tabs can add an extra click.** If you know your users will want to see the content, don't hide it behind a tab.

### 3.2 Accessibility considerations

#### Accessibility guidance

- **Include tabs in screen reader order.** Tabs should be individually labeled and called in the order they appear within the layout of the page.
- **Announce element type.** JAWS and NVDA users find it helpful if all expandable components like accordions and tabs announce their element type (with descriptive naming conventions that allude to the content nested inside of them) to save confusion and enable the element to be predictable, and understood. [Need source/research]
- **Ensure ARIA labels allude to tab label and content within tab.**
- **Design your content with assistive technologies in mind.** Consider the experience of using this component with keyboard navigation, screen readers, voice command, and with zoom magnification.
- To ensure the operation of a tab is predictable, [ARIA design pattern for tabs](https://www.w3.org/WAI/ARIA/apg/example-index/tabs/tabs-manual.html) is recommended.
  - The tab list should have an aria-label and contain the buttons marked-up with the role of tab. [Needs confirmation]
  - The tabs should have an aria-controls attribute referencing the id of the corresponding tab panel. [Needs confirmation]
  - The aria-selected attribute can be used to indicate the selected tab. [Needs confirmation]
  - The role of tabpanel should then be used with an aria-labelledby referencing the corresponding tab. [Needs confirmation]
  - Users should be able to move focus between tabs using the arrow keys on keyboard. [Needs confirmation]
  - Use ARIA live regions to highlight dynamically loaded content. When tags are used to call out new content that is dynamically loaded onto a page, be sure to use ARIA live regions to alter screen readers of the change.[Needs confirmation]

#### Accessibility risks

- **Content can be cut off with zoom magnification.** For low-vision users who require a zoom up to 400%, some tabs would appear off-screen even at large viewports, rendering the component unusable. To address this, we implemented a horizontal scroll and ultimately wrapped tab items in divs top to bottom to provide an experience that was more consistent than what we were able to achieve using list items within lists.
- A tabs component implemented without accessibility considerations may put keyboard-only users at risk of missing or not being able to access content nested within subsequent tabs.
- Any user dependent on ARIA labels to find content might be at risk of finding content if labels are not properly labeled.

#### What audiences would benefit from this component?

Users who have difficulty comprehending large quantities of information at once, or people with learning disorders such as dyslexia may benefit the most from tabbed content. These users will be able to select specific tabs and choose what to read without having to scan the entire content of a page at once. [Needs source/research]

### Unknowns

**Mobile presentation is unclear.** We need to figure out how this component will behave in narrow viewports. Here are some possible options:
- The [AWS demo](https://demo.badger.wwps.aws.dev/fire-safety-and-emergency-medical-services) implements horizontal scroll
- [State.gov](https://www.state.gov/) converts their tabs into accordions
- [GOV.UK](https://design-system.service.gov.uk/components/tabs/) stacks tab content

## 4. Stakeholders

### 4.1 Volunteers

_Tag any volunteers who are willing to help design, develop, or test this component. Include details about their roles._

### 4.2 Endorsements

_If there is significant support from a given agency or group, include their names here and tag any stakeholders._

### 4.3 Contributors

- Mazen Kharbutli, Software Development Engineer, AWS
- Miguel Abreu, Software Development Engineer, AWS
- Tanner Bachelor, User Experience Designer, AWS
