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
- `query_clean` &mdash; `query_lc`, but with whitespace and non-alphanumeric ASCII removed

## Triggers in Multiple Languages

We have plans to make it possible to trigger Instant Answers in many different languages. Until an internationalization mechanism is place, to uphold maintainability and consistency, **we cannot accept pull requests that add languages directly in the code.**
