# [Skipto] proposal

## 1. About this component

### 1.1 Component name

As stated in https://github.com/uswds/uswds/discussions/5769 the most logical name is Skipto as this is the name of the library and the functionality it provides. There are some other names for skip-to functionality, but not sure any is better understood. 

### 1.2 Description

SkipTo uses JavaScript to create a per-page drop-down menu with links to important landmarks and headings, as an alternative to traditional "Skip To Main Content" links. 

### 1.3 Design system need

This fills an important accessibility and usability need, particularly for government sites. Often, government pages are long, and filled with multiple sections and hierarchies. For any user, trying to share, record or just remember where they were, having a Table of Contents for a pge is helpful. 

It ensures that there is better support for navigation within the page. The traditional "Skip To Main Content" is currently part of the USWDS, but this provides much richer functionality. 

This provides better support for long web pages. Currently the USWDS does not provide support for a Table of Contents, and there are a lot of pages like this, which need one:
  https://www.access-board.gov/ict/

This helps support Section 508. It has also been implemented in Joomla!:
  https://issues.joomla.org/tracker/joomla-cms/35590


### 1.4 Component design

A full description is available here https://github.com/paypal/skipto

There is no need to re-build this functionality, however it should be carefully reviewed for security, performance and of course accessibility, prior to implementation. 

#### 1.4.1 Core functionality

"SkipTo is a replacement for your old classic "Skip To Main Content" link, (so please use it as such)! The SkipTo script creates a drop-down menu consisting of the links to important landmarks and headings on a given web page identified by the author. Once installed and configured, the menu makes it easier for keyboard and screen reader users to quickly jump to the desired region of a page by simply choosing it from the list of options."

#### 1.4.2 Interactive states (Optional)

It interacts with the compoents on the page to build the dynamically menu, which is I think what you are looking for. 

#### 1.4.3 Possible variants (Optional)

I am unaware of a comparable alternative. 

#### 1.4.4 Demonstration (Optional)

See 1.4.

### 1.5 Implementation examples

See 1.4.

### 1.6 Related USWDS components

Some thought would need to be given to how to manage the existing "Skip To Main Content" link. Should this be an optionsl add-on? Should it depend on the complexity or location of the page? 

### 1.7 Key audiences

Any reader of a page with long content. 

Users with disabilities who may need additional navigational elements within a site. 

Authors, who may need to be able to see visualy how creating structured content is useful for more users.

## 2. Usage

### 2.1 When to use this component

I think this should be the default for most government sites.  It is more functional than the Main Content links. Also provides flexibility so that users can more quickly navigate where they need to, in order to share top tasks.

This component is particularly useful for long content. 

This component will need to be styled to align with the USWDS, and ensure that it matches the customizations required for the agency adopting it. 

Pages with long and complicated content is ideal for this type of content. 

### 2.2 When to consider something else

This may not be the best choice for short pages. Pages with dynamically generated content may be a problem. Login pages. 

It requires JavaScript, so some users may need a fall-back. 

## 3. Usability and accessibility

### 3.1 Usability considerations

User research on a variety of government pages would definitely be beneficial. 

### 3.2 Accessibility considerations

User research with people with disabilities on a variety of government pages would definitely be beneficial. 

This is a pattern which has been pioneered by some world-class leaders on digital accessibility. It is worth noting that there isn't an open issue queue on their repository.  

If this component isn't properly maintained, there may be some users who are faced with barriers. 

## 4. Stakeholders

### 4.1 Volunteers

@mgifford

### 4.2 Endorsements

PayPal Accessibility Team & the University of Illinois. 

### 4.3 Contributors

@mgifford
