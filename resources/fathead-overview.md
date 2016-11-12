# Fathead Instant Answers

Fatheads are key-value Instant Answers backed by a database. The keys of the database are typically words or phrases, and they are also the exact queries that will trigger the the Instant Answer. When a database key is queried, the corresponding row from the database is returned, which is typically a paragraph of text.

Developing a Fathead Instant Answer entails writing a program that generates an **output.txt** file. This tab-delimited file indicates the keys and values for the database, as well as some other important information discussed below. The program may be written in Perl, Python, JavaScript, or Ruby, and if necessary, will be run periodically to keep the database current.

The **output.txt** file that is generated will be consumed by the DuckDuckGo backend, cleaned up (details below) and then finally entered into an SQL database.


## Fathead Directory Structure

Each Fathead Instant Answer has its own directory, which contains several files. **The name of the fathead directory must match the ID associated with the Instant Answer**.

Here is an overview of the files typically found in the Fathead directory:

- `lib/fathead/fathead_id/fetch.sh` &ndash; a shell script called to fetch the data.

- `lib/fathead/fathead_id/download/` &ndash; a directory to hold temp files created by fetch.sh

- `lib/fathead/fathead_id/parse.xx` &ndash; the script used to parse the data once it has been fetched. .xx can be `.pl`, `.py`, `.rb`, or `.js`.

- `lib/fathead/fathead_id/parse.sh` &ndash; a shell script wrapper around parse.xx

- `lib/fathead/fathead_id/README.txt` &ndash; Please include any dependencies here, or other special instructions for people trying to run it. Currently, Fathead Instant Answers require some hand work by DuckDuckGo staff during integration.

- `lib/fathead/fathead_id/output.txt` &ndash; the output file. It generally should **not** be committed to github, but may be committed if it is small (<1MB).

- `lib/fathead/fathead_id/data.url` &ndash; an optional pointer to a URL in the cloud somewhere, which contains the data to process.

- `lib/fathead/fathead_id/requirements.txt` &ndash; an optional file outlining the required packages for Fatheads writtein in Python


## Data File Format

Please name the output file `output.txt` (tab delimited) but do not store the file in the Fathead directory (as noted above) **unless it is under 1MB**.

The output file needs to use UTF-8 encoding so we can process it. Please make sure you write your parse scripts accordingly or we'll likely run into some problems getting it integrated.

The output format from `parse.xx` depends on the type of content. In any case, it should be a tab delimited file, with **one line per entry**. All newline characters (e.g. `\n`, `\r\n`) must be replaced with an escaped newline, i.e. `\\n`.  Any literal newlines (e.g. the string '\n' inside a code snippet) must be replaced with a double escaped newline, i.e, `\\\\n`.

#### Example

To render this:

```html
<pre><code>bprint("Hello World\n");</code></pre>
Hello World in QuakeC (QuakeC.qc)
```

Your output.txt should look like this:

```html
<pre><code>bprint("Hello World\\n");</code></pre>\nHello World in QuakeC (QuakeC.qc)
```

This can be done with two simple regular expression:
 - `s/\\n/\\\\n/g` (to escape literal newlines)
 - `s/\r?\n+/\\n/g` (to create escaped newlines)


### Output Fields

Every line in the output file must contain thirteen fields, separated by tabs. Some of the fields may be empty. The fields are as follows:

  1. Full article title: This must be unique across the data set of this Instant Answer. *This field is required*  
  Example: `border-right`

  2. Type of entry: `A` for articles, `D` for disambiguation pages (displays a list of articles), or `R` for redirects (). *This field is required*

  3. *For redirects only* - An alias for a title such as a common variation. The format is the full title of the Redirect.  
  Example: `border-right property` (this would ensure a search for "border-right property" displays the same result as a search for "border-right")

  4. *Leave this field empty*

  5. Categories: An article can have multiple categories, and category pages will be created automatically. An example of a category page can be seen at https://duckduckgo.com/c/css_pseudo_elements. The maximum number of items in a single category is 750. Multiple categories must be separated by an escaped newline, `\\n`. Categories should generally end with a plural noun.  
  Examples: `css properties`, `css properties\\ncss box model`

  6. *Leave this field empty*

  7. Related topics. One or more article titles, that are related to the article. This will be turned into a list of links displayed beside the answer.  
  Example: For the CSS `border-right` article, we should have `[[border-right-color]]\\n[[border-right-style]]\\n[[border-right-width]]`. If you want to display different text for the link use a `|` to separate the display text from the article title: `[[Specifying Right-Border Color|border-right-color]]`.

  8. *Leave this field empty*

  9. External links: These will be displayed first when an article is shown. The canonical example is an official site, which looks like `[$url Official site]\\n`. You can have several, separated by an escaped newline, though only a few will be used. You can also have before and after text or put multiple links in one.  
  Example: `Before text [$url link text] after text [$url2 second link].\\n`

  10. *For disambiguation pages only* - Content of disambiguation page: Should be a list, where each item is an article title, followed by a one sentence description ending in a period. The items must be separated by `\n*`.  
  Example: We should disambiguate the query `css repeating gradient` by showing all the relevant articles: `*[[repeating-vertical-gradient]], The CSS repeating-linear-gradient function creates an <image> consisting of repeating gradients.\n*[[repeating-radial-gradiient]], This works similarly to the standard radial gradients as described by radial-gradient(), but it automatically repeats the color stops infinitely in both directions, with their positions shifted by multiples of the difference between the last color stop's position and the first one's position.`

  11. Image. You can reference one external image that we will download and reformat for display.  
  Example: `[[Image:$url]]`

  12. Abstract. This is the main content, it should contain all the information you wish to display. Abstracts related to technical documentation must be formatted appropriately. More details below!  
  Example: `<section><p>The non-standard ::-moz-list-bullet Mozilla CSS pseudo-element is used to style the bullet of a list element.</p><pre><code>li::-moz-list-bullet { style properties }</code></pre></section>`

  13. URL. This is the full URL for the source. Ideally the URL should be specific to the article so more information about the result is easily accessible. Relative URLs will have the `source_domain` from the metadata prepended to them.  
  Example: `https://developer.mozilla.org/en-US/docs/Web/CSS/border-right`



An example snippet from parse.xx written in [Perl](https://duckduckgo.com/Perl) may look like this:

``perl

my $title = $line[0] || '';
my $type = $line[1] || '';
my $redirect = $line[2] || '';
my $otheruses = $line[3] || '';
my $categories = $line[4] || '';
my $references = $line[5] || '';
my $see_also = $line[6] || '';
my $further_reading = $line[7] || '';
my $external_links = $line[8] || '';
my $disambiguation = $line[9] || '';
my $images = $line[10] || '';
my $abstract = $line[11] || '';
my $source_url = $line[12] || '';

print "$title\t$type\t\t\t$categories\t\t$see_also\t\t$external_links\t$disambiguation\t$images\t$abstract\t$source_url\n";
``

There is a pre-process script that is run on this output, which:

- Removes duplicates (on `$title`)
- Reduces `$abstract` to one sentence (optional)
- Drops records that look like spam (optional)
- Normalizes spacing
- Makes sure the `$abstract` ends in a period (optional)

**Note:** Some elements of the pre-process script are configurable from the Fatheads metadata, specified on the Instant Answer Page.


## Formatting the Abstract:

- Make sure to wrap the entire abstract in a `<section class="prog__container"></section>` tag
- All headers should be wrapped in a `<span class="prog__sub"></span>` element
- Code snippets should be wrapped in `<pre><code></code></pre>` tags
- Descriptions should go inside `<p></p>` tags, before the code snippets

#### Example Markup:

```html
<section class="prog__container">
    <p>Creates a JavaScript Date instance that represents a single moment in time.</p>
    <pre>
        <code>
            new Date;
            new Date(value);
            new Date(dateString);
            new Date(year, month[, day[, hour[, minutes[, seconds[, milliseconds]]]]]);
        </code>
    </pre>
    <span class="prog__sub">Return Value</span>
    <p>The removed element.</p>
</section>
```

Multiline code blocks should also contain escaped newlines, `\n`, to separate lines:

```html
<pre><code>functions(){\n    console.log("Hello World");\n}</code></pre>
```

### Notes

There should be no duplicates in the `$title` (first) field. If you have multiple articles with the same title you will mostly liked need to create a disambiguation entry. However, if the content is related you can group the content into a single article, or have your parsing script use only the most important article.


## Instant Answer Page Fields

Part of [submitting](http://docs.duckduckhack.com/submitting/submitting-overview.html) your Fathead Instant Answer involves creating an [Instant Answer Page](https://duck.co/ia/new_ia). Here is how to fill out several **meta fields** you may encounter:

![](http://docs.duckduckhack.com/assets/fathead-fields.png)

### Source Domain

Specifies the domain name which this Fathead's data came from. For example, the [MDN CSS](https://duck.co/ia/view/mdn_css) Fathead has the Source Domain: 'https://developer.mozilla.org'.

### Source Name

Specifies the written name for the `Source Domain`. This name will be used for the "More at" link at the bottom of each Fathead result. For example, the [MDN CSS](https://duck.co/ia/view/mdn_css) Fathead has the Source name: 'Mozilla Developer Network'. This should be a recognizable name users can identify to understand where the data is from, and where they will be taken when they click the name.

### Source Info

Specifies the name of the language, or library this Fathead is related to. This term is used as the subtitle for Fathead Articles. E.g. "JavaScript" or "macOS"

If you can find some pages like that make sure you input the name of the page in this field.
