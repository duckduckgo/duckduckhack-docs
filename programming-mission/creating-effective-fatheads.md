# Creating Effective Reference Fatheads

While on the surface Fatheads appear simple, there are a few steps you can take toward increasing your Fathead's query coverage and accuracy.

This article will run through some of these, focusing on creating programming IAs.

## Full topic coverage

A strong first step in planning your Fathead is to gather the set of articles you wish to provide coverage for.

Firstly, you can check index pages and content menus for lists of content you can incorporate. For example, the navigation menu on the left of [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/) pages has a list of language entities under "References:". Taking note of these and ensuring they are all processed by your parser will go a long way in increasing coverage.

If creating a programming Fathead, you need to create a `cover/` directory containing one or more text files (`.txt`) that list all the topic titles and language features you need to cover (i.e. the specific keywords ). Using the example of a programming language Fathead, this list should come from a source separate to the Fathead source. For example, if using MDN you could use the [list of reserved keywords from the ECMA specification](http://ecma-international.org/ecma-262/6.0/#sec-keywords).

These lists are used in two ways:

- As Unit tests to help measure your Fathead's coverage
- To generate extra article aliases (redirects) - see below

### Example

The Perl Fathead serves as a great example. It has two lists covering functions and special variables. The lists can be seen [here](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/c441e54d98b92cabce04154774cfbae485da63bd/lib/fathead/perl_doc/cover).

### Using Coverage Data To Generate Redirects

Special filenames can be used for the file(s) in your `/cover` directory to automatically generate additional redirects (aliases) for your Fathead. The following filenames will generate redirects by prefixing, and appending the associated keywords to each article title in the file:

Filename      | Redirect Keywords
------------- | ---------------------------------------------------------------------
methods.txt   | method, function, func, subroutine
functions.txt | function, func, method, subroutine, keyword, call
variables.txt | var, variable, special variable
operators.txt | operator, function, func
tags.txt      | tag, tags, element, elements, entity, entities, attribute, attributes
keywords.txt  | function, func, method, class, object, obj, variable, var, keyword

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

Try also thinking about what are the peculiarities of the language you're working on, and how people usually search for reference. For instance, in jQuery we have the following additional redirects:

- "on" + the event name ("on click")
- event name + "event" ("click event")
- $.[method] instead of jQuery.[method] ("$.ajax()")

### Using a Redirects.txt file

Fatheads can use a `redirects.txt` file to specify additional redirects for specific articles. This file can be generated from code, or manually compiled. Each line of the file should include the name of the redirect, and the name of the original article, separated with a comma.

#### Example

```
::selection element, ::selection css pseudo element
selection element, ::selection css pseudo element
selection pseudo elements, ::selection css pseudo element
css selection element, ::selection css pseudo element
ambient lights, ambient light
ambient lights api, ambient light api
animated png, animated png (apng)
animated pngs, animated png (apng)
apngs, apng
```

#### Result

Redirect                  | Article
------------------------- | ------------------------------
::selection element       | ::selection css pseudo element
selection element         | ::selection css pseudo element
selection pseudo elements | ::selection css pseudo element
css selection element     | ::selection css pseudo element
ambient lights            | ambient light
ambient lights api        | ambient light api
animated png              | animated png (apng)
animated pngs             | animated png (apng)
apngs                     | apng

**Future steps :** Work is in progress on creating as many of these redirects automatically as possible, as well as feeding back common query misses to developers.

## Specifying Trigger Words

Fatheads can use a `trigger_words.txt` file to specify trigger words/phrases that are expected to appear before/after article titles in a query. Each line of the file should specify a unique word or phrase.

### Example

```
pyhton
python
python2
python2.6
python26
python2.7
python27
python 2
python 27
python 2.4
python 2.5
python 2.6
python 2.7
python 2.7.10
python 2.7.12
```

### Result

Given an article with a title of 'print', all of the following queries would now trigger the [Python2 Instant Answer](https://duck.co/ia/view/python2) and show a result for the `print` method:

- "pyhton print" AND "print pyhton"
- "python print" AND "print python"
- "python2 print" AND "print python2"
- "python2.6 print" AND "print python2.6"
- "python26 print" AND "print python26"
- "python2.7 print" AND "print python2.7"
- "python27 print" AND "print python27"
- "python 2 print" AND "print python 2"
- "python 27 print" AND "print python 27"
- etc...

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

To help you measure feature coverage and validity of your Fathead's output, a test exists to check for common issues and feature coverage. You can run this from the **zeroclickinfo-fathead** repository with DuckPAN like so:

```bash
duckpan test <your_fathead>
```

Alternatively, you can run:

```bash
DDG_TEST_FATHEAD=<your_fathead> prove -Ilib t/validate_fathead.t
```

...where "`your_fathead`" is the name of your Fathead's directory in `lib/fathead/`. This will provide detailed output on errors in your Fathead's `output.txt` file.

**NB:** Ensuring these tests pass is not a prerequisite for your Fathead to be merged. It is purely a helper to assist developers and reviewers to measure the potential effectiveness of their Fatheads.
