## JavaScript API Reference

For a list of available frontend JavaScript functions see:

# Functions in the DDG Namespace

The following functions are useful in the broader context of DuckDuckGo's frontend and available for use by Instant Answers.

## get_query_encoded()

Provides the value of `DDG.get_query` as a URIEncoded string

Note: The query is trimmed (i.e. no leading or trailing spaces) and
has any extra spaces within the query removed

## get_query()

Provides the search query, as displayed in the search box

Note: The query is trimmed (i.e. no leading or trailing spaces) and
has any extra spaces within the query removed

## get_is_safe_search()

Indicates if "safe search" is on, for the current query

**Returns**

*boolean*,  Either `1` or `0` (on/off)

## get_asset_path(spice_name, asset)

Provides the path to the given asset, for the specified Instant Answer

Example:

`DDG.get_asset_path('quixey', 'quixey_logo.png')` -> `'/share/spice/quixey/1234/quixey_logo.png'`

**Parameters**

**IA_name**:  *string*,  The name of the Instant Answer (this gives us the correct `/share/...` relative path)

**asset**:  *string*,  The filename of the asset, including extension


## getRelevants(p)

Provides an array of relevant strings, given an input array of comparator strings

Note: This is a shortcut to running `isRelevant()` against an array and collecting only the relevant results

Example:

```javascript
var relevants = DDG.getRelevants({
    num:        10, // the first 10 relevant candidates will be returned
    candidates: ['is this relevant', 'is this one relevant', 'how about this one', ... ], //candidate strings
    skipArray:  ['a', 'list', 'of', 'words'], //words to ignore in comparison
    strict:     false
});
```
Only the `candidates` array is required, the other parameters are optional. `num` defaults to `candidates.length`

**Parameters**

**p**:  *object*,  An object containing an array of candidate strings and other optional parameters to be passed along to `DDG.isRelevant`, including: `num` - the maximum amount of results to return, `skipArray`, `minWordLength`, and `strict`


## isRelevant(candidate, skipArray, minWordLength, strict)

Determines if the candidate string is relevant to **the search query**

**Parameters**

**candidate**:  *string*,  The string to be checked for relevancy

**skipArray**:  *array*,  **[optional]** An array of words (usually the trigger words) that should not be considered in determining the candidate string's relevancy

**minWordLength**:  *number*,  **[optional]** The minimum length for any words to be considered in the comparison (used to ignore small words like "to", "and", "is", "a", etc.), Default: `4`

**strict**:  *boolean*,  **[optional]** Turns on stricter relevancy checking, by switching candidate and comparator strings, Default: `0`


## stringsRelevant(s1, s2, skipArray, minWordLength, strict)

Determines if the candidate string is relevant to the given comparator string

**Parameters**

**s1**:  *string*,  The string to be checked for relevancy

**s2**:  *string*,  The string to be compared against

**skipArray**:  *array*,  **[optional]** An array of words (usually the trigger words) that should not be considered in determining the candidate string's relevancy

**minWordLength**:  *number*,  **[optional]** The minimum length for any words to be considered in the comparison (used to ignore small words like "to", "and", "is", "a", etc.), Default: `4`

**strict**:  *boolean*,  **[optional]** Turns on stricter relevancy checking, by switching candidate and comparator strings, Default: `0`


## parse_link(string, wanted)

Parses a string containing an anchor tag, ('<a href="URL">text</a>'), and returns the URL or text
as indicated

Note: If more than one anchor tag exists in the string, the first will be parsed

Example:

`str = '<a href="https://mywebsite.com">Click here!</a> to see my website.'`

- `DDG.parse_link(str)` -> `'https://mywebsite.com'`
- `DDG.parse_link(str, 'text')` -> `'Click here!'`
- `DDG.parse_link(str, 'rest')` -> `' to see my website.'`

**Parameters**

**string**:  *string*,  A string containing an anchor tag

**wanted**:  *string*,  **[optional]** The piece of the link to return Default: `'url'`


## getDateFromString(date)

Provides a JavaScript `Date()` object for the given Date string

**Parameters**

**date**:  *string*,  Date string in UTC format with time (yyyy-mm-ddThh:mm:ss) or without (yyyy-mm-dd)


## strip_html(html)

Removes HTML tags/characters from a string

**Parameters**

**html**:  *string*,  String containing HTML

Example:
	
- `strip_html("<strong>DuckDuckGo</strong>")` -> `"DuckDuckGo"`
- `strip_html("<a href='http://duckduckgo.com'>DuckDuckGo</a>'")` -> `"DuckDuckGo"`

## strip_href(html)
Removes `src` and `href` attributes from a string

Note: The `src` and `href` attributes are not removed entirely. They are prefixed with `_`

**Parameters**

**html** : *string*, String containing `href` or `src` attributes

Example:

- `strip_href("<a href='http://duckduckgo.com'>DuckDuckGo</a>")` -> `"<a _href='http://duckduckgo.com'>DuckDuckGo</a>"`
- `strip_href("<img src='image.png'")` -> `"<img _src='image.png'"`

## getOrdinal(number)

Provides the proper ordinal noun for a given number

Example:

`DDG.getOrdinal(456)` -> `'456th'`

**Parameters**

**number**:  *number*,  The number you need an ordinal for


## strip_non_alpha(str)

Removes Non-Alpha characters (`\W`) from a string

**Parameters**

**str**:  *sting*,  The input string to strip

## capitalize(str)

Capitalizes the first letter of the given string

**Parameters**

**str**:  *string*,  String to capitalize


## capitalizeWords(str)

Capitalizes the first letter of each word in the given string

**Parameters**

**str**:  *string*,  String to capitalize


## getProperty(obj, pathname)

Provides the member of an object using dot separated path

It's best to use this only when the sub elements might not be defined,
to avoid complex and awkward expressions.

Note: Arrays can use the index number since we access object
properties and array indices in the same way

Example:

`obj = { a: { b: { c: 'test', d: [1,2,3] }}}`

- `getProperty(obj, 'a.b.c')`     -> `'test'`
- `getProperty(obj, 'a.b')`       -> `{ c:'test' }`
- `getProperty(obj, 'a.b.d.0')`   -> `1`

**Parameters**

**obj**:  *object*,  the object to look through

**pathname**:  *string*,  the dot separated path of object properties and/or array indices

## isNumber(value)

Determines if an input is a Number

**Parameters**

**value**: the value to check

Example:

- `isNumber(10)` -> `true`
- `isNumber("HelloWorld")` -> `false`
- `isNumber(NaN)` -> 'false'

## abbrevNumber(value)

Returns an abbreviated string representation of a number.

**Parameters**

**value**: *number*, the number to abbreviate


Example:

- `abbrevNumber(1)` -> `1`
- `abbrevNumber(1000)` -> `1k`
- `abbrevNumber(1000000)` -> `1M`

## commifyNumber(value)

Returns the comma separated string representation of a number

**Parameters**

**value**: *number*, the number to comma separate

Example:

- `commifyNumber(10000)` -> `10,000`

## formatDuration(value)

Returns a string in the format of HH:MM:SS

**Parameters**

**value**: *number*, the total milliseconds to format

Example:

- `formatDuration(86400000)` -> `24:00:00`
- `formatDuration(150000)` -> `2:30`
- `formatDuration(1000)` -> `0:01`


## toHTTPS(url)

Returns a string with the https protocol

**Parameters**

**url**: *string*, A url with the http protocol

Example:
 - `toHTTPS("http://duckduckgo.com")` -> `"https://duckduckgo.com"`
 - `toHTTPS("duckduckgo.com")` -> `"duckduckgo.com"`


## toHTTP(url)

Returns a string with the http protocol

**Parameters**

**url**: *string*, A url with the https protocol

Example:
 - `toHTTP("https://duckduckgo.com")` -> `"http://duckduckgo.com"`
 - `toHTTP("duckduckgo.com")` -> `"duckduckgo.com"`


## scaleToFit(width, height, maxWidth, maxHeight)
Returns an object containing width and height properties scaled proportionally to fit within a specified range

**Parameters**

**width** : *number*, Current width of an element

**height** : *number*, Current height of an element

**maxWidth** : *number*, Max width available for element

**maxHeight** : *number*, Max height available for element

Example:

- `scaleToFit(4,2, 2, 1)` -> `{ width: 2, height: 1 }`
- `scaleToFit(10,10,5,3);` -> `{ width: 3, height: 3 }`

------


# DDH Namespace

The following functions are available and relevant to both Spice and Goodie Instant Answers.

## getDOM(id)

Provides a scoped DOM for a given the Instant Answer's id.

Note: Seeing as we maintain a cache, this is more efficient than using jQuery, i.e. `$('IA_name')`

Example:

`var $my_IA = DDH.getDOM('my_IA')`

**Parameters**

**id**:  *string*,  The id of the Instant Answer. If a Spice, should match the `id` property of the object given to `Spice.add()`.

**Returns**

*object*, A jQuery object, matching the selector that targets the given id.

## registerHelper(id, fn)

Provides access to `Handlebars.registerHelper()` so you can register helpers for your Instant Answer.

**Parameters**

**id**:  *string*,  The name of the helper to register

**fn**:  *function*,  The function we are registering


# Spice Namespace

The following functions are available and relevant to Spice Instant Answers.

## add(options)

Add an Instant Answer to the AnswerBar and display it

Note: A detailed explanation of `Spice.add()` can be found in [Displaying your Spice](#)

**Parameters**

**options**:  *object*,  The object containing all necessary information for creating a Spice Instant Answer


## failed(id)

Alerts the frontend that an Instant Answer has stopped executing, preventing it from being displayed.

Note: This is generally used when a Spice API returns no useful results.

Example:

```javascript
if (/* check for no results */) {
	Spice.failed()
}
```

To see an example of this, visit the [Forum Lookup Walkthrough](#).

**Parameters**

**id**:  *string*,  The id of the Spice Instant Answer, should match the `id` property of the object given to `Spice.add()`
