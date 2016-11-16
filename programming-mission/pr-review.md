# How to review a Pull Request

This checklist is intended for Language Leaders and Community Leaders. Here you'll find everything that should be addressed when reviewing a Pull Request.

Before merging, make sure the latest changes have been deployed to Beta and thoroughly tested. In case you're unsure or have issues, please reach out to either **@moollaza** or **@maria** on Slack.


## General
- Is the PR related to an existent GitHub issue? 
    - If not, and if it's a new IA, the contributor should [create a new project for it on the forum](https://forum.duckduckhack.com/t/how-to-create-a-new-forum-project/814). The PR will be on hold until the idea is approved.
- Does the PR follow the [correct template](https://github.com/duckduckgo/zeroclickinfo-fathead/blob/master/.github/PULL_REQUEST_TEMPLATE.md)?
- Does the Instant Answer have an associated IA Page?
- Is there a link to the IA Page, and is it correct?
- The PR should only contain changes related to 1 Instant Answer and associated files
- Is the PR title appropriate?
    - For a Bug Fix: {IA Name}: {Description of change}
    - For a New Instant Answer: New {IA Name} {Type (eg "Fathead")}
    - For anything else: {Tests/Docs/Other}: {Short Description}


## Code

#### Style
- Does it adhere to our [code style guide](https://docs.duckduckhack.com/resources/code-style-guide.html)?
    - 4-space indents
    - Semicolons
    - etc.
- Do filenames adhere to our naming conventions?

#### Fatheads
- Does the code have dependencies?
    - If yes, make sure they're specified in a requirements.txt/gemfile/package.json/etc. file in the IA directory
- Is [coverage data](https://docs.duckduckhack.com/programming-mission/creating-effective-fatheads.html) included?
    - Make sure to run the Fathead coverage test to identify anything missing


#### Spices and Goodies
- Does it use a built-in [template](https://docs.duckduckhack.com/frontend-reference/template-groups.html)?
    - It shouldn't use the [Base template](https://docs.duckduckhack.com/frontend-reference/template-groups.html#base-template-group) unless explicitly requested/approved by staff
- If an API key is required, where can the DDG staff request their own copy? Make sure to ping **@moollaza** on Slack

#### Perl:
- Are all constants and private `sub`s defined outside the `handle` fn?
- Is there a check that `$loc`, `$req`, and `$lang` are defined before using them?
- Are all files opened and read outside of the handle function?
- Does a CPAN module exist that we can use?
    - Instead of implementing something yourself, check if a module already exists on CPAN
- The Perl should not make any network requests
    - We cannot allow the Perl to do this
    - Any CPAN modules that make web requests are not allowed

#### JavaScript:
- Is the code wrapped in closure?
- Is `use strict;` included at the top
- Does this rely on any third party libraries?
    - The developer should ask us before using external libraries. We need to add it internally if we agree to use it
- Private variables and functions should be defined outside callback function
- `Spice.failed()` should always be called when stopping execution prematurely
- If the code needs to exit (e.g. the API response is missing required information) it must call `Spice.failed()`, so other Instant Answers are able to display
- Experimental and browser-specific methods are not allowed. We need to ensure a consistent experience across all devices and browsers
    - We support IE 9+, Edge, Chrome, Firefox, Safari, Opera, etc.
- Will any code break if the API response is undefined?
    - Make sure objects exist before accessing nested properties
    - You can use `DDG.getProperty()` to get properties which may undefined (e.g. `DDG.getProperty(my_obj, 'some.property.name')`)

#### CSS:
- Is there any custom CSS?
    - Custom CSS should be kept to a minimum. We prefer none, if possible
- Are all CSS rules name-spaced?
    - None of the CSS should be able to affect other Instant Answers or page elements
- Font-colour, font-size and font-family should be defined by template variants, or our DDG classes (e.g. `.tx--14`, `.bg-clr--grey`, `.tx-clr--green`)
- Template padding and margins should not be modified
- Experimental and browser-specific methods are not allowed. We need to ensure a consistent experience across all devices & platforms
    - We support IE 9+, Edge, Chrome, Firefox, Safari, Opera, etc.

#### Tests:
- Is a test file included?
- Are all example queries covered by tests?
- Are there tests for queries that **shouldn't** trigger the IA?
    - Make sure edge cases and false positives are handled correctly

#### Triggers:
- List of dictionary words as triggers should be avoided (i.e. generic or ambiguous words that don't indicate search intent)
- Use word/phrase triggers unless regex is absolutely neceseary
    - Regexes should only be used when matching specific patterns or types of characters (numbers, unicode symbols)
- Trigger words must be lowercase

#### Cheat Sheets
- Make sure the description is not redundant
- Is the spelling correct?
- "Title Case" should be used for name and sections
- "Sentence case" should be used for description and explanations
- Ensure the `CheatSheet.t` test passes
- Use JSONLint to check the file and the text format
- Every key, value and section should be filled; There should be no blanks.
- Are there less than 200 lines of JSON?
    - Cheat sheets should be easy-to-read, quick references

## Design
- Does it look good on all 5 major browsers and mobile?
    - Chrome, Safari, Firefox, IE 9, IE Edge
    - Android, iOS, iPad
    - There should be no breakage when the page is resized
- Does it look good across all DDG themes?
    - Check especially the default and dark themes
- Do all actions work both on desktop and mobile?
    - There shouldn’t be “desktop only” behaviour (e.g. rollover/hover effects) that can’t be used on mobile


## IA Pages
- Does the IA Page specify the correct Perl module? (e.g `DDG::Spice::MySpice`)
- Is the Instant Answer type field (i.e. Spice, Goodie, Fathead, Longtail) correct?
- Is the ID correctly formatted and matching the filenames?
  - ID's must be lowercased, and words must be separated with and underscore (`_`)
  - You can see the ID from the IA Page URL, eg in duck.co/ia/view/mdnjs the ID is "mdnjs"
- Is the Pull Request listed in the IA Page? 
    - If not, ensure the ID specified in the PR description matches the IA Page ID
- Is the IA tab name taken from our list of Topics?
    - It should not contain any brand names and should be generalized to a larger topic
- Does the IA Page have the correct topics (language topic, eg "JavaScript", and category topic, like "Reference")
- Is the maintainer field filled in? Is that the correct person?

#### Fatheads
- Does it have a source ID?
- Does it have a Perl Module matching the ID?
  - Although the file won't exist, we currently need a defined Perl Module (e.g. `DDG::Fathead::MdnCss` for ID `mdn_css`)

