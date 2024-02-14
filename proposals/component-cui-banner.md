# CUI Banner proposal

## 1. About this component

### 1.1 Component name

Controlled Unclassified Information (CUI)  Banner

### 1.2 Description

The CUI banner creates a consistent pattern for marking controlled unclassified information in electronic contexts.

### 1.3 Design system need

CUI must be clearly marked when it is displayed on a website or printed from the screen. Creating a common CUI banner would create a clear and consistent pattern that ensures compliance with current policy.

From GSA’s CUI Guide: “CUI indicators must be present to alert users of the presence of CUI within the system. A warning must be shown on the login screen or via a screen after logging in, and optionally in headers that appear on each page displayed. Additionally, any printouts generated from an application must have the CUI banner on every page of the printout. If these are not printed by the application, the user must write the banner on every page that is printed or use a CUI cover sheet to protect the information that is printed.”

#### Related laws and policies

The CUI program was established by Executive Order 13556 [PDF], and implemented by 32 CFR part 2002.

### 1.4 Component design

The CUI banner should clearly convey to users that they are viewing controlled unclassified information.

The banner must be present both when viewed on screen and when printed from the screen.

#### Resources

- [CUI Marking guide](https://www.archives.gov/files/cui/documents/20161206-cui-marking-handbook-v1-1-20190524.pdf) [NARA]
- [CUI Marking quick tips](https://www.gsa.gov/system/files/CUI%20Quick%20Tips.docx) [GSA]

#### 1.4.3 Possible variants

There are two likely variants for this component:

- **CUI Basic:** CUI Basic is, as the name implies, the standard “flavor” of CUI. All of the rules of CUI apply to CUI Basic Categories and Subcategories, making the handling and marking of CUI Basic the simplest. [NARA’s CUI marking guide](https://www.archives.gov/files/cui/documents/20161206-cui-marking-handbook-v1-1-20190524.pdf).
- **CUI Specified:** CUI Specified is different, since the requirements for how users must treat each type of information vary with each Category or Subcategory. This is because some Authorities have VERY specific requirements for how to handle the type of information they pertain to – requirements that simply would not make sense for the rest of CUI. CUI Specified is NOT a “higher level” of CUI, it is simply different.
  And because the things that make it different are dictated in laws, Federal regulations, and government-wide policies, they are not things that can legally be ignored or overlooked. As such, a document containing multiple CUI Specified Categories and Subcategories must include ALL of them in the CUI Banner Marking. [NARA’s CUI marking guide](https://www.archives.gov/files/cui/documents/20161206-cui-marking-handbook-v1-1-20190524.pdf)

#### 1.4.4 Demonstration

Here is a simple mockup of a CUI banner from NARA’s CUI marking guide:

### 1.5 Implementation examples

Provide a list of links to examples of this kind of component on government (preferred) or non-government sites.

### 1.6 Related USWDS components

This component could possibly be a cousin of the site alert component.

### 1.7 Key audiences

This component is designed for agencies that want to display CUI on websites and applications.

## 2. Usage

### 2.1 When to use this component

- Use this component when you need to mark controlled unclassified information.
- Follow the specific guidelines for the particular type of CUI that is present (CUI Basic/CUI Specified)
- All other rules and regulations for CUI must be followed.

### 2.2 When to consider a different component

Do not use this component for content that does not contain CUI.

## 3. Usability and accessibility

### 3.1 Usability considerations

The banner should be prominent and clearly communicate its message.

### 3.2 Accessibility considerations

The banner should be visible to all assistive devices. The accessibility guidance added to the site alert component could possibly apply here.

## 4. Stakeholders

### 4.1 Volunteers

If there are any volunteers who are willing to help design, develop, or test this component, tag them here with details about their roles.

### 4.2 Endorsements

If there is significant support from a given agency or group, include their names here and tag any stakeholders.

### 4.3 Contributors

Create a list of those who helped carry out the research and work to prepare this proposal. Include your name and/or GitHub username if you'd like credit as a contributor.
