# Fathead Instant Answers

Fatheads are key-value Instant Answers backed by a database. The keys of the database are typically words or phrases, and they are also used as the triggers for the Instant Answer. When a database key is queried, the corresponding row from the database is returned, which is typically a paragraph of text. Developing a Fathead Instant Answer entails writing a program that generates an **output.txt** file. This tab-delimited file indicates the keys and values for the database, as well as some other important information discussed below. The program may be written in Perl, Python, JavaScript, or Ruby, and if necessary, will be run periodically to keep the database current.

The **output.txt** file that is generated will be consumed by the DuckDuckGo backend, cleaned up (details below) and then finally entered into an SQL database.

## Structure

Each Fathead Instant Answer has its own directory, which looks like this:

- ``lib/DDG/Fathead/FatheadName.pm`` &ndash; a Perl file that lists some meta information about the Instant Answer

- ``share/fathead/fathead_name/fetch.sh`` &ndash; a shell script called to fetch the data.

- ``share/fathead/fathead_name/download/`` &ndash; a directory to hold temp files created by fetch.sh

- ``share/fathead/fathead_name/parse.xx`` &ndash; the script used to parse the data once it has been fetched. .xx can be .pl, .py, .rb, .js, etc. depending on what language you use.

- ``share/fathead/fathead_name/parse.sh`` &ndash; a shell script wrapper around parse.xx

- ``share/fathead/fathead_name/README.txt`` &ndash; Please include any dependencies here, or other special instructions for people trying to run it. Currently, Fathead Instant Answers require some hand work by DuckDuckGo staff during integration.

- ``share/fathead/fathead_name/output.txt`` &ndash; the output file. It generally should **not** be committed to github, but may be committed if it is small (<1MB).

- ``share/fathead/fathead_name/data.url`` &ndash; an optional pointer to a URL in the cloud somewhere, which contains the data to process.


## Data File Format

Please name the output file output.txt (tab delimited) but do not store the data file(s) in the repository (as noted above) unless it is under 1MB.

The output file needs to use UTF-8 encoding so we can process it. Please make sure you write your parse scripts accordingly or we'll probably run into some problems getting it integrated.

The output format from `parse.xx` depends on the type of content. In any case, it should be a tab delimited file, with one line per entry. Usually there is no need for newline characters, but if there is a need for some reason, escape them with a backslash like `\\\n`. If you want a newline displayed, use `<br>`

Every line in the output file must contain thirteen fields, separated by tabs. Some of the fields may be empty. The fields are as follows:

  1. Full article title. Must be unique across the data set of this Instant Answer. *This field is required.* Examples: `Perl`

  2. Type of article. `A` for actual articles, `D` for disambiguation pages, or `R` for redirects. *This field is required.*

  3. *For redirects only.* An alias for a title such as a common misspelling or AKA. The format is the full title of the Redirect, e.g., DuckDuckGo. Examples: `Duck Duck Go -> DuckDuckGo`

  4. *Ignore.*

  5. Categories. An article can have multiple categories, and category pages will be created automatically. An example of a category page can be seen at [http://duckduckgo.com/c/Procedural_programming_languages](http://duckduckgo.com/c/Procedural_programming_languages). Multiple categories must be separated by an escaped newline, `\\n`. Categories should generally end with a plural noun. Examples: `Procedural programming languages\\n`

  6. *Ignore.*

  7. Related topics. These will be turned into links in the Zero-click Info box. Examples: `[[Perl Data Language]]`. If the link name is different, `[[Perl Data Language|PDL]]`.

  8. *Ignore.*

  9. External links. These will be displayed first when an article is shown. The canonical example is an official site, which looks like ``[$url Official site]\\n``. You can have several, separated by an escaped newline, though only a few will be used. You can also have before and after text or put multiple links in one. Examples: ``Before text [$url link text] after text [$url2 second link].\\n``

  10. *For disambiguation pages only.* Content of disambiguation page. Should be a list, where each item is a link to a page followed by a one sentence description ending in a period. The items have to be separated by ``\n``. Examples: ``*[[Enum.value]], returns the value part of the Enum.\n*[[Pair.value]], returns the value part of the Pair.``

  11. Image. You can reference an external image that we will download and reformat for display. Examples: ``[[Image:$url]]``

  12. Abstract. This is the snippet info. It should generally be ONE readable sentence, ending in a period. Examples: ``Perl is a family of high-level, general-purpose, interpreted, dynamic programming languages.``

  13. URL. This is the full URL for the source. If all the URLs are relative to the main domain, this can be relative to that domain. Examples: `http://www.perl.org`



An example snippet from parse.xx written in [Perl](https://duckduckgo.com/Perl) may look like this:

```perl

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
```

There is a pre-process script that is run on this output, which:

* Drops duplicates (on `$title`).

* Reduces `$abstract` to one sentence.

* Drops records that look like spam.

* Normalizes spacing.

* Makes sure the `$abstract` ends in a sentence.


## Code Blocks

If you want to include a code snippet or another pre-formatted example in the abstract, like the [perl](https://duckduckgo.com/?q=perl+open) Fathead, wrap the code block like this:

```html
<pre><code>code block goes here</code></pre>
```

For multiline code snippets, use only `\n` to separate lines:

```html
<pre><code>foo\nbar\nbaz</code></pre>
```

## Notes

There should be no duplicates in the `$page` (first) variable. If you have multiple things named the same thing you have a number of options:
  - make disambiguation pages
  - put everything in one snippet
  - pick the most general one
