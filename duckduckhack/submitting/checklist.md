# Instant Answer Checklist

All Instant Answers currently live on DDG adhere to x... we've tried to outline what we believe make for the best experience. These are below... 

In order to be as transparent and simple as possible, we've collected these requirements into a checklist you can review when planning - and before submitting - your Instant Answer. We do our best to keep this list as quick and relevant as we can.

We'd love your help in evolving these standards! Have an opinion or suggestion on how to make these better? Definitely let us know.

If you're not sure, or want help satisfying this checklist, we'd love to help! We have a great community [on Slack](mailto:QuackSlack@duckduckgo.com?subject=AddMe) where you can find someone to give detailed feedback. You can also [send an email](mailto:open@duckduckgo.com).

## What queries will your Instant Answer show up on?

- **Instant Answers should answer more than a single query, and preferably more than ten.**

	For example, if your idea is to answer "What is the speed of light?" with a constant, that's only one query for an Instant Answer. Instead, consider a "Physics Constants Instant Answer" to cover many common constants (Speed of sound, Planck's constant, and so on...). Similarly, "When is Christmas?" would be better grouped under a "Holiday Dates Instant Answer."
	
	If a wider Instant Answer already exists that should encompass your queries, consider improving it.

## Do you plan to use an external data source?

- **API queries must be free.**

	While paid APIs are not allowed, many APIs are happy to offer DuckDuckGo free access because of attribution and exposure. Consider reaching out and asking.
	
- **APIs must return in JSON format.**

	Currently we can only support JSON responses.
	
- **APIs must be accessible via GET requests, and authorized via URL parameters.**

	Currently we cannot support POST requests. We also cannot authorize requests via OAuth or HTTP Headers.
	
- **APIs must respond in under 1 second, and with less than 200kb of data.**

	If you're not sure about this, we're happy to help.

## Are you using static (hardcoded) information?

- **All information should remain accurate in the long term.**

	Any information likely to change should come from an API, not a data file. For example, an Instant Answer that answers "Who is the president of the United States?" should not be hardcoded.
	
## Anything you wouldn't show or say to your mother?

- **Crude language is allowed.**

	For example, Urban Dictionary definitions are allowed. Just make sure to set the [`is_unsafe`](#) attribute.

- **No adult content.**

	Adult content is not allowed, neither in handling of queries, or results returned.
	
## How are you displaying your results?

- **All new Instant Answers should use [built-in Template Groups](#).**

	For reasons of maintainability, we cannot accept submissions using the Base template unless they've received prior permission. There are many ways to customize the built-in templates, including [options](#), [variants](#), and [sub-templates](#).
	
- **Tab names ([`name` display property](#)) should belong to the list of topics.**

	See our list of topics [topics and their guidelines](#).
	
## What did you include in your code?

- **All JavaScript methods should be supported on IE9+, Chrome, Firefox, and Safari.**

	You can check this [handy table for reference](http://kangax.github.io/compat-table/es5/).
	
- **No external requests can be made in Perl.**

	Any CPAN modules that make web requests are not allowed.
	
## How are you testing your code?

- **All example queries should be covered in a [test file](#).**

- **All test files should include negative cases - queries that *should not* trigger.**
	
## User Experience

- **All interactions should work on both desktop and mobile.**

	Avoid interactions that only work on desktop - e.g., hover.
	
- **Instant Answers should look good across all platforms.**

	Test how your Instant Answer looks on Chrome, Safari, Firefox, IE 9, IE Edge, as well as Android, iOS, and the iPad.

- **Instants Answers should look good across [DuckDuckGo Themes](#).**

	Test your Instant Answer with the Dark Theme in particular. 
	
	If you normally use a theme, make sure to test it on the the default theme.
	
