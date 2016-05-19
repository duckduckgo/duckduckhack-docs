# Handle Functions

[Triggers](http://docs.duckduckhack.com/backend-reference/triggers.html) are coarse filters; they may send you queries you cannot handle. By defining a *handle function* you can tell your Instant Answer on which triggered search queries to run - or not.

A simple handle function, below, checks if the query *remainder* has anything in it. If not, it returns `undef`.

```perl
handle remainder => sub {
    return if $_ eq ''; # Explicitly check for the empty string
    return $_;
};
```

## Handle Function Return Values

In a Spice, the handle function returns a value that will be inserted as the parameter to the API call. 

In a Goodie, the handle function returns the actual answer.

To stop the Instant Answer from proceeding, a handle function simply returns nothing, e.g. `return;`

## Handle Function Handlers

A handle function takes a handler - a pre-packaged part of the query - that it can use to determine whether the Instant Answer should run or not. 

**When you choose a handler, you're choosing which input to pass to your handle function.** For example, passing `query_lc` means that `query_lc` is passed as the input to the function so the value of `query_lc` (a string) is available in `$_`:

```perl
handle query_lc => sub {
    my $lowercased_query = $_;
}
```

However, `words` and `matches` return an array - these values will be available in the default array variable, `@_`:

```perl
handle words => sub {
   my @words_array = @_;
   my $first_word = shift;
};
```

The available handlers are:

- `remainder` -  The query without the trigger words, spacing and case are preserved

- `remainder_lc` - Like remainder but in lowercase

- `query_raw` -  Like remainder but with trigger words intact

- `query` -  Full query normalized with a single space between terms

- `query_lc` -  Like query but in lowercase

- `query_clean` -  Like query_lc but with non-alphanumeric characters removed

- `query_nowhitespace` -  All whitespace removed

- `query_nowhitespace_nodash` -  All whitespace and hyphens removed

- `matches` -  Returns an array of captured expression from a regular expression trigger

- `words` -  Like query_clean but returns an array of the terms split on whitespace

- `query_parts` -  Like query but returns an array of the terms split on whitespace

- `query_raw_parts` -  Like query_parts but array contains original whitespace elements

## Accessing the Original Query

Inside the handle function you have access to the various attributes of the original query (the `DDG::Request` instance) in a variable called `$req`. For example, `$req->query`, `$req->query_lc`, `$req->query_raw`, `$req->remainder`, and so on.

This can be useful in determining whether your Instant Answer should run. For example, in [`GoWatchIt.pm`](https://github.com/duckduckgo/zeroclickinfo-spice/blob/d53dcf3842c337a626405af2bff0be28d85c1fd2/lib/DDG/Spice/GoWatchIt.pm#L22), the handle function aborts if the query contains words in a "stop words" array (defined at the top of the file):

```perl
	return if grep {$req->query_lc eq $_} @stopwords;
```

## Accessing Location and Language Information

Inside the handle function you also have access to `$loc` for location data, and `$lang` for language related attributes. Learn more about these two useful: [Language and Location Reference](http://docs.duckduckhack.com/backend-reference/language-location-apis.html).

## Regex Guards in Handle Functions

We much prefer you use [trigger words](http://docs.duckduckhack.com/backend-reference/triggers.html) when possible because they are faster on the back end. In some cases however, **regular expressions** are necessary, e.g., you need to determine whether a query is suitable beyond the trigger words.

In this case we suggest you consider using [triggers](http://docs.duckduckhack.com/backend-reference/triggers.html) as much as you can, supplemented with a **regex guard** in your handle function. A regex guard is a conditional return statement at the very beginning of your handle function.

A good example of this is the Base64 Goodie. In this case we want to trigger on queries with the form "base64 encode/decode \<string\>". Here's an excerpt from [Base64.pm](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base64.pm) which shows how this case is handled using a word trigger, with a regex guard:

```perl
triggers startend => "base64";

handle remainder => sub {
    return unless $_ =~ /^(encode|decode|)\s*(.*)$/i;
```

Another example, the [Base Goodie's](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base.pm) has a `return` statement paired with an `unless` right on the first line of its `handle` function:

```perl
handle remainder => sub {
  return unless  /^([0-9]+)\s*(?:(?:in|as)\s+)?(hex|hexadecimal|octal|oct|binary|base\s*([0-9]+))$/;
  ...
}
```
