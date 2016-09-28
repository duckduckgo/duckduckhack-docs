# How Instant Answers Work

Each Instant Answer is a set of code that runs alongside DuckDuckGo's search engine. This includes both code that runs on DuckDuckGo's back end, and code that runs on DuckDuckGo's front end.

Here is the basic flow of all Instant Answers:

![Basic](http://docs.duckduckhack.com/assets/basic_ia_flow.png)

Exactly what happens at steps (2) and (3) depends on the type of Instant Answer. There are two types of Instant Answers you can develop: Goodies, and Spice.

## How Goodies Work

A "Goodie" is a type of Instant Answer that calculates its result on DuckDuckGo's server without calling external resources (like an API). Here is the basic flow of the ["Greatest Common Factors" Goodie](https://duck.co/ia/view/greatest_common_factor):

![Basic Goodie](http://docs.duckduckhack.com/assets/basic_goodie_flow.png)

*You can see a walkthrough of [how to build the Greatest Common Factors Goodie](http://docs.duckduckhack.com/walkthroughs/calculation.html).*

As you can see, Goodies can be pretty simple. They mostly consist of server-side (Perl) code. Below is how the actual code files play a part in the Greatest Common Factors Goodie:

![Basic Goodie Files](http://docs.duckduckhack.com/assets/basic_goodie_files.png)

File | Purpose | Location
-----|---------|---------
[`GreatestCommonFactor.pm`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GreatestCommonFactor.pm) | A Perl file that specifies the query triggers and calculate the answer. | Perl files are placed in the [`zeroclickinfo-goodies/lib/DDG/Goodie`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/lib/DDG/Goodie) directory.
[`GreatestCommonFactor.t`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/GreatestCommonFactor.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer, and what responses to expect | Test files are placed in the [`zeroclickinfo-goodies/t`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/t) directory.

There is no need for frontend files because the display is simple enough to [set our frontend properties in the back end Perl](http://docs.duckduckhack.com/frontend-reference/setting-goodie-display.html).

> To easily generate these files, name them correctly, and locate them in the right folders, you can use the `duckpan new` command line tool. More details can be found in the walkthroughs, as well as the [DuckPAN reference](http://docs.duckduckhack.com/resources/duckpan-overview.html).

### Custom Goodie Display

Your Goodie can also have a more sophisticated front end response. The [BPMToMs](https://duck.co/ia/view/bpmto_ms) Goodie is a good example. It uses a [handlebars](http://handlebarsjs.com) HTML template and a css file to render and style the results:

![BPM Goodie](http://docs.duckduckhack.com/assets/bpm_goodie_files.png)

File | Purpose | Location
-----|---------|---------
[`BPMToMs.pm`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) | A Perl file that specifies the query triggers and calculate the answer. | Perl files are placed in the [`zeroclickinfo-goodies/lib/DDG/Goodie`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/lib/DDG/Goodie) directory.
[`BPMToMs.t`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/BPMToMs.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer, and what responses to expect | Test files are placed in the [`zeroclickinfo-goodies/t`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/t) directory.
[`content.handlebars`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms/content.handlebars)| Handlebars template for rendering the server response into HTML. | Front end files are placed in the appropriate `share` subdirectory [`share/goodie/bpmto_ms/`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms)
[`bpmto_ms.css`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms/bpmto_ms.css)| A style sheet for customizing the HTML display. | Front end files are placed in the appropriate `share` subdirectory [`share/goodie/bpmto_ms/`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms)

> To easily generate these files, name them correctly, and locate them in the right folders, you can use the `duckpan new` command line tool and the `all` preset file template. More details can be found in the [DuckPAN reference](http://docs.duckduckhack.com/resources/duckpan-overview.html).

You can learn more about how to [customize the display](http://docs.duckduckhack.com/frontend-reference/setting-goodie-display.html#setting-display-properties-in-a-goodie) of your Goodie results.

## What about Cheat Sheets?

All Cheat Sheets fall under a single Goodie: [The Cheat Sheets Goodie](https://duck.co/ia/view/cheat_sheets). Each new [cheat sheet](https://duck.co/ia?q=cheat+sheet) simply adds a JSON file to the [`share/goodie/cheat_sheets/json/`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/) subdirectory.

Get started with Cheat Sheets with a [cheat sheet walkthrough](http://docs.duckduckhack.com/walkthroughs/programming-syntax.html). For more information about how Cheat Sheets work, check out the [Cheat Sheets Reference](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html).

## How Spice Instant Answers Work

A "Spice" is a type of Instant Answer that makes use of an external API. Here is the basic flow of the ["Hacker News" Spice](https://duck.co/ia/view/hacker_news):

![Basic Spice](http://docs.duckduckhack.com/assets/basic_spice_flow.png)

*You can see a walkthrough of [how to build the Hacker News Spice](http://docs.duckduckhack.com/walkthroughs/forum-lookup.html).*

As you can see, a Spice Instant Answer has most of the action taking place on the front end. The back end mainly decides *when* to trigger, and constructs the API call. The front end *actually calls* the API, processes the results, and displays them to the user.

> Interesting side note: To protect users' privacy, the AJAX call is passed through a DuckDuckGo proxy server. That way, users' browsers never speaks to the third party directly.

Below is how the actual code files play a part in the Hacker News Spice:

![Basic Spice Files](http://docs.duckduckhack.com/assets/basic_spice_files.png)

File | Purpose | Location
-----|---------|---------
[`HackerNews.pm`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/lib/DDG/Spice/HackerNews.pm) | Specifies the query triggers and Hacker News API call. | Perl files are placed in the [`zeroclickinfo-spice/lib/DDG/Spice`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/lib/DDG/Spice) directory.
[`HackerNews.t`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/t/HackerNews.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer. | Test files are placed in the [`zeroclickinfo-spice/t`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/t/) directory.
[`hacker_news.js`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/hacker_news.js) | When the IA is triggered, this file runs on the search results page. It processes the response from the Hacker News API and specifies how to display it. | Front end files are placed in the [`zeroclickinfo-spice/share/spice/hacker_news/`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/) directory.
[`hacker_news.css`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/hacker_news.css) | A minor, optional, custom css file | [`zeroclickinfo-spice/share/spice/hacker_news/`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/)
[`footer.handlebars`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/footer.handlebars) | A minor, optional [sub-template](http://docs.duckduckhack.com/frontend-reference/subtemplates.html), a custom handlebars HTML template used as part of the main template. Its use is specified in `hacker_new.js`. | [`zeroclickinfo-spice/share/spice/hacker_news/`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/hacker_news/)

> To easily generate these files, name them correctly, and locate them in the right folders, you can use the `duckpan new` command line tool and the `all` preset file template. More details can be found in the walkthroughs, as well as the [DuckPAN reference](http://docs.duckduckhack.com/resources/duckpan-overview.html).

And that's how Spices work! Check out the walkthrough of [how to build the Hacker News Spice](http://docs.duckduckhack.com/walkthroughs/forum-lookup.html) to get into the details of each file.

## Naming Conventions

You may look at these files and wonder how are they tied together? Why do back end files have 'CamelCase' naming, and front end files are lowercased? How do they know they are connected to one another?

The formats are conventions. Back end and front end code are indeed linked by their names. The JavaScript callbacks are linked to Perl packages by these same conventions. For example, the Hacker News Perl Package is mapped to its front end JavaScript callback as follows:

> DDG::Spice::HackerNews => ddg_spice_hacker_news

Don't worry about getting this right. By making use of the [`duckpan new`](http://docs.duckduckhack.com/resources/duckpan-overview.html) command used in the walkthroughs, the naming boilerplate is automatically generated for you.

**Now that you know the big picture, start hacking with a walkthrough!**

## Get in Touch

Want help? Need to think out loud? There are [several ways](http://docs.duckduckhack.com/resources/get-in-touch.html) to get in touch with staff, leaders, and community members. We look forward to hearing from you!

*P.S. Let us know if we can improve anything in these documents [by opening issues directly on Github]( https://github.com/duckduckgo/duckduckhack-docs/new).*
