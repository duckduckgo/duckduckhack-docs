# Instant Answer Production Guidelines

The community has developed a set of guidelines by which all live Instant Answers adhere. The guidelines have one goal in mind: **create a great experience across millions of queries.**

We do our best to keep this list as quick and relevant as we can. We'd love your help in evolving these standards! Have an opinion or suggestion on how to make these better? Definitely let us know.

[![slack](http://docs.duckduckhack.com/assets/slack.png) We'd love to help you with these guidelines. Talk to us on Slack]({{ book.slackURL }}) or [email us](mailto:open@duckduckgo.com).

## What queries will your Instant Answer show up on?

- **Instant Answers should answer more than a single query - preferably more than ten.**

	For example, if your idea is to answer "What is the speed of light?" with a constant, that's only one query for an Instant Answer. Instead, consider a "Physics Constants Instant Answer" to cover many common constants (Speed of sound, Planck's constant, and so on...). Similarly, "When is Christmas?" would be better grouped under a "Holiday Dates Instant Answer."

	If a wider Instant Answer already exists that should encompass your queries, consider improving it.

## Do you plan to use an external data source?

- **API sources must be reliable and authoritative.**

	APIs used should represent the *most credible source* for the information. This means it should be the preferred data source of its community.

	It should be reasonable to expect that an API will continue be around for at least several years.

	APIs must, of course, have the appropriate rights to serve their data.

	*For all of these reasons, APIs created by contributors solely for the purpose of an Instant Answer cannot be accepted.*

- **APIs must be free.**

	Many APIs are happy to offer DuckDuckGo free access because of attribution and exposure. Consider reaching out and asking - you may be surprised.

- **APIs must return in JSON format.**

	Currently we can only support JSON responses.

- **APIs must be accessible via GET requests, and authorized via URL parameters.**

	Currently we cannot support POST requests.

	Instant Answers cannot authorize requests with OAuth or HTTP Headers.

- **APIs must respond in under 1 second, and with less than 200kb of data.**

	We do not recommend "APIs" that are actually static hosted files. You can, however, [use a data file](http://docs.duckduckhack.com/backend-reference/data-files.html) as part of your Instant Answer.

	If you're not sure about this, we're happy to help.

## Does the data source have paywalled content?

- **For any content provider supplying data to an Instant Answer, any paywalled content must be:**

	1. Labeled as such in the Instant Answer; and

	2. Must always provide enough information in the Instant Answer/landing page combination to be significantly more useful than the organic results.

## Are you using static (hardcoded) information?

- **All information should remain accurate in the long term.**

	Any information likely to change should come from an API, not a data file. For example, an Instant Answer that answers "Who is the president of the United States?" should not be hardcoded.

## Anything you wouldn't show or say to your mother?

- **Crude language is allowed.**

	For example, Urban Dictionary definitions are allowed. Just make sure to set the [`is_unsafe`](http://docs.duckduckhack.com/backend-reference/spice-attributes.html#spice-isunsafe) attribute.

- **No adult content.**

	Adult content is not allowed, neither in handling of queries, or results returned.

## How are you displaying your results?

- **All new Instant Answers should use [built-in Template Groups](http://docs.duckduckhack.com/frontend-reference/templates-overview.html).**

	For reasons of maintainability, we cannot accept submissions using the Base template unless they've received prior permission (by discussing with community leaders or staff on [Slack]({{ book.slackURL }}) or [email](mailto:open@duckduckgo.com)).

	There are many ways to customize the built-in templates, including [options](http://docs.duckduckhack.com/frontend-reference/display-reference.html), [variants](http://docs.duckduckhack.com/frontend-reference/variants-reference.html), and [sub-templates](http://docs.duckduckhack.com/frontend-reference/subtemplates.html).

- **Tab names ([`name`](http://docs.duckduckhack.com/frontend-reference/display-reference.html#name-string-required) display property) should belong to the [list of topics](http://docs.duckduckhack.com/frontend-reference/display-reference.html#name-string-required).**

	See our list of topics [topics and their guidelines](http://docs.duckduckhack.com/frontend-reference/display-reference.html).

## What did you include in your code?

- **All JavaScript methods should be supported on IE9+, Chrome, Firefox, and Safari.**

	You can check this [handy table for reference](http://kangax.github.io/compat-table/es5/).

- **No external requests can be made in Perl.**

	Any CPAN modules that make web requests are not allowed. All external requests must be made in the form of a Spice Instant Answer. See this [walkthrough](http://docs.duckduckhack.com/walkthroughs/forum-lookup.html) for details.

## How are you testing your code?

- **All example queries should be covered in a [test file](http://docs.duckduckhack.com/testing-reference/test-files.html).**

	A good test file makes sure your Instant Answer continues to function properly. In addition, test files makes your intentions clear to future collaborators.

	This is not necessary for cheat sheets.

- **All test files should include negative cases - queries that *should not* trigger.**

	If test cases make your intentions clear, negative test cases make them even clearer! Negative test cases are a great opportunity to ensure the scope of your Instant Answer.

## User Experience

- **All interactions should work on both desktop and mobile.**

	Avoid interactions that only work on desktop - e.g., hover.

- **Instant Answers should look good across all platforms.**

	Test how your Instant Answer looks on Chrome, Safari, Firefox, IE 9, IE Edge, as well as Android, iOS, and the iPad.

- **Instants Answers should look good across [DuckDuckGo Themes](https://duckduckgo.com/settings) (click *Theme*).**

	Test your Instant Answer with the Dark Theme in particular.

	If you normally use a theme, make sure to test it on the the default theme.

[![slack](http://docs.duckduckhack.com/assets/slack.png) Have questions? Talk to us on Slack]({{ book.slackURL }}) or [email us](mailto:open@duckduckgo.com).
