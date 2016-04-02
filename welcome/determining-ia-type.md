# What Type of Instant Answer Should I Make?

There are two main types of Instant Answers you can develop: Goodies, and Spice.

The difference comes down to a simple question: **do you need to retrieve data from a third party API?**

## Goodie Instant Answers

Goodies **do not retrieve data from a third party API.** Goodies provide their results entirely through server-side code. They may use a [static data file](http://docs.duckduckhack.com/backend-reference/data-files.html) stored on DuckDuckGo's server, but they do not call external resources.

Learn how to make a Goodie with these walkthroughs:

- [Make a Quick Calculation Tool](http://docs.duckduckhack.com/walkthroughs/calculation.html)
- [Make a Word Count Tool (VIDEO)](http://docs.duckduckhack.com/walkthroughs/word-count-screencast.html)

**Cheat Sheets** are a subset of Goodies. [Learn to make a cheat sheet](http://docs.duckduckhack.com/walkthroughs/programming-syntax.html).

You can see examples of Goodies by filtering on the [Instant Answer Directory](https://duck.co/ia).

## Spice Instant Answers

Spices **retrieve data from third party APIs.** Spices provide their results via one or more calls to external endpoints. You can learn more about [how this works here](http://docs.duckduckhack.com/welcome/how-ias-work.html).

Learn how to make a Spice with these walkthroughs:

- [Make an API-Based Lookup](http://docs.duckduckhack.com/walkthroughs/forum-lookup.html)
- [Make an API-Based Generator](http://docs.duckduckhack.com/walkthroughs/random-person-screencast.html)

You can see examples of Spices by filtering on the [Instant Answer Directory](https://duck.co/ia).

## Fathead Instant Answers

> Fatheads are rare, and we don't recommend them for new contributors. If you're interested in making one, [talk to us on Slack]({{ book.slack-address }}) or [email us directly](mailto:open@duckduckgo.com) at open@duckduckgo.com.

Fatheads are key-value Instant Answers backed by a database on DuckDuckGo's servers. The keys of the database are typically words or phrases, and they are also used as the triggers for the Instant Answer. When a database key is queried, the corresponding row from the database is returned, which is typically a paragraph of text.

For more on Fathead Instant Answers, see the [Fathead overview](http://docs.duckduckhack.com/resources/fathead-overview.html).

## Longtail Instant Answers

> Longtails are rare, and we don't recommend them for new contributors. If you're interested in making one, [talk to us on Slack](mailto:QuackSlack@duckduckgo.com?subject=AddMe) or [email us directly](mailto:open@duckduckgo.com) at open@duckduckgo.com.

Longtails are database-backed, full text search, Instant Answers. For every query DuckDuckGo receives, each Longtail's database of articles is searched and any matching articles are used to display a paragraph of text, highlighting the portion of the article which matches the query.

For more on Longtail Instant Answers, see the [Longtail overview](http://docs.duckduckhack.com/resources/longtail-overview.html).

## Get in Touch

Want help? Need to think out loud? There are several ways to get in touch with staff, leaders, and community members. We look forward to hearing from you!

- **Slack**: Join our organization on Slack by [emailing us](mailto:QuackSlack@duckduckgo.com?subject=AddMe). We should respond within a day.
- **Mailing list**: [Get our developer newsletter](https://www.listbox.com/subscribe/?list_id=197814) (low traffic)
- **Meet Up**: Meet us at a [DuckDuckHack MeetUp group near you](http://www.meetup.com/pro/duckduckgo/) - or start a new one.
- **Twitter**: Tweet at us [@DuckDuckHack](https://twitter.com/duckduckhack/)
- **Email**: You can always send an [email](mailto:open@duckduckgo.com) to [open@duckduckgo.com](mailto:open@duckduckgo.com)
- **IRC**: #duckduckgo on freenode


*P.S. Let us know if we can improve anything in these documents [by opening issues directly on Github]( https://github.com/duckduckgo/duckduckhack-docs/issues/new).*
