# Working with APIs

Below is a reference of how to work with special API cases. When choosing an API, there are several important criteria to keep in mind, which you can learn about in the [production guidelines](http://docs.duckduckhack.com/submitting/checklist.html#do-you-plan-to-use-an-external-data-source).

## Multiple API endpoints

Many Instant Answers construct their answers out of multiple endpoints of the same API. For example, one endpoint might list results, while another might provide in-depth details. You can work with multiple endpoints by defining them in the `alt_to` attribute in your Spice Perl package.

Defining an endpoint creates a proxy through DuckDuckGo to the API. This is exactly how the standard Spice AJAX call is proxied through DuckDuckGo, to maintain user privacy.

For example, the [Astronomy Picture of the Day](https://duck.co/ia/view/apod) Instant Answer defines the first endpoint in the standard `to` attribute, then a second endpoint inside the `alt_to` attribute:

```perl
spice to => 'http://www.astrobin.com/api/v1/imageoftheday/?limit=1&api_key={{ENV{DDG_SPICE_ASTROBIN_APIKEY}}}&api_secret={{ENV{DDG_SPICE_ASTROBIN_APISECRET}}}&format=json$1';
spice proxy_cache_valid => "200 60m";
spice wrap_jsonp_callback => 1;

spice alt_to => {
    fetch_id => {
        to => 'http://www.astrobin.com/api/v1/image/$1/?api_key={{ENV{DDG_SPICE_ASTROBIN_APIKEY}}}&api_secret={{ENV{DDG_SPICE_ASTROBIN_APISECRET}}}&format=json',
        wrap_jsonp_callback => 1
    }
};
```

The contributor gave the second endpoint the name `fetch_id`. As a result, the corresponding [JavaScript code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/astrobin/apod/astrobin_apod.js) can call on an endpoint found at `/js/spice/astrobin/fetch_id/`:

```javascript
env.ddg_spice_astrobin_apod = function(api_result) {
    if(!api_result) {
        return Spice.failed('apod');  
    }
    var getimageid = api_result.objects[0].image.split("/");
    $.getScript("/js/spice/astrobin/fetch_id/" + getimageid[4]);
};
```

> `$.getScript()` is just a shorthand wrapper for `$.ajax()`. Many Spice Instant Answers similarly use `$.getJSON()` instead to do the job.

The result of calling the second endpoint is automatically wrapped in a call to `env.ddg_spice_astrobin_fetch_id`. This is because `wrap_jsonp_callback` was set to `1` in the Perl definition, above.

```javascript
env.ddg_spice_astrobin_fetch_id = function(api_result) {
	...
}
```

**Note that there is no need for `alt_to` endpoints to wrap results in a function call, as is normal with primary calls.** You can directly call the endpoint and process its results however you prefer (you don't even need `wrap_jsonp_callback => 1`). 

A good example of this is the [Pokemon Spice](https://duck.co/ia/view/pokemon_data). It creates a second endpoint in order to fetch more detailed information in the JavaScript; the endpoint is called directly and managed using JavaScript promises.

### Attributes of `alt_to` Endpoints

When defining `alt_to` endpoints, you can set the same [attributes](http://docs.duckduckhack.com/backend-reference/spice-attributes.html) that characterize the standard `to` endpoint. For example, the [Pokemon Spice](https://duck.co/ia/view/pokemon_data) sets caching variables:

```perl
spice to => 'http://pokeapi.co/api/v1/pokemon/$1/';
spice wrap_jsonp_callback => 1;

spice alt_to => {
	description => {
		is_cached => 1,
		proxy_cache_valid => '200 30d',
		to => 'http://pokeapi.co/api/v1/description/$1/'
	}
};
```

and the [APOD Spice](https://duck.co/ia/view/apod) wraps results in a function call:

```perl
spice alt_to => {
    fetch_id => {
        to => 'http://www.astrobin.com/api/v1/image/$1/?api_key={{ENV{DDG_SPICE_ASTROBIN_APIKEY}}}&api_secret={{ENV{DDG_SPICE_ASTROBIN_APISECRET}}}&format=json',
        wrap_jsonp_callback => 1
    }
};
```

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

Some APIs require API keys to function properly like in the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm). You can insert an API key for testing in the callback function and replace it with a variable reference when submitting. The API key variable should be named using the provider name as a reference. 

As Wordnik is the API provider used for the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm) we use `DDG_SPICE_WORDNIK_APIKEY` as the variable name.

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
