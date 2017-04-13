# Developing a Reference Fathead

Developing a reference Fathead has **three** phases:

1. Covering the main articles
2. Adding article redirects
3. Addressing unanswered queries

For each of these phases there will be a pull request, which will be merged and deployed upon phase completion; we will then be able to observe the changes to the Instant Answer's coverage and engagement data. The data is available within the Search Overview topic for the specific language.

See the [Fathead Overview](https://docs.duckduckhack.com/fathead-reference/section.html) article to learn more about Fatheads.


## Phase 1: Covering Articles
For the first phase you will open a pull request in which your Fathead parsing script fetches and parses all the articles referencing keywords, operators, classes, functions, methods, etc, for the language or library you're working on.

The article titles should be unique and specific. Ideally you want to look for documentation that documents the language/library API specifically.

For example, an SQLAlchemy Fathead should avoid the generic "[tutorial](http://docs.sqlalchemy.org/en/rel_1_1/core/tutorial.html)" section of the documentation, and focus on the portions which outline the specific functions/methods/classes along with descriptions. That way, for queries like `sqlalchemy.types.DateTime` we can show an answer based on the [relevant documentation](http://docs.sqlalchemy.org/en/rel_1_1/core/type_basics.html#sqlalchemy.types.DateTime), and provide a direct link to it.

### Ensuring Coverage

To ensure your Fathead covers all the keywords and phrases you expect it to, you'll need to compile a list of them. This list will then be used by our test suite to ensure your Fathead has articles for each of the items in your coverage list, and will also help determine when the first phase is done.

Learn more about Fathead coverage [here](https://docs.duckduckhack.com/fathead-reference/creating-effective-fatheads.html#full-topic-coverage).


## Phase 2: Adding Article Redirects
Once your Instant Answer has gone live and we have some data about its performance, you will need to open another pull request that modifies your Fathead parsing script to add article redirects for common variations of the article titles that are already covered.

For example, it would be good to redirect `sqlalchemy datetime type` to the `sqlalchemy.types.DateTime` article. That way when someone searches "sqlalchemy datetime type", we would show an Instant Answer for `sqlalchemy.types.DateTime` class.

This is usually the longest phase and could involve several iterations, and multiple pull requests.

Learn more about article redirects [here](https://docs.duckduckhack.com/resources/creating-effective-fatheads.html).

### Note

Everytime a new iteration is released, it's good to check the coverage data in the Search Overview topic. It may take up to one week to see reliable results, and determine if any trends are forming. Ideally you will see an increase in coverage meaning there are fewer unanswered queries. Based on the data, it should be possible to spot patterns in the queries and determine if more redirects are needed.


## Phase 3: Addressing unanswered queries
After phase 2, there may still be unanswered queries. We're working to provide lists of categorized, unanswers queries to developers. Based on the queries, and the coverage data, we may need to iterate on phase 1 and 2, by covering more articles and creating additional redirects.

### Examples
The [JQuery Fathead](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/lib/fathead/jquery), written in Python, is a great example of what a reference Fathead should look like.

Here are other great Fatheads implemented in different languages:
 - [MDN CSS](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/lib/fathead/mdn_css) (Perl)
 - [Ruby Language](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/lib/fathead/ruby) (Ruby)
 - [PHP Language](https://github.com/duckduckgo/zeroclickinfo-fathead/blob/master/lib/fathead/php/parse.js) (Javascript - Node.js)
