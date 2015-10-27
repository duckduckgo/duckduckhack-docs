# API Reference

## API Criteria

With millions of search queries triggering Instant Answers every day, it's important to choose APIs wisely. There are several criteria for APIs used in Spice Instant Answers.

### Technical constraints

- APIs called by Spice Instant Answers **must use the JSON or JSONP formats**. We do not support the use of XML (it's coming soon though!), HTML, or plain text responses.
- APIs should respond to requests in **less than one second** (< 1s).
- Avoid **static JSON files**. These often have large payloads and require heavy local processing. Not sure? [Talk to us about your idea](mailto:open@duckduckgo.com).

### Reliability

- APIs used should be **reliable**. Pick sources that will be most likely be around and accurate for the foreseeable future.
- APIs created by contributors solely for the purpose of an Instant Answer cannot be accepted.

### Credibility

- APIs used should represent the **most credible source** for the information. This means it should draw upon the preferred data source of the relevant community. Look for posts and sources like [these](https://duck.co/forum/thread/37/great-resources-for-instant-answer-ideas) which have been suggested by others. 
- APIs must have the appropriate permissions or rights to serve their information.

## Multiple API endpoints

Learn how to handle multiple API endpoints when developing a DuckDuckGo Instant Answer.

[Watch video on Vimeo](https://vimeo.com/137152536)

![https://vimeo.com/137152536](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fscreencast_multiple-endpoints.jpg&f=1)

## Multiple Placeholders in API URL

If you need to substitute multiple parameters into the API call you can use the **Spice from** keyword. In the following example, the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm) uses two numbers to specify the min and max length of the random word:

```perl
spice from => '(?:([0-9]+)\-([0-9]+)|)';
```

Whatever you return from the handle function gets sent to this **spice from** regexp, which then gets fed into the **spice to** API:

For example, if your `handle` function looked like this:

```perl
handle remainder => sub {
  ...
  if ( $foo ){
    my $minMax = "10-100"
    return $minMax;
  }
  return;
}
```

Then the the string `10-100` would be sent to the `spice from` regexp, which would capture the two numbers into `$1` and `$2`. These two placeholders are then used to replace `$1` and `$2` in the `spice to` URL:

```perl
spice to => 'http://api.wordnik.com/v4/words.json/randomWord?minLength=$1&maxLength=$2&api_key={{ENV{DDG_SPICE_WORDNIK_APIKEY}}}&callback={{callback}}';
```

**Note:** The reason why you do not need to specify a **from** keyword by default, is that the default value of `spice from` is **(.*)**, which means whatever you return gets gets captured into `$1`.

## Passing Multiple Values to Spice From

You can have multiple return values in your handle function like the [AlternativeTo Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/AlternativeTo.pm).

```perl
return $prog, $platform, $license;
```

In this case they are URL encoded and joined together with '/' chars, e.g., in this case **$prog/$platform/$license**. Then that full string is fed into the **spice from** regexp.

```perl
spice from => '([^/]+)/?(?:([^/]+)/?(?:([^/]+)|)|)';
```

## API Keys

Some APIs require API keys to function properly like in the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm). You can insert an API key for testing in the callback function and replace it with a variable reference when submitting. The API key variable should be named using the provider name as a reference. As Wordnik is the API provider used for the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm) we use `DDG_SPICE_WORDNIK_APIKEY` as the variable name.

```perl
spice to => 'http://api.wordnik.com/v4/words.json/randomWord?minLength=$1&maxLength=$2&api_key={{ENV{DDG_SPICE_WORDNIK_APIKEY}}}&callback={{callback}}';
```

You can set the variable when you start DuckPAN server like this:

```bash
DDG_SPICE_WORDNIK_APIKEY=xyz duckpan server
```

Alternatively you can save the API key variable in the `env.ini` file, which DuckPAN will load on start, using:

```bash
duckpan env set DDG_SPICE_WORDNIK_APIKEY xyz
```

## JSON -> JSONP

Some APIs don't do JSONP by default, i.e. don't have the ability to return the JSON object to a callback function. In this case, first you should try to contact the API provider and see if it can be added. Where it cannot, you can tell us to wrap the JSON object return in a callback function like in the [XKCD Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Xkcd.pm).

```perl
spice wrap_jsonp_callback => 1;
```

## Caching

Spice Instant Answers have two forms of caching: API Response caching (remembers the JSON returned from the API) and API Call caching (remembers the API call URL created for a given query). Both of these will be explained with examples.

<!-- /summary -->

### Caching API Responses

By default, we cache API responses for for **24 hours**. We use [nginx](https://duckduckgo.com/?q=nginx) and get this functionality by using the [proxy_cache_valid](http://wiki.nginx.org/HttpProxyModule#proxy_cache_valid) directive. You can override our default behavior by setting your own `spice proxy_cache_valid` directive like in the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm):

```perl
spice proxy_cache_valid => "200 304 1d";
```

This will cache any HTTP 200 and 304 responses for 1 day. You can also force API responses to **not** be cached like so:

```perl
spice proxy_cache_valid => "418 1d";
```

This is a special declaration that will only cache [418 HTTP](https://duckduckgo.com/?q=HTTP+418) return values for 1 day. Since regular return codes are [200](https://duckduckgo.com/?q=HTTP+200) and [304](https://duckduckgo.com/?q=HTTP+304), nothing will get cached.

If you expect API response to change very frequently you should lower the caching time. As well, if your API is supposed to return random results (such as the RandWord spice) it makes sense to prevent all caching so every time the spice is trigger a new result will be returned.

### Caching API Calls

When a Spice triggers, its Perl code is used to construct the URL for the API call. It's likely that a given query will always map to the same API call so by default we cache the API calls for a given query for **1 hour**:

```
# This query will always make the same API call
"random word" => http://api.wordnik.com/v4/words.json/randomWord
```

Sometimes, a given query won't always require the same API call. This scenario generally arises when a Spice Instant Answer uses the Location API and uses it to append the user's location to the API call:

```
# This query will NEVER make the same API call, because the location is dynamic
"weather" => http://forecast.io/ddg?q=<user_location>
```

To **turn off** API Call caching, you must set `spice is_cached` to `0` as we do in the [Forecast](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Forecast.pm) Instant Answer:

```perl
spice is_cached => 0;
```

This way, every time the Forecast Instant Answer is triggered, **Forecast.pm** will be run, so the correct URL will be built and  the current user's location will be used for the API call.
