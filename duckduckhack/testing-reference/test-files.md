## Test Files
Good test files can help you quickly test code iterations. They also serve as a functional specification for your code. This specification helps everyone quickly understand and verify the expected behavior of the tested code, improving the quality of the feedback you receive and accelerating the review process.

<!-- /summary -->

Every Instant Answer must include a test file in the `t` directory. The test files are run automatically before each release to ensure that all Instant Answers are functioning properly. Properly functioning Instant Answers:

- ignore any unsuitable queries,
- trigger on the expected queries, and
- provide appropriate answers for the queries handled.

At a minimum, your tests should cover all of your primary and secondary example queries. If possible, you should also include examples of similar queries on which your code does **not** trigger. If your answer depends on the user's location, please review the [Location API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_language_location_apis.md) for help in developing your tests. If your answer depends on the time of day or year, please be sure that your tests will continue to pass no matter when they are run.

## Creating Test Files

If you used `duckpan new` to start your project, a simple test file was automatically created for you. Otherwise, copying the test file from a similar Instant Answer is an easy way to get started. Either way, you are only a few well-placed edits away from a test file suitable for your Instant Answer.

Your test file should have **the same name** as the package it is testing. For example, the code in `lib/DDG/Goodie/Fortune.pm` is tested by `t/Fortune.t`.

The standard DuckPAN installation includes Goodie and Spice testing libraries (`DDG::Test::Goodie` and `DDG::Test::Spice`, respectively.) These libraries make it quick and easy to develop tests for your Instant Answer.

## Running Test Files

Tests are run from the root of the repository using the `prove` command included in your Perl distribution. During development, you can quickly run a single test file to verify your changes:

```shell
prove -Ilib t/TestName.t
```

<!-- /summary -->

Or all of the tests in the repository's `t` directory:

```shell
prove -Ilib t/
```

To ensure that you have not inadvertently changed the behavior of other code, you should run the full test suite before submitting your Instant Answer. This is easily accomplished via `duckpan`:

```shell
duckpan test
```

## Example Goodie Test File

Below is the test file of the **RouterPasswords** Goodie, found at [`t/RouterPasswords.t`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/RouterPasswords.t).

<!-- /summary -->

```perl
#!/usr/bin/env perl

use strict;
use warnings;

# These modules are necessary for the functions we'll be running.
use Test::More;
use DDG::Test::Goodie;

# These zci attributes aren't necessary, but if you specify them inside your
# goodie, you'll need to add matching values here to check against.
zci answer_type => 'password';
zci is_cached => 1;

ddg_goodie_test(
    [
        # This is the name of the goodie that will be loaded to test.
        'DDG::Goodie::RouterPasswords'
    ],
    # This is a sample query, just like the user will enter into the DuckDuckGo
    # search box.
    'Belkin f5d6130' =>
        test_zci(
            # The first argument to test_zci is the plain text (default)
            # returned from a goodie.  If your goodie also returns an HTML
            # version, you can pass that along explicitly as the second
            # argument. If your goodie is random, you can use regexps instead of
            # strings to match against.
            'Default login for the BELKIN F5D6130: Username: (none) Password: password',
            html => 'Default login for the BELKIN F5D6130:<br><i>Username</i>: (none)<br><i>Password</i>: password'
        ),
    # You should include more test cases here. Try to think of ways that your
    # Instant Answer might break, and add them here to ensure they won't. Here are a
    # few others that were thought of for this goodie.
    'Belkin f5d6130 password default' =>
        test_zci('Default login for the BELKIN F5D6130: Username: (none) Password: password',
            html => 'Default login for the BELKIN F5D6130:<br><i>Username</i>: (none)<br><i>Password</i>: password'),
    'default password Belkin f5d6130' =>
        test_zci('Default login for the BELKIN F5D6130: Username: (none) Password: password',
            html => 'Default login for the BELKIN F5D6130:<br><i>Username</i>: (none)<br><i>Password</i>: password'),
    'Belkin f5d6130 password' =>
        test_zci('Default login for the BELKIN F5D6130: Username: (none) Password: password',
            html => 'Default login for the BELKIN F5D6130:<br><i>Username</i>: (none)<br><i>Password</i>: password'),
    'default BELKIN password f5d6130' =>
        test_zci('Default login for the BELKIN F5D6130: Username: (none) Password: password',
            html => 'Default login for the BELKIN F5D6130:<br><i>Username</i>: (none)<br><i>Password</i>: password'),
    'password bELKIN default f5d6130' =>
        test_zci('Default login for the BELKIN F5D6130: Username: (none) Password: password',
            html => 'Default login for the BELKIN F5D6130:<br><i>Username</i>: (none)<br><i>Password</i>: password'),
);

# This function call is expected by Test::More. It makes sure the program
# doesn't exit before all the tests have been run.
done_testing;
```

## Example Spice Test File

Below is the test file of the **Xkcd** Spice, found at [`t/Xkcd.t`](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/t/Xkcd.t).

<!-- /summary -->

```perl
#!/usr/bin/env perl

use strict;
use warnings;

# These modules are necessary for the functions we'll be running.
use Test::More;
use DDG::Test::Spice;

ddg_spice_test(
    [
        # This is the name of the Spice will be loaded to test.
        'DDG::Spice::Xkcd'
    ],
    # This is a sample query, just like the user will enter into the DuckDuckGo
    # search box.
    '619 xkcd' => test_spice(
        # The first argument is the Spice callback. It includes the javascript
        # endpoint and the argument list constructed by the Perl code. In this
        # case, the endpoint is '/js/spice/xkcd/', and the argument returned by
        # the Perl code is 619.
        '/js/spice/xkcd/619',
        # This is the Spice calltype. It's almost always set to 'include',
        # except for some special cases like FlashVersion which don't make a
        # normal API call.
        call_type => 'include',
        # This is the Spice that should be triggered by the query.
        caller => 'DDG::Spice::Xkcd',
        # This is the cache value to expect. It's only necessary if you specify
        # one in your Spice.
        is_cached => 0
    ),
    # You should include more test cases here. Try to think of ways that your
    # Instant Answer might break, and add them here to ensure they won't. Here are is
    # another that is tested for this Spice.
    'xkcd' => test_spice(
        '/js/spice/xkcd/',
        call_type => 'include',
        caller => 'DDG::Spice::Xkcd',
        is_cached => 0
    ),
);

# This function call is expected by Test::More. It makes sure the program
# doesn't exit before all the tests have been run.
done_testing;
```

