# Creating Effective Reference Fatheads

While on the surface Fatheads appear simple, there are a few steps you can take toward increasing your Fathead's query coverage and accuracy.

This article will run through some of these, focusing on creating programming IAs.


## Full topic coverage

A strong first step in planning your Fathead is to gather the set of articles you wish to provide coverage for.

Firstly, you can check index pages and content menus for lists of content you can incorporate. For example, the navigation menu on the left of [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/) pages has a list of language entities under "References:". Taking note of these and ensuring they are all processed by your parser will go a long way in increasing coverage.

If creating a programming Fathead, you need to create a `cover/` directory containing one or more text files (`.txt`) that list all the topic titles and language features you need to cover. These lists will then be used as Unit tests to help you measure your Fathead's coverage. Using the example of a programming language Fathead, this list should come from a source separate to the Fathead source. For example, if using MDN you could use the [list of reserved keywords from the ECMA specification](http://ecma-international.org/ecma-262/6.0/#sec-keywords).

These files should be categorised by entity type to aid validation and Fathead redirect creation. As described below, certain filenames can be used to also generate additional redirects.

### Example
The Perl Fathead serves as a great example. It has two lists covering functions and special variables. The lists can be seen [here](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/c441e54d98b92cabce04154774cfbae485da63bd/lib/fathead/perl_doc/cover).


### Coverage Data Redirect Generation

Special filenames can be used for the file(s) in your `/cover` directory to automatically generate additional redirects (aliases) for your Fathead. The following filenames will generate redirects by prefixing, and appending the associated keywords to each article title in the file:

- methods.txt   => [ method, function, func, subroutine ]
- functions.txt => [ function, func, method, subroutine, keyword, call ]
- variables.txt => [ var, variable, special variable ],
- operators.txt => [ operator, function, func ]
- tags.txt      => [ tag, tags, element, elements, entity, entities, attribute, attributes ]
- keywords.txt  => [ function, func, method, class, object, obj, variable, var, keyword ]

#### Example

**lib/fathead/jquery/cover/methods.txt**:
```txt
.add
.addBack
.addClass
.after
...
```

**Generated Redirects**:
- .add method, .add function, .add func, .add subroutine
- .addBack method, .addBack function, .addBack func, .addBack subroutine
- .addClass method, .addClass function, .addClass func, .addClass subroutine
- .after method, .after function, .after func, .after subroutine

## Effective redirects

Full coverage is great, but how do people then find your articles? The Fathead system is fast because it is simple - you need an exact match of the title in the search term.

Take a JavaScript article like [do...while](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while). The likelihood of someone searching for 'do...while' is fairly low, so you should think about what people do search for. In this instance, redirects to this article from 'do' and 'while' would be a strong start.

**Common redirects:**

- Article names with punctuation stripped and replaced by spaces (e.g. "array.length" would have an "array length" redirect)
- Camel case split into two lowercase words (e.g. "camelCase" would have a "camel case" redirect)
- Adding the reference category to the article title (e.g. "or" would become "or logical operator")

Try also thinking about what are the peculiarities of the language you're working on, and how people usually search for reference.
For instance, in jQuery we have the following additional redirects:
- "on" + the event name ("on click")
- event name + "event" ("click event")
- $.[method] instead of jQuery.[method] ("$.ajax()")

**Future steps :** Work is in progress on creating as many of these redirects automatically as possible, as well as feeding back common query misses to developers.


## Valid output

Any invalid entries in output.txt will be stripped from your Fathead on release. You should take steps to minimise invalid entries in output.

**Common Errors :**
- Field count
- Title duplication
- Escaping
- Disambiguation syntax
- Disambiguation titles not existing as articles
- Category titles clashing with article titles


## Testing

To help you measure feature coverage and validity of your Fathead's output, a test exists to check for common issues and feature coverage. You can run this from the **zeroclickinfo-fathead** repository like so:

```bash
DDG_TEST_FATHEAD=<your fathead> prove --quiet t/validate_fathead.t 1>/dev/null
```

...where "`your fathead`" is the name of your fathead's directory in `lib/fathead/`. This will provide detailed output on potential errors in your Fathead's output.txt file.

**NB:** Ensuring these tests pass is not a prerequisite for your Fathead to be merged. It is purely a helper to assist developers and reviewers to measure the potential effectiveness of their Fatheads.
