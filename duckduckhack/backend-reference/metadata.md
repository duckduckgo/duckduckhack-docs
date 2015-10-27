# Instant Answer Metadata

Including metadata helps us to categorize and describe your Instant Answer. This document explains the different types of metadata that you may add to the source code of your Instant Answer.

Metadata is added to your Instant Answer Perl file, above the triggers. For example, the ["Alternative To" Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/AlternativeTo.pm) has the following metadata:

```perl
name "AlternativeTo";
primary_example_queries "alternative to notepad";
secondary_example_queries "alternative to photoshop for mac", "free alternative to spotify for windows";
description "Find software alternatives";
icon_url "/i/alternativeto.net.ico";
source "AlternativeTo";
code_url "https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/AlternativeTo.pm";
topics  "everyday", "programming";
category  "computing_tools";
attribution github => ['https://github.com/Getty','Torsten Raudssus'],
           twitter => ['https://twitter.com/raudssus','Torsten Raudssus'];
```

Metadata will be used in several places relating to your Instant Answer, including its [IA Page](https://duck.co/ia/view/alternative_to). Below is an explanation of each available property.

------

## `name`

A unique name for this Instant Answer.

While this can be arbitrary, it is considered good practice to have the chosen name be similar to the Perl package in which it is contained, e.g., DDG::Spice::RedditSubSearch.

```perl
name "Subreddit Search";
```

## `source`

The name of the data source used for your Instant Answer.

```perl
source "Reddit";
```

## `icon_url` (optional)

The favicon URL for the data source used.

**Note:** The favicon is not always located at `http://domain/favicon.ico`. It is often given as an explicit URL in the HTML header as `x-icon`, `apple-touch-icon` or similar.

Favicons can sometimes be found by searching for the data source on DuckDuckGo. If a favicon exists, we will display it beside any results from that domain. Feel free to use our link from there.

```perl
icon_url "http://www.reddit.com/favicon.ico";
```

or, for DuckDuckGo-sourced favicons,

```perl
icon_url "/i/reddit.com.ico";
```

## `description`

A succinct explanation of what the Instant Answer does. For clarity, *exclude* the source name if possible.

```perl
description "Search for Subreddits";
```

## `primary_example_queries`

Examples of the most common types of queries which will trigger the Instant Answer.

```perl
primary_example_queries "/r/pizza", "subreddit nature";
```

## `secondary_example_queries` (optional)

Examples of other, less common, trigger words or phrases for the Instant Answer, if applicable.

```perl
secondary_example_queries "r/accounting";
```

## `category`

The category into which your Instant Answer best fits.

<!-- /summary -->

Supported categories include:

- bang
- calculations
- cheat_sheets
- computing_info
- computing_tools
- conversions
- dates
- entertainment
- facts
- finance
- food
- formulas
- forums
- geography
- ids
- language
- location_aware
- physical_properties
- programming
- q/a
- random
- reference
- special
- software
- time_sensitive
- transformations

**Note:** Instant Answers may specify ***exactly one*** category.

```perl
category "forums";
```

## `topics`

A list of the topics to which your Instant Answer applies.

<!-- /summary -->

Supported topics include:

- everyday
- economy\_and\_finance
- computing
- cryptography
- entertainment
- food_and_drink
- gaming
- geek
- geography
- math
- music
- programming
- science
- social
- special_interest
- sysadmin
- travel
- trivia
- web_design
- words\_and\_games

**Note:** Instant Answers may specify ***multiple*** topics.

```perl
topics "social", "entertainment", "special_interest";
```

## `code_url`

URL for the Instant Answer code on github.

```perl
code_url "https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RedditSubSearch.pm";
```

## `attribution`

Information about you, the author.

<!-- /summary -->

Supported attribution sources include:

- email
- twitter
- web
- github
- facebook
- cpan

**Note:** For each attribution type, you may provide either a single string or an array reference with two values.

If a single string is given, it will be used to create a link to the defined profile and **also** serve as the **text** for the link.

When an array reference is provided, the first element will be used to create the link while the second will be used as the text for the link.

The same attribution type can appear multiple times if necessary, for example when there is more than one contibutor.

```perl
attribution twitter => "mithrandiragain",
            github  => ["MithrandirAgain", "Gary Herreman"],
            web     => ['http://atomitware.tk/mith', 'MithrandirAgain'],
            github  => ["jarmokivekas", "Jarmo Kivekas"];
```
