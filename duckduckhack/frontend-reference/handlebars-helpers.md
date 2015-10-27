# Handlebars Helpers

When creating [custom handlebars sub-templates](https://duck.co/duckduckhack/subtemplates) for your Instant Answer, you have access to a variety of built-in helper functions. In addition to the standard [handlebars helpers](http://handlebarsjs.com/#helpers), the following helpers are provided as part of the Instant Answer framework:

- [`#concat`](#codeconcatcode): Concatenates all the elements in a collection

- [`#condense`](#codecondensecode): Shortens a string

- [`#stripHTML`](#codestriphtmlcode): Strips HTML tags/elements from text

- [`#loop`](#codeloopcode): Counts from zero to the value of `context`

- [`#each`](#codeeachcode): Extends Handlebars' built-in `{{each}}` lets you specify optional first and last indices

- [`#keys`](#codekeyscode): Iterates over the properties of an object and provides a new object containing the "key" and "value" 

- [`include`](#codeincludecode): Loads the specified Handlebars template and applies it with the current context

- [`plural`](#codepluralcode): Returns the value of `context` and appends the singular or plural form of the specified word

- [`numFormat`](#codenumformatcode): Delimits a number or string with multiple numbers, using commas or given delimiter

- [`imageProxy`](#codeimageproxycode): Rewrite a URL as a DuckDuckGo image redirect

- [`ellipsis`](#codeellipsiscode): Shortens a string by removing words until string length is <= `limit` and appends an ellipsis ('...') to the output 

- [`trim`](#codetrimcode): Removes leading and trailing spaces from text 

## `#concat`

**Block Helper**

Concatenates all the elements in a collection

An optional item separator can be appended to
each item and an optional conjunction can be
used for the last item.

Example:

```html
{{#concat context sep="," conj="and"}}
{{this}}
{{/concat}}
```

when `context` is:
- `['a']`           returns:  `a`
- `['a', 'b']`      returns:  `a and b`
- `['a', 'b', 'c']` returns:  `a, b and c`

**Parameters**

**sep**:  *string*,  **[optional]** Item separator. Default: `''`

**conj**:  *string*,  **[optional]** Final separator, precedes last item. Default: `''`


## `#condense`

**Block Helper**

Shortens a string

An optional maximum string length can be provided if preferred.

Example:

`{{condense myString maxlen="135" truncation="..."}}`

This will output the value of `myString` up to a maximum of 135 characters
(not including the length of the truncation string) and then append
the truncation string to the output

**Parameters**

**maxlen**:  *number*,  **[optional]** Maximum allowed string length. Default: `10`

**fuzz**:  *number*,  The allowable deviation from the maxlen, used to allow a sentence/word to complete if it is less than fuzz characters longer than the maxlen

**{string**,  truncation **[optional]** The truncation string. Default: `'...'`


## `#stripHTML`

**Block Helper**

Strips HTML tags/elements from text

Example:

`{{#stripHTML stringWithHTML}}Here is my string: {{this}}{{/stripHTML}}`


## `#loop`

**Block Helper**

Counts from zero to the value of `context` (assuming `context` is a **number**)
applying the content of the block each time

Note: A maximum of 100 loops is allowed.

Example:

```html
{{#loop star_rating}}
<img src="{{star}}" class="star"></span>
{{/loop}}
```


## `#each`

**Block Helper**

Extends Handlebars' built-in `{{each}}`
lets you specify optional inclusive first and last indices
to iterate between

Example:

`{{#each myArray from="2" to="5"}} ... {{/each}}`

This will limit the iteration to array indices 2, 3 and 4.

If `to` is not given, defaults to array (or object) length:

`{{#each myArray from="2"}} ... {{/each}}`

will skip the first two items

If `from` is not given, defaults to 0:

`{{#each myArray to="5"}} ... {{/each}}`

will only do the first five items

**Parameters**

**from**:  *number*,  **[optional]** Index to start from. Default: `0`

**to**:  *number*,  **[optional]** Index to end on. Default: array/object length


## `#keys`

**Block Helper**

Iterates over the properties of an object and provides
a new object containing the "key" and "value" for each

Example:

```html
{{#keys myObject}}
{{key}} : {{value}}
{{/keys}}
```


## `include`

Loads the specified Handlebars template and applies it with
the current context

Note: There is no recursive cycle detection! **Be careful**.

Example:

`{{include ../myTemplate}}`

Applies the template `myTemplate` using `this` as the data context

`{{include ../myTemplate with="x"}}`

Applies the template `myTemplate` using `this.x` as the data context.
Identical to:

`{{#with x}} {{include ../template}} {{/with}}`

**Parameters**

**with**:  *string*,  **[optional]** Context to use when including the template. Supports simple dot paths.


## `plural`

Returns the value of `context` (assuming `context` is a **number**)
and appends the singular or plural form of the specified word,
depending on the value of `context`

Example:

`{plural star_rating singular="star" plural="stars"}}`

Will produce:
- `{{star_rating}} star`  if the value of `star_rating` is `1`, or
- `{{star_rating}} stars` if `star_rating` > `1`

**Parameters**

**singular**:  *string*,  Indicates the singular form to use

**plural**:  *string*,  Indicates the plural form to use

**delimiter**:  *string*,  **[optional]** Format the number with the `numFormat` helper


## `numFormat`

Delimits a number or string with multiple numbers,
using commas or given delimiter

Note: This supports integers and decimal numbers.

Credit: This function was borrowed from
http://cwestblog.com/2011/06/23/javascript-add-commas-to-numbers/

Example:

```html
{{numFormat num}}
{{numFormat num delimiter="." }}
```

**Parameters**

**delimiter**:  *string*,  **[optional]** The delimiter string. Default: `','`

## `imageProxy`

Rewrite a URL as a DuckDuckGo image redirect

Example:

`{{imageProxy imageURL}}`

produces: `/iu/?u={{imageURL}}`


## `trim`

Removes leading and trailing spaces from text

Example:

`{{trim stringWithSpaces}}`


## `ellipsis`

Shortens a string by removing words until string length is <= `limit` and
appends an ellipsis ('...') to the output

Note: It automatically appends any closing tag if one is missing.

Example:

`{{ellipsis title 50}}`

**Parameters**

**text**:  *string*,  text to shorten

**limit**:  *number*,  maximum length of shortened string

## Creating Custom Helpers

Of course, since we're using [Handlebars](http://handlebarsjs.com/), you can create your own helpers as well. Simply define your helper alongside your frontend callback. For example, see how the *Alternative To* Instant Answer defines the `AlternativeTo_getPlatform` helper in [`alternative_to.js`](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js):


```javascript
    env.ddg_spice_alternative_to = function(api_result) {
        ...
    };

    Handlebars.registerHelper("AlternativeTo_getPlatform", function (platforms) {
        return (platforms.length > 1) ? "Multiplatform" : platforms[0];
    });
```

This handlebars helper is very simple: it takes an array as input and depending on the length, returns either the first element in the array, or if more than one element exists, returns the string "Multiplatforms". You can learn more about helpers on the [Handlebars documentation](http://handlebarsjs.com/).