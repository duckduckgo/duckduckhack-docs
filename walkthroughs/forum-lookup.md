# How to Make an API-Based Forum Lookup

Some of the coolest Instant Answers are those that bring external APIs directly into search results.

One application of these include direct access to forums, such as [Stack Overflow](https://duck.co/ia/view/stack_overflow) or [Reddit](https://duck.co/ia/view/reddit_search). We'd love to see more communities made part of search results, and this tutorial is an example of how to do that.

**Together we'll build an Instant Answer that directly displays Hacker News posts alongside DuckDuckGo.com search results:**

![](https://docs.duckduckhack.com/assets/hacker_news_search.png)

You can see it in action by searching for ["hn dropbox"](https://duckduckgo.com/?q=hn+dropbox&ia=social), for example.

## How It Works

When a user searches anything containing words such as "hn", "hn search", or "hacker news" at certain locations in the query, DuckDuckGo will trigger this Instant Answer.

When the Instant Answer is triggered by an appropriate search query, the following steps take place:

1. The DuckDuckGo results page makes an AJAX call to the Hacker News API.

2. When the API call returns, DuckDuckGo will pass the response to the Instant Answer's front end callback.

3. If the response contains any articles, the Instant Answer will display each item to the user.

Simple enough. So how do we make that work in code?

## Anatomy of this Instant Answer

Because this Instant Answer calls an external API, it's called a "Spice" Instant Answer. All Spice Instant Answers are kept together in the [Spice repository](https://github.com/duckduckgo/zeroclickinfo-spice) on Github.

A Spice is a combination of several back end and front end files, each handling a different aspect of the process.

![Basic Spice Files](http://docs.duckduckhack.com/assets/basic_spice_files.png)

Back end files:

File | Purpose | Location
-----|---------|---------
[`HackerNews.pm`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/lib/DDG/Spice/HackerNews.pm) | Specifies the query triggers and the Hacker News API call. | Perl files are placed in the [`zeroclickinfo-spice/lib/DDG/Spice`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/lib/DDG/Spice) directory.
[`HackerNews.t`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/t/HackerNews.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer. | Test files are placed in the [`zeroclickinfo-spice/t`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/t/) directory.

Front end files:

File | Purpose | Location
-----|---------|---------
[`hacker_news.js`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/hacker_news.js) | When the IA is triggered, this file runs on the search results page. It processes the response from the Hacker News API and specifies how to display it. | Front end files are placed in the [`zeroclickinfo-spice/share/spice/hacker_news/`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/) directory.
[`hacker_news.css`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/hacker_news.css) | A minor, optional, custom css file | [`zeroclickinfo-spice/share/spice/hacker_news/`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/)
[`footer.handlebars`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/footer.handlebars) | A minor, optional [sub-template](http://docs.duckduckhack.com/frontend-reference/subtemplates.html), a custom handlebars HTML template used as part of the main template. Its use is specified in `hacker_new.js`. | [`zeroclickinfo-spice/share/spice/hacker_news/`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/)

That's it! These are all the files and functionality necessary to create this Instant Answer. Next, we'll go line by line and build it together from scratch.

## Set Up Your Development Environment

Before we begin coding, we'll need to set up our development environment. There are three main steps:

1. Fork the Spice repository on Github.com. ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#1-fork-the-appropriate-repository-on-githubcom))
2. Set up the DuckDuckHack environment on Codio.com ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#2-set-up-the-duckduckgo-environment-on-codiocom))
3. Clone your Github fork onto the Codio environment. ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#3-clone-your-github-fork-onto-the-codio-environment))

If this is your first time developing an Instant Answer, check out our [detailed, step-by-step guide](http://docs.duckduckhack.com/welcome/setup-dev-environment.html) to getting your development environment set up.

## Create the Instant Answer Page

> If you're just using this walkthrough to learn and practice for now, you can skip this step. This is important only if you plan to submit what you're working on.

Every Instant Answer on DuckDuckGo.com has its very own [*Instant Answer Page*](https://duck.co/ia/). These are the home base for planning, collaboration, and metadata. Instant Answer pages also show any Github issues and let you know what stage the Instant Answer is in.

- If you're building a brand new Spice, start by [creating a new Instant Answer page](https://duck.co/ia/new_ia).
- If you're fixing an existing Spice, [find the matching page](https://duck.co/ia) and click "Create Issue" to let the community know what you're working on.

When done coding, you'll use the URL of your Instant Answer page when [submitting your contribution](http://docs.duckduckhack.com/submitting/submitting-overview.html).

Now let's start coding!

## Generate Spice Boilerplate Code

Back in Codio, load the terminal:

![](https://docs.duckduckhack.com/assets/terminal_menu.png)

Next, change into the Spice repository's home directory, `zeroclickinfo-spice`:

```
[08:17 PM codio@border-carlo workspace ]$ cd zeroclickinfo-spice
```

Before doing any coding, it's recommended you work from a [new, separate Git branch](http://docs.duckduckhack.com/resources/git-workflow.html#step-3-create-a-working-branch-for-coding) *and not master*. A separate branch allows you to keep your repository up-to-date, and work on multiple pull requests at one time.

The branch name can be anything you like, for example:

```
[08:18 PM codio@border-carlo zeroclickinfo-spice {master}]$ git checkout -b hacker_newz
```

[The `duckpan` tool](http://docs.duckduckhack.com/resources/duckpan-overview.html) helps make and test Instant Answers. To create new Spice boilerplate, run **`duckpan new`** with the `all` template ([more about duckpan here](http://docs.duckduckhack.com/resources/duckpan-overview.html)):

```
[08:18 PM codio@border-carlo zeroclickinfo-spice {hacker_newz}]$ duckpan new --template all
```

When prompted for a name, type **`Hacker Newz`** (since *Hacker News* already exists in the repository, we'll change one letter for this tutorial). The tool will do the rest.

You may be prompted to choose a 'handler'. We'll select the **default handler** ('remainder').

```
Please enter a name for your Instant Answer : Hacker Newz
...
Which handler would you like to use to process the query? [1]: 1
```

You'll then receive confirmation that our initial files were successfully created:

```
Created files:                                                                                         
    lib/DDG/Spice/HackerNewz.pm                                                                        
    t/HackerNewz.t                                                                                     
    share/spice/hacker_newz/hacker_newz.js                                                             
    share/spice/hacker_newz/hacker_newz.css                                                            
    share/spice/hacker_newz/hacker_newz.handlebars                                                     
Success!
```

Conveniently the files have each been named — and located — according to the project's conventions. Internally, each file contains correct boilerplate to save us time.

## `HackerNewz.pm`

Let's open up `HackerNewz.pm`.

Navigate using the Codio file tree on the left, and click on the file in the `lib/DDG/Spice/` directory. It'll be full of comments and sample code we can change as we please.

### Settings

Each Instant Answer is a Perl package, so we start by declaring the package namespace in CamelCase format. This was done automatically for us when we ran the  `duckpan new` command:

```perl
package DDG::Spice::HackerNewz;
```

Next, change the comments to contain a short abstract. Easy enough:

```perl
# ABSTRACT: Search for Hacker News
```

Now we'll import the Spice class — also already done for us:

```perl
use DDG::Spice;
```

On the next line, we'll leave caching on. By default, caching saves the results to individual API calls for an hour. Of course, this may not be right for some Instant Answers so you can just replace `1` with `0`. There are several options when it comes to caching — [learn more in the API reference](http://docs.duckduckhack.com/backend-reference/api-reference.html#caching).

```perl
spice is_cached => 1;
spice proxy_cache_valid => "200 1d";
```

### API Endpoint

With the formalities out of the way, let's define the most important element of our Instant Answer — the API call. This is a URL to which we'll make a GET request.

> How do we choose an API? Currently, the community can only accept JSON or JSONP APIs. Due to DuckDuckGo's [scale](https://duckduckgo.com/traffic.html), APIs must be [free, fast, credible, and reliable](http://docs.duckduckhack.com/submitting/checklist.html#do-you-plan-to-use-an-external-data-source).

We're just hacking for now, so let's enter our URL for querying the Hacker News Search API:

```perl
spice to => 'https://hn.algolia.com/api/v1/search?query=$1&tags=story';
```

Notice the `$1` — that's a placeholder for a dynamic value our Instant Answer will provide. Many Instant Answers take advantage of this for search endpoints, but others might not need it at all. Others may use [multiple placeholders](http://docs.duckduckhack.com/backend-reference/api-reference.html#multiple-placeholders-in-api-url). Feel free to leave it out of your URL.

What fills the `$1`? Our *handle* function, which we'll talk about in a bit.

### Indicate our Callback Function

In most cases, APIs support JSONP, which allows for a "callback" parameter. That way, the JSON object returns neatly wrapped in a JavaScript function call. This parameter is usually called "callback", but that depends on the API.

**For APIs that support this parameter** pass the special environment variable `{{callback}}` in the URL. For example, `spice to => 'http://www.api.example.com/?q=$1&callback={{callback}}';`. DuckDuckGo will then insert the corresponding JavaScript callback name. (How does it know which callback? Great question. [More on this below](#define-the-callback).)

Our particular Hacker News API doesn't allow us to specify a callback. No worries — we'll leave out the `{{callback}}` variable from the URL. We'll set a separate attribute called  `wrap_jsonp_callback` to equal `1`. (This is already included in the boilerplate — just change the value to `1`.)

```perl
spice wrap_jsonp_callback => 1;
```

Now, when the JSON is returned by the API, DuckDuckGo will wrap our result in a call to our Spice's JavaScript callback function. Later, we'll *define* the callback function in the front end, in `hacker_newz.js`.

### Triggers

How will DuckDuckGo know to display our Instant Answer on a user's search? That's what *triggers* are for. For now we'll keep it simple. Add the following triggers after the `triggers` attribute in the boilerplate:

```perl
triggers startend => "hacker newz";
```

This tells DuckDuckGo that if this string occurs at the *start or end* of any user's search query, it should activate our Instant Answer and attempt calling the API. There are several types of triggers in addition to `startend` — [see them all here](http://docs.duckduckhack.com/backend-reference/triggers.html).

Of course, simply matching a trigger doesn't guarantee the API will return anything useful, just that the API is worth trying.

### Handle Function

Remember our `$1` placeholder before? It's filled in by the `handle` function. This function acts as the last filter before we call the API. Whatever the handle function returns will be inserted into the API call. If it returns nothing, the API will not be called.

In our case, we'll change our handle function to abort the Instant Answer if there is no remainder. If there is a remainder, pass it directly to the API placeholder:

```perl
handle remainder => sub {
    return $_ if $_;
    return;
};
```

Within our `handle` function, `$_` is a special variable that takes on the value of `remainder`. The `remainder` refers to the rest of the query after removing our matched triggers.

This function is a simple case: it returns the *remainder* of the query, unless it's blank. The *remainder* is just the query minus the trigger. If a user searches 'hacker news meteor', the remainder would be 'meteor'.

While triggers specify when to trigger our Instant Answer, handle functions are used to limit those cases. Handle functions can get more complicated if necessary, by including regular expressions and returning *multiple* placeholders: [learn about using regular expressions in handle functions](http://docs.duckduckhack.com/backend-reference/handle-functions.html#regex-guards) and [returning multiple placeholders](http://docs.duckduckhack.com/backend-reference/api-reference.html#multiple-placeholders-in-api-url).

There's one final line of code on our back end. Because this is a Perl package, it must return `1` at the end to indicate successful loading:

```perl
1;
```

Our Spice back end is complete. Functionally, we've told DuckDuckGo:

- *Where* to call the API (endpoint)
- *When* to call the API (triggers)
- *When not* to call the API (handle function)

We're done with our back end. Next, we'll tell DuckDuckGo how to display any results we get back.

## `hacker_newz.js`

Let's open up `hacker_newz.js`. Navigate using the Codio file tree on the left, and click on the file in the `zeroclickinfo-spice/share/spice/hacker_newz/` directory. It, too, will be full of comments and sample code we can change as we please.

### JavaScript Formalities

Our JavaScript file is wrapped inside the "[module pattern](http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript)" that makes sure we can access the global scope, but that no variables inside this pattern will leak into the global scope. We also take advantage of JavaScript's [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FFunctions_and_function_scope%2FStrict_mode).

```javascript
(function(env) {
    "use strict";

    // Everything else...

}(this));
```

It's not at all critical to understand this, simply that it is required for any Instant Answer front end.

### Define the Callback

Our front end callback is what handles any data from our API call. When our API call returns, its response is passed to this callback as `api_result`. It is already included in the boilerplate, and no need to change anything:

```javascript
env.ddg_spice_hacker_newz = function(api_result) {
    // Everything else...
}
```

> You might be asking yourself, why is the callback named `ddg_spice_hacker_newz`? How does DuckDuckGo know to connect this JavaScript callback to the Perl package we wrote above? *The answer is in naming conventions.* The Perl package name we defined in the first line of `HackerNewz.pm` is used to determine the name of the callback:

> DDG::Spice::HackerNewz => ddg_spice_hacker_newz

### Call Spice.Failed() If Nothing Returned

Just because our Instant Answer triggered doesn't mean the API will necessarily return any results. Here, we check for the case of no response, error response, or empty response.

Below is the default code you will see. **However, this code should be customized to fit the response of your particular API.**

```javascript
if (!api_result || api_result.error) {
    return Spice.failed('hacker_newz');
}
```

The Hacker News API, in particular, returns its data inside a `hits` property, so we check for its existence.

Like many APIs, the results come as an *array*. That means we'll also check if `hits` has a `length`. That way, if no results were returned from the API, we can stop that as well.

Change the section of the code to look like this, to fit our particular API:

```javascript
if (!api_result || !api_result.hits || api_result.hits.length === 0) {
    return Spice.failed('hacker_newz');
}
```

It's important to use `Spice.failed()` because this lets the rest of the Spice system know our Spice isn't going to display so that other relevant answers can be given an opportunity to display.

### Display the Data

With results in hand, we call `Spice.add()` to display our Spice to the user. In this function call we'll instruct the framework how to display the information returned by our API.

### Set Our Display Properties

Let's look inside the `Spice.add()` call. It's passed an object with display properties — let's go through each. A full explanation of each display property can be found in the [Display Reference](http://docs.duckduckhack.com/frontend-reference/display-reference.html).

The `id` is automatically inserted for us:

```javascript
id: 'hacker_newz',
```

The `name` is the name of the clickable tab in the AnswerBar containing our Instant Answer. Change it to be as follows:

```javascript
name: 'Social',
```

We specify the `data` returned by the API. This is usually `api_result` or the sub-property containing the array of data items — in this particular API's case, `hits`.

```javascript
data: api_result.hits,
```

The `meta` property defines all the surrounding details of the Instant Answer, such as the phrase "Showing 20 Hacker News Submissions", or the link to the information source. You can learn about each meta property available to you in the [Display Reference](http://docs.duckduckhack.com/frontend-reference/display-reference.html).

In this example, `sourceUrl` is calculated at the top of the callback in [`hacker_newz.js`](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/hacker_news/hacker_news.js#L8)

```javascript
meta: {
    sourceName: 'HNZ Search',
    total: api_result.hits,
    itemType: (api_result.hits.length === 1) ? 'Hacker Newz submission' : 'Hacker Newz submissions'
},
```

To prepare our data for displaying as HTML, we define a `normalize` function. This optional function takes each raw API item (a JavaScript object), and creates a new object which the HTML template can display.

The `normalize` function is iterated on each item in the API result. Also, the original properties of each API item are also included (unless explicitly overwritten). Learn more about the [`normalize` function here](http://docs.duckduckhack.com/frontend-reference/display-reference.html#normalize-function-optional).

```javascript
normalize: function(item) {
    return {
        title: item.title,
        url: (item.url) ? item.url : 'https://news.ycombinator.com/item?id=' + item.objectID,
        points: item.points || 0,
        num_comments: item.num_comments || 0
    };
},
```

These fields correspond to the fields in the HTML templates we've chosen to use.

Next, let's specify what HTML templates we'll use to display each item. The vast majority of Instant Answers use the DuckDuckHack [built-in templates system](http://docs.duckduckhack.com/frontend-reference/templates-overview.html). There are all sorts of specialized templates, from displaying places on a map, to displaying movie titles, to products, and lookup information. Each of these can be customized using [options](http://docs.duckduckhack.com/frontend-reference/templates-reference.html) and [variants](http://docs.duckduckhack.com/frontend-reference/variants-reference.html).

[Template groups](http://docs.duckduckhack.com/frontend-reference/template-groups.html) are convenient presets. They're specified in the `group` property. The other properties you see under templates customize the behavior of the group. For example, `detail: false` makes sure items will always be displayed as tiles. Learn more about these options in the [templates reference](http://docs.duckduckhack.com/frontend-reference/templates-reference.html).

```javascript
templates: {
    group: 'text',
    options: {
        footer: Spice.hacker_newz.footer
    },
    detail: false,
    item_detail: false,
    variants: {
        tileTitle: "3line-small",
        tileFooter: "3line"
    }
},
```

Finally, we'll define the properties on which we'll sort results. [Learn more about sorting here](http://docs.duckduckhack.com/frontend-reference/display-reference.html#sortfields-object-optional).

Following the `templates` property, define `sort_fields` and `sort_default`:

```javascript
sort_fields: {
    score: function(a, b){
        return (a.points > b.points) ? -1 : 1;
    },
    date: function(a, b){
        return (a.created_at_i > b.created_at_i) ? -1 : 1;
    }
},
sort_default: 'score'
```

As an aside, for those interested in doing more advanced things in the front end, the Instant Answer framework also provides a [JavaScript API](http://docs.duckduckhack.com/frontend-reference/js-api-reference.html) with useful functions you can call.

As far as our "Hacker Newz" Instant Answer is concerned, our front end is complete. We've fully specified how DuckDuckGo should display our data to users.

## Handlebars Templates

Many [built-in templates](http://docs.duckduckhack.com/frontend-reference/templates-overview.html) allow for inserting [sub-templates](http://docs.duckduckhack.com/frontend-reference/subtemplates.html) to fill out particular features. For example, sub-templates can be used to create custom footers, calls-to-action, or decide how to display lists of values.

You'll notice that above in the `templates` property, we've set a footer:

```javascript
templates: {
    ...
    options: {
        footer: Spice.hacker_newz.footer
    },
    ...
}
```

If you'd like, you can go ahead and create this template. First, go to the `zeroclickinfo-spice/share/spice/hacker_newz/` directory.

Rename `hacker_newz.handlebars` to `footer.handlebars` by right-clicking on it.

Finally, open the file and overwrite the following HTML into it:

```html
<div class="one-line  text--secondary">{{created_at}}</div>
<div class="tile__domain  one-line  text--secondary">{{author}}</div>
<div class="one-line">
    <span class="tile__score  text--primary">{{points}}</span> &middot; <a href="http://news.ycombinator.com/item?id={{objectID}}">{{plural num_comments singular="Comment" plural="Comments"}}</a>
</div>
```

> Sub-templates can either be built-in or created custom for your Instant Answer. You can learn more about how they work in the [sub-templates reference](http://docs.duckduckhack.com/frontend-reference/subtemplates.html).

## CSS Files

You'll notice there's a [css file](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/hacker_news/hacker_news.css) in the `share/spice/hacker_newz/` directory.

While any CSS files in the directory will be included automatically, **this is no longer necessary or encouraged**. Instead, the more stable and maintainable option is to use [variants](http://docs.duckduckhack.com/frontend-reference/variants-reference.html).

## Test File

Creating a test file for your Instant Answer is a critical requirement for [submitting](http://docs.duckduckhack.com/submitting/submitting-overview.html) your Instant Answer. You can learn more in the [Test File Reference](http://docs.duckduckhack.com/testing-reference/test-files.html).

In this case, `duckpan new` created a test file for us, under `t/HackerNewz.t`. We'll specify two test queries to make sure they trigger our Instant Answer:

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Spice;

ddg_spice_test(
    [qw( DDG::Spice::HackerNewz )],
    'hacker newz duckduckgo' => test_spice(
        '/js/spice/hacker_newz/duckduckgo',
        call_type => 'include',
        caller => 'DDG::Spice::HackerNewz'
    ),
    'hacker newz postgresql' => test_spice(
        '/js/spice/hacker_newz/postgresql',
        caller    => 'DDG::Spice::HackerNewz',
    ),
);

done_testing;
```

A test file is required for submitting your Instant Answer. However, we don't need it to proceed with interactively testing our code, which we'll do next.

## Interactively Test Our Instant Answer

Inside Codio, we can preview the behavior of all Instant Answers on a local test server.

In Codio, load the terminal, and make sure you're in your repository's home directory. If not, change into it.

Enter the **`duckpan server`** command and press Enter.

```
[08:18 PM codio@border-carlo zeroclickinfo-spice {hacker_newz}]$ duckpan server

```

The terminal should print some text and let you know that the server is listening on port 5000.

```
Starting up webserver...

You can stop the webserver with Ctrl-C

HTTP::Server::PSGI: Accepting connections at http://0:5000/
```

Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type a query to see the results (actual search results will be placeholders.)

![](https://docs.duckduckhack.com/assets/duckpan_server.png)

For example, search for **'hacker newz code'**. You should see something like this:

![](https://docs.duckduckhack.com/assets/hackernewz-code.png)

Congratulations! Want to create an Instant Answer to go live on DuckDuckGo.com? Learn more about [submitting your idea](http://docs.duckduckhack.com/submitting/submitting-overview.html).

[![slack](http://docs.duckduckhack.com/assets/slack.png) Have questions? Talk to us on Slack]({{ book.slackURL }}) or [email us](mailto:open@duckduckgo.com).
