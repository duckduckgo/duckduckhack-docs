## Language & Location APIs

Some Instant Answers employ contextual data about the user's search to provide the most relevant results. For example, since weather conditions vary widely around the world, the [Is it snowing?](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Snow.pm) Instant Answer requires the user's approximate location.

The [core DDG library](https://github.com/duckduckgo/duckduckgo) provides Goodie and Spice Instant Answers with location and language APIs to provide simple, helpful and delightful results.

## Location API

The [core DDG library](https://github.com/duckduckgo/duckduckgo) provides a Location API. Since Goodie and Spice Instant Answers inherit from this package, their `handle` functions have access to a `$loc` variable which refers to a [Location object](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Location.pm).

This Location object has a number of [useful attributes](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Location.pm#L6) to help you provide relevant answers:

```perl
my @geo_ip_record_attrs = qw( country_code country_code3 country_name region
    region_name city postal_code latitude longitude time_zone area_code
    continent_code metro_code );
```

Example data from `$loc`:

```perl
country_code   => US
country_code3  => USA
country_name   => United States
region         => PA
region_name    => Pennsylvania
city           => Phoenixville
postal_code    => 19460
latitude       => 40.1246
longitude      => -75.5385
time_zone      => America/New_York
area_code      => 610
continent_code => NA
metro_code     => 504
```

**Note:** When testing Instant Answers interactively with `duckpan`, the location will **always** point to "Phoenixville, Pennsylvania, United States":

```perl
my $location = join(", ", $loc->city, $loc->region_name, $loc->country_name);
# "Phoenixville, Pennsylvania, United States"
```

For assistance with specifying the location to be used in automated testing, please refer to the [Location API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_location_language_apis.md).

Naturally, once your Instant Answer is live, `$loc` will refer to the appropriate location.

## Language API

The [core DDG library](https://github.com/duckduckgo/duckduckgo) exposes a Language API which Goodie and Spice Instant Answers can access in their `handle` functions. The language data is contained in the `$lang` variable.

<!-- /summary -->

`$lang` refers to a [Language object](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Language.pm) with the following properties:

```perl
my @language_attributes = qw( flagicon flag_url name_in_local rtl locale nplurals name_in_english);
```

Example data from `$lang`:

```perl
'nplurals'        => 2,
'name_in_local'   => 'English of United States',
'rtl'             => 0,
'flag_url'        => 'https://duckduckgo.com/f2/us.png',
'name_in_english' => 'English of United States',
'locale'          => 'en_US',
'flagicon'        => 'us'
```

**Note**: The user's locale does not imply their preferred language. It simply provides the locale based on the user's IP. Thus, the locale should not be used to determine the display language for an Instant Answer.

When testing interactively with `duckpan`, the locale will always be set to `en_US`.

It is possible to set different locales when running automated tests. Please refer to the [Language API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_location_language_apis.md) for more information.
