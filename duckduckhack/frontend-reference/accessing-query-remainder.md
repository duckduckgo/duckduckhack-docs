# Accessing the Query Remainder

While it's possible to get the user's full original query with [`DDG.get_query()`](#), but often you may only need a specific part of it.

For example, let's look at the [Hacker News IA](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/HackerNews.pm).

If a user searches for something like "hacker news oculus rift", you may want to ignore the trigger words ("hacker news") and only retrieve what the user was searching for ("oculus rift").

You could replace those trigger words manually, but it's better not to have a duplicate list of trigger words between your backend and frontend code. Luckily, there's a way to get the user's query as processed by the backend code.

```javascript
var script = $('[src*="/js/spice/hacker_news/"]')[0],
    source = $(script).attr("src"),
    query = source.match(/hacker_news\/([^\/]+)/)[1],
    decodedQuery = decodeURIComponent(query);

console.log(decodedQuery); // "oculus rift"
```

Here's what this snippet does, line by line:

```
var script = $('[src*="/js/spice/hacker_news/"]')[0],
    source = $(script).attr("src"),
```

The JSONP response from the Spice query will be retrieved as a script with a source of `/js/spice/hacker_news/oculus%20rift`. The first part of this (`/js/spice/hacker_news/`) will always be the same for our Spice, so we can use jQuery to get access to our `script` tag, and get its full `src` attribute.

At this point the `source` variable contains `/js/spice/hacker_news/oculus%20rift`.

```
    query = source.match(/hacker_news\/([^\/]+)/)[1],
    decodedQuery = decodeURIComponent(query);
```

Then we use regular expressions to get anything after `/hacker_news/`, and run it against `decodeURIComponent()` to remove all URL encoded characters.

If you're returning multiple values in your backend `handle` function, you may need some more logic. For instance:

```
// our JSONP response has src like "/js/spice/example_answer/term1/term2"

var matches = source.match(/example_answer\/([^\/]+)\/([^\/]+)/),
    partOne = matches[1], // equals "term1"
    partTwo = matches[2]; // equals "term2"
```

(More for this section is coming soon! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)
