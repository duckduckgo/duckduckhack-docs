# How to Make a Quick Calculation Tool

Some of the most delightful Instant Answers are easy calculation tools that work right from the search bar, such as [conversions](https://duckduckgo.com/?q=convert%205%20oz%20to%20grams&ia=answer), [permutations](https://duckduckgo.com/?q=16+permutation+3&ia=answer), or [aspect ratios](https://duckduckgo.com/?q=aspect+ratio+4%3A3+640%3A%3F&ia=answer). If you're thinking about building an Instant Answer that performs a quick calculation, this walkthrough is a great example.

We're going to build the [Greatest Common Factor](https://duck.co/ia/view/greatest_common_factor) Instant Answer. See it in action by searching for ["12 76 greatest common factor"](https://duckduckgo.com/?q=12+76+greatest+common+factor&ia=answer):

![](http://docs.duckduckhack.com/assets/gcf.png)

## How It Works

When a user searches anything containing words such as "gcf", "greatest common factor", etc. in the query, DuckDuckGo will trigger this Instant Answer.

When the Instant Answer is triggered, DuckDuckGo executes Perl code on the server to calculate the greatest common factor:

1. It checks that there are two or more numbers present;

2. It determines the greatest common factor;

3. It displays the information to the user.

Let's code it.

## Anatomy of this Instant Answer

Because this Instant Answer executes as Perl code on the server, and doesn't require an external source of data, it's called a "Goodie" Instant Answer. All Goodie Instant Answers are kept together in the [Goodie repository](https://github.com/duckduckgo/zeroclickinfo-goodies) on Github.

A Goodie can be a combination of several back end and front end files, each handling a different aspect of the process. In our case, however, we can get away with no front end files, because our display is simple enough that we can [set our frontend properties in the Perl](http://docs.duckduckhack.com/frontend-reference/setting-goodie-display.html).

![BPM Goodie](http://docs.duckduckhack.com/assets/bpm_goodie_files.png)

Back end files:

File | Purpose | Location
-----|---------|---------
[`GreatestCommonFactor.pm`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GreatestCommonFactor.pm) | A Perl file that specifies the query triggers, calculate the answer, and displays the result | Perl files are placed in the [`zeroclickinfo-goodies/lib/DDG/Goodie`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/lib/DDG/Goodie) directory.
[`GreatestCommonFactor.t`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/GreatestCommonFactor.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer, and what responses to expect | Test files are placed in the [`zeroclickinfo-goodies/t`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/t) directory.

Front end files: none for this Goodie — [we set display properties in the Perl](http://docs.duckduckhack.com/frontend-reference/setting-goodie-display.html)

That's it! Just one code file and one test file is all we need. Next, we'll go line by line and build it together from scratch.

## Set Up Your Development Environment

Before we begin coding, we'll need to set up our development environment. There are three main steps:

1. Fork the Goodie repository on Github.com. ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#1-fork-the-appropriate-repository-on-githubcom))
2. Set up the DuckDuckHack environment on Codio.com ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#2-set-up-the-duckduckgo-environment-on-codiocom))
3. Clone your Github fork onto the Codio environment. ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#3-clone-your-github-fork-onto-the-codio-environment))

If this is your first time developing an Instant Answer, check out our [detailed, step-by-step guide](http://docs.duckduckhack.com/welcome/setup-dev-environment.html) to getting your development environment set up.

## Create the Instant Answer Page

> If you're just using this walkthrough to learn and practice for now, you can skip this step. This is important only if you plan to submit what you're working on.

Every Instant Answer on DuckDuckGo.com has its very own [*Instant Answer Page*](https://duck.co/ia/). These are the home base for planning, collaboration, and metadata. Instant Answer pages also show any Github issues and let you know what stage the Instant Answer is in.

- If you're building a brand new Goodie, start by [creating a new Instant Answer page](https://duck.co/ia/new_ia).
- If you're fixing an existing Goodie, [find the matching page](https://duck.co/ia) and click "Create Issue" to let the community know what you're working on.

When done coding, you'll use the URL of your Instant Answer page when [submitting your contribution](http://docs.duckduckhack.com/submitting/submitting-overview.html).

Now let's start coding!

## Generate Goodie Boilerplate Code

Back in Codio, load the terminal:

![](http://docs.duckduckhack.com/assets/terminal_menu.png)

Next, change into the Goodie repository's home directory, `zeroclickinfo-goodies`:

```
[01:07 PM codio@border-carlo workspace ]$ cd zeroclickinfo-goodies
```

Before doing any coding, it's recommended you work from a [new, separate Git branch](http://docs.duckduckhack.com/resources/git-workflow.html#step-3-create-a-working-branch-for-coding) *and not master*. A separate branch allows you to keep your repository up-to-date, and work on multiple pull requests at one time.

The branch name can be anything you like, for example:

```
[08:18 PM codio@border-carlo zeroclickinfo-goodies {master}]$ git checkout -b gcf
```

[The `duckpan` tool](http://docs.duckduckhack.com/resources/duckpan-overview.html) helps make and test Instant Answers. To create new Goodie boilerplate, run **`duckpan new`**:

```
[01:08 PM codio@border-carlo zeroclickinfo-goodies {gcf}]$ duckpan new
Please enter a name for your Instant Answer :
```

Type `Greatest Common Factors` (since *Greatest Common Factor* already exists in the repository, we'll add an 's' for this tutorial). The tool will do the rest.

You may be prompted to choose a 'handler' and configure optional templates. We'll select the **default handler** ('remainder') and **no optional templates**:

```
Please enter a name for your Instant Answer : Greatest Common Factors
...
Which handler would you like to use to process the query? [1]: 1
Would you like to configure optional templates? [y/N]: n  
```

You'll then receive confirmation that our initial files were successfully created:

```
Created files:                                                                                         
    lib/DDG/Goodie/GreatestCommonFactors.pm                                                            
    t/GreatestCommonFactors.t                                                                          
Success!
```

Conveniently the files have each been named — and located — according to the project's conventions. Internally, each file contains correct boilerplate to save us time.

## `GreatestCommonFactors.pm`

Let's open up `GreatestCommonFactors.pm`.

Navigate using the Codio file tree on the left, and click on the file in the `lib/DDG/Goodie/` directory. It'll be full of comments and sample code we can change as we please.

### Settings

Each Instant Answer is a Perl package, so we start by declaring the package namespace in CamelCase format. This was done automatically for us when we ran the  `duckpan new` command:

```perl
package DDG::Goodie::GreatestCommonFactors;
```

Next, change the comments to contain a short abstract. Easy enough:

```perl
# ABSTRACT: Returns the greatest common factor of the two numbers entered
```

Now we'll import the Goodie class (as well as tell the Perl compiler to be strict), also already done for us:

```perl
use DDG::Goodie;
use strict;
```

We'll specify the `answer_type` (filled in already), and caching. Since the same query will always return the same result, we'll leave caching on:

```perl
zci answer_type => "greatest_common_factors";
zci is_cached   => 1;
```

### Triggers

[Triggers](http://docs.duckduckhack.com/backend-reference/triggers.html) tell DuckDuckGo when to display our Instant Answer. Replace the boilerplate trigger code to the following test trigger:

```perl
triggers startend => 'gcf test';
```

This tells DuckDuckGo that if this string occurs at the *start or end* of any user's search query, it should run this Instant Answer (specifically, the code in this Instant Answer's `handle` function).

Of course, you can put any number of triggers (the [live code](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GreatestCommonFactor.pm#L10) uses `'greatest common factor', 'gcf', 'greatest common divisor', 'gcd'` for example).

### Handle Function

The `handle` function is the meat of our Goodie Instant Answer — where the functionality lives:

```perl
handle remainder => sub {

	# Everything else...

};
```

Our `handle` function accomplishes three things:

1. Filters for queries that can be acted upon
2. Actually calculates the greatest common factors
3. Decides how to display the result

Step 1 is to return immediately *unless* we have two or more numbers to calculate. Copy the following line into the top of the function:

```perl
handle remainder => sub {

	return unless /^\s*\d+(?:(?:\s|,)+\d+)*\s*$/;

	# Everything else...

};
```

Within our `handle` function, we have a [default variable](http://perlmaven.com/the-default-variable-of-perl), which means it's implied in statements like the above regular expression match.

In our `handle` function, our default variable takes on the value of `remainder`. The `remainder` refers to the rest of the query after removing our matched triggers (the remainder of 'greatest common factor 9, 81' would be '9, 81').

Let's split the numbers up into an array, and sort them in ascending order:

```perl
handle remainder => sub {

	return unless /^\s*\d+(?:(?:\s|,)+\d+)*\s*$/;

	my @numbers = grep(/^\d/, split /(?:\s|,)+/);
	@numbers = sort { $a <=> $b } @numbers;

	# Everything else...

};
```

Next we'll calculate the greatest common factor. Notice we'll place a subroutine outside the handle function, so make sure to paste that in as well, just outside the handle function.

```perl
handle remainder => sub {

	return unless /^\s*\d+(?:(?:\s|,)+\d+)*\s*$/;

	my @numbers = grep(/^\d/, split /(?:\s|,)+/);
    @numbers = sort { $a <=> $b } @numbers;

    my $formatted_numbers = join(', ', @numbers);
    $formatted_numbers =~ s/, ([^,]*)$/ and $1/;

    my $result = shift @numbers;
    foreach (@numbers) {
        $result = gcf($result, $_)
    }

	# Everything else...

};

sub gcf {
    my ($x, $y) = @_;
    ($x, $y) = ($y, $x % $y) while $y;
    return $x;
}
```

Finally let's display the result. Since we don't need any special JavaScript or frontend interactions, we can specify everything we need to [display our Goodie right in the Perl](http://docs.duckduckhack.com/frontend-reference/setting-goodie-display.html). We'll use the basic `text` [template group](http://docs.duckduckhack.com/frontend-reference/templates-overview.html).

```perl
handle remainder => sub {

    # Everything else...

    return "Greatest common factor of $formatted_numbers is $result.",
		structured_answer => {
			data => {
				title => $result,
				subtitle => "Greatest common factor of $formatted_numbers"
			},
			templates => {
				group => 'text'
			}
		};
};
```
Goodies can involve more complex display elements, such as HTML templates and JS interactions: learn more about [displaying Goodie results](http://docs.duckduckhack.com/frontend-reference/setting-goodie-display.html).

There's one final line of code on our backend. Because this is a Perl package, it must return `1` at the end to indicate successful loading:

```perl
1;
```

## `GreatestCommonFactors.t`

Creating a test file for your Instant Answer is a critical requirement for [submitting](http://docs.duckduckhack.com/submitting/submitting-overview.html) your Instant Answer. You can learn more in the [Test File Reference](http://docs.duckduckhack.com/testing-reference/test-files.html).

In this case, `duckpan new` created a test file for us, under `t/GreatestCommonFactors.t`.

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Goodie;

zci answer_type => "greatest_common_factors";
zci is_cached   => 1;

ddg_goodie_test(

    # Tests...

);

done_testing;
```

We'll specify several test queries to make sure they trigger our Instant Answer. You can see the full set used [on Github](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/GreatestCommonFactor.t):

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Goodie;

zci answer_type => "greatest_common_factor";
zci is_cached   => 1;

ddg_goodie_test(
    [qw( DDG::Goodie::GreatestCommonFactor )],
    'gcf test 9 81' => test_zci(
        'Greatest common factor of 9 and 81 is 9.',
        structured_answer => {
            input     => ['9 and 81'],
            operation => 'Greatest common factor',
            result    => 9
        }
    )
	# Etc...
);

done_testing;
```

You can execute this test file by running:

```
[01:08 PM codio@border-carlo zeroclickinfo-goodies {gcf}]$ prove -Ilib t/GreatestCommonFactors.t
```

## Interactively Test Our Instant Answer

Inside Codio, we can preview the behavior of all Instant Answers on a local test server.

In Codio, load the terminal, and make sure you are in the `zeroclickinfo-goodies` main directory. If not, change into it.

Enter the **`duckpan server`** command and press Enter.

```
[04:10 PM codio@border-carlo zeroclickinfo-goodies {gcf}]$ duckpan server

```

The terminal should print some text and let you know that the server is listening on port 5000.

```
Starting up webserver...

You can stop the webserver with Ctrl-C

HTTP::Server::PSGI: Accepting connections at http://0:5000/
```

Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type your query to see the results (actual search results will be placeholders.)

![](http://docs.duckduckhack.com/assets/duckpan_server.png)

For example, search for **'gcf test 48 27'**. You should see something like this:

![](http://docs.duckduckhack.com/assets/gcftest.png)

Congratulations! Want to create an Instant Answer to go live on DuckDuckGo.com? Learn more about [submitting your idea](http://docs.duckduckhack.com/submitting/submitting-overview.html).

[![slack](http://docs.duckduckhack.com/assets/slack.png) Have questions? Talk to us on Slack](mailto:QuackSlack@duckduckgo.com?subject=AddMe) or [email us](mailto:open@duckduckgo.com).
