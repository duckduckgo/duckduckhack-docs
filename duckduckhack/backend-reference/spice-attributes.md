# Spice Attributes (Perl)

## Spice `to`

This attribute defines the API endpoint for your Instant Answer. E.g.

```perl
spice to => 'http://example.com/search/$1?loc=$2';
```

A GET request will be made to this URL to retrieve data. The **$1** and **$2** in the URL are values captured from the regular expression defined by `spice from`, which has a default value of `(.*)`. See the full documentation of `spice from` below for more information.

## Spice `from`

The `spice from` attribute defines a regular expression which groups data returned from the `handle` function. All parameters returned from the `handle` function in a Spice are converted into strings and joined with a `/`. Here's an example:

```perl
handle remainder => sub {
  # Produces the string "foo/bar/baz"
  return "foo", "bar", "baz";
}

# Captures three groups separated by a forward slash
spice from => '(.*)/(.*)/(.*)';
```

In the above example, the values returned from `handle` are passed to `spice from` as "foo/bar/baz", which then matches the regex and passes the parameters to `spice to`, where `$1 = "foo"`, `$2 = "bar"`, and `$3 = "baz"`. `spice to` then uses these parameters to handle the API request.

By default, `spice from` has a value of `(.*)`, which sends all parameters from the `handle` function to `spice to` in a single group, **$1**.

## Spice `wrap_jsonp_callback`

If the API used for your Instant Answer does not support JSONP (ie. it doesn't provide a URI parameter to indicate the callback function to be used on the API response), set `wrap_jsonp_callback` to true and the API response will automatically be wrapped in the appropriate function call for your Instant Answer.

## Spice `proxy_cache_valid `

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Spice `is_unsafe`

If your Instant Answer has the potential to return unsafe results (eg. contains vulgar words, crude humour) the `is_unsafe` flag must be set to true. Any Instant Answers that have `is_unsafe` set to true can only be seen when a user has safe-search turned off, or when they add the phrase `!safeoff` to their query (eg. "automeme !safeoff").
