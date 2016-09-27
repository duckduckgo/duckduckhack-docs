# Creating Effective Fatheads

While on the surface Fatheads appear simple, there are a few steps you can take toward increasing your Fathead's query coverage and accuracy.

This article will run through some of these, using examples drawn from creating programming IAs.


## Full topic coverage

A strong first step in planning your Fathead is to gather the set of articles you wish to provide coverage for.

Firstly, you can check index pages and content menus for lists of content you can incorporate. For example, the navigation menu on the left of [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/) pages has a list of language entities under "References:". Taking note of these and ensuring they are all processed by your parser will go a long way in increasing coverage.

We also suggest you create a `cover/` directory containing text files that list all the topic titles you intend to cover. These lists will then be used as Unit tests to help you measure your Fathead's coverage. Using the example of a programming language Fathead, this list should come from a source separate to the Fathead source. For example, if using MDN you could use the [list of reserved keywords from the ECMA specification](http://ecma-international.org/ecma-262/6.0/#sec-keywords).

These files should be categorised by entity type to aid validation and Fathead redirect creation.

### Example
The Perl Fathead serves as a great example. It has two lists covering functions and special variables. The lists can be seen [here](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/c441e54d98b92cabce04154774cfbae485da63bd/lib/fathead/perl_doc/cover).


## Effective redirects

Full coverage is great, but how do people then find your articles? The Fathead system is fast because it is simple - you need an exact match of the title in the search term.

Take a JavaScript article like [do...while](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while). The likelihood of someone searching for 'do...while' is fairly low, so you should think about what people do search for. In this instance, redirects to this article from 'do' and 'while' would be a strong start.

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


**Formatting the content:**
- Make sure to wrap the whole content to be displayed in a `<div class="prog__container"></div>` element
- All headers should be wrapped in a `<div class="prog__sub"></div>` element
- Code snippets should be wrapped in `<pre><code></code></pre>` tags
- Descriptions should go inside `<p></p>` tags, before the code snippets

Example:
```html
<div class="prog_container"> 
    <div class="prog__sub">Header</div>
    <p>Desc</p> 
    <pre>
        <code>Code</code>
    </pre> 
</div>
```

## Testing

To help you measure feature coverage and validity of your Fathead's output, a test exists to check for common issues and feature coverage. You can run this from the **zeroclickinfo-fathead** repository like so:

```bash
DDG_TEST_FATHEAD=<your fathead> prove --quiet t/validate_fathead.t 1>/dev/null
```

...where "`your fathead`" is the name of your fathead's directory in `lib/fathead/``. This will provide detailed output on potential errors in your Fathead's output.txt file.

**NB:** Ensuring these tests pass is not a prerequisite for your Fathead to be merged. It is purely a helper to assist developers and reviewers to measure the potential effectiveness of their Fatheads.
