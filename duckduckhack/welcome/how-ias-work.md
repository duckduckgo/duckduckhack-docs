# How Instant Answers Work

Each Instant Answer is a set of code that runs alongside DuckDuckGo's search engine. This includes both code that runs on DuckDuckGo's backend, and code that runs on DuckDuckGo's frontend.

Here is the basic flow of all Instant Answers:

![Basic](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/basic_ia_flow.png)

Exactly what happens at steps (2) and (3) depends on the type of Instant Answer. There are two types of Instant Answers you can develop: Goodies, and Spice.

## Goodie Instant Answers

A "Goodie" is a type of Instant Answer that calculates its result on DuckDuckGo's server without calling external resources (like an API). Here is the basic flow of the ["Greatest Common Factors" Goodie](https://duck.co/ia/view/greatest_common_factor):

![Basic Goodie](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/basic_goodie_flow.png)

*You can see a walkthrough of [how to build the Greatest Common Factors Goodie](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/walkthroughs/calculation.html).*

As you can see, Goodies can be pretty simple. They mostly consist of server-side (Perl) code. Below is how the actual code files play a part in the Greatest Common Factors Goodie:

![Basic Goodie Files](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/basic_goodie_files.png)

File | Purpose | Location
-----|---------|---------
[`GreatestCommonFactor.pm`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GreatestCommonFactor.pm) | A Perl file that specifies the query triggers and calculate the answer. | Perl files are placed in the [`zeroclickinfo-spice/lib/DDG/Goodie`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/lib/DDG/Goodie) directory.
[`GreatestCommonFactor.t`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/GreatestCommonFactor.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer, and what responses to expect | Test files are placed in the [`zeroclickinfo-goodies/t`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/t) directory.

There is no need for frontend display files because this Goodie uses the simplest form of displaying results: [structured responses](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/frontend-reference/setting-goodie-display.html#easy-structured-responses).

### Custom Goodie Display

Your Goodie can also have a more sophisticated frontend response. The [BPMToMs](https://duck.co/ia/view/bpmto_ms) Goodie is a good example. It uses a [handlebars](http://handlebarsjs.com) html template and a css file to render and style the results:

![BPM Goodie](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/bpm_goodie_files.png)

File | Purpose | Location
-----|---------|---------
[`BPMToMs.pm`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) | A Perl file that specifies the query triggers and calculate the answer. | Perl files are placed in the [`zeroclickinfo-spice/lib/DDG/Goodie`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/lib/DDG/Goodie) directory.
[`BPMToMs.t`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/t/BPMToMs.t) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer, and what responses to expect | Test files are placed in the [`zeroclickinfo-goodies/t`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/t) directory.
[`content.handlebars`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms/content.handlebars)| Handlebars template for rendering the server response into html. | Frontend files are placed in the appropriate `share` subdirectory [`share/goodie/bpmto_ms/`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms)
[`bpmto_ms.css`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms/bpmto_ms.css)| A stylesheet for customizing the html display. | Frontend files are placed in the appropriate `share` subdirectory [`share/goodie/bpmto_ms/`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/bpmto_ms)


You can learn more about how to [customize the display](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/frontend-reference/setting-goodie-display.html#setting-display-properties-in-a-goodie) of your Goodie results.













