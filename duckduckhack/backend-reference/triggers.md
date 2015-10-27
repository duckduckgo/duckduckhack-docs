# Triggers

Triggers tell DuckDuckGo on which search queries to initiate an Instant Answer. There are two types of triggers, **words** and **regex**. 

The two types of triggers cannot be combined, but you may consider a third option of [Regex Guards](#regex-guards). We insist that you use word triggers whenever possible as they are simpler and faster.

## Word Triggers

Word triggers specify *what* to look for, and *where* to look for it:

```perl
triggers <location> => <array of words and phrases>
```

For example:

```perl
triggers start => "stackoverflow", "stack overflow", "SO";
```

You may find the [qw](http://perlmeme.org/howtos/perlfunc/qw_function.html) function convenient:

```perl
@triggers = qw(john jacob jingleheimer schmidt);
triggers any => @triggers;
```

You can also use multiple trigger statements together:

```perl
triggers start => "tv", "television";
triggers end => "schedule", "hours";
```

### Word Trigger Locations

- `start` &mdash; Word exists at the start of the query
- `end` &mdash; Word exists at the end of the query
- `startend` &mdash; Word is at the beginning or end of the query
- `any` &mdash; Word is anywhere in the query

**Note:** You can combine several trigger statements if, for example, you want certain words or phrases to be **startend** but others to be **start**. The [Average Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Average.pm#L5) demonstrates the usage of multiple Word trigger statements.

## Regex Triggers

***We insist that you use word triggers whenever possible as they are simpler and faster.*** 

***Note that you cannot combine the use of Regex Triggers with Word Triggers.***

Regex triggers specify *which version of the query*, and a *regular expression* to apply.

```perl
triggers <query_format> => <regular expression>
```

<!-- /summary -->

#### Examples

```perl
triggers query_lc => qr/trigger (?:my|your|our) instant answer/;
```

or

```perl
my $regex = qr/^this is an? instant answer regexp$/;
triggers query_raw => $regex;
```

#### Query Formats

- `query_raw` &mdash; The query in its original form, with whitespace and case preserved
- `query` &mdash; Uniformly whitespaced version of `query_raw`
- `query_lc` &mdash; Lowercase version of `query`
- `query_nowhitespace` &mdash; `query` with all whitespace removed
- `query_clean` &mdash; `query_lc`, but with whitespace and non-alphanumeric ascii removed

## Regex Guards

Trigger words are coarse filters; they may send you queries you cannot handle. Your Instant Answer should return nothing in these cases.  As such, you generally need to further qualify the query in your code.

We much prefer you use Word Triggers when possible because they are faster on the backend. In some cases however, **regular expressions** are necessary, e.g., you need to trigger on sub-words. In this case we suggest you consider using a **word trigger** and supplement it with a **regex guard**. A regex guard is a return clause immediately inside the `handle` function.

A good example of this is the Base64 goodie. In this case we want to trigger on queries with the form "base64 encode/decode \<string\>". Here's an excerpt from [Base64.pm](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base64.pm) which shows how this case is handled using a word trigger, with a regex guard:

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


## Triggers in Multiple Languages 

We have plans to make it possible to trigger Instant Answers in many different languages. Until an internationalization mechanism is place, to uphold maintainability and consistency, **we cannot accept pull requests that add languages directly in the code.**