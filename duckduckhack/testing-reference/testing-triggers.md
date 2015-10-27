## Testing

Testing is crucial to ensuring a smooth integration process.  This section of the documentation walks you through the process of testing everything that you've written so far. Don't forget to write your test files!

## Interactive Testing

Interactive command-line testing is available using DuckPAN for **Goodie** and **Spice** Instant Answer types.

This section assumes you've set up your development environment and worked through either the [Basic Goodie Tutorial](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_basic_tutorial.md) or the [Basic Spice Tutorial](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_basic_tutorial.md).

1. Enter the root directory of your forked Instant Answer repository:

	Log in to Codio and visit the dashboard. In the menu, click Codio > [Dashboard](https://codio.com/home/projects)
	
	Click on the **DuckDuckHack project**, which you previously forked and cloned.
	
	Next, open a terminal window if it's not already open. (Tools > Terminal).
	
	At the command prompt, change into your repository directory, for example:
	
	```shell
	cd zeroclickinfo-goodies
	```

	The command line prompt will now indicate the repository and branch you are in, for example:
	
	```shell
	[ codio@border-carlo workspace zeroclickinfo-goodies {master}]$    
	```

2. Next, use the DuckPAN tool to test your triggers interactively:

    Type this command at the command line.

    ```shell
    duckpan query
    ```

    This command will present you with an interactive prompt.

    ```shell
    Loading Instant Answers...

    (Empty query for ending test)                                                   
	Query:
    ```

	*In some environments, the `duckpan query` command may print a long list of country aliases - that's perfectly fine. The end of the output will still display the `Query:` prompt.*

    **Now type in any query to see the response.** 

	Typing a query here is just like using DuckDuckGo.com, except you're only viewing the ZeroClickInfo response, and in its raw form.
	
	In the following example, we've entered `chars this is a test` into the prompt and received the following response:

    ```shell
    Query: chars this is a test

    DDG::ZeroClickInfo  {
        Parents       WWW::DuckDuckGo::ZeroClickInfo
        Linear @ISA   DDG::ZeroClickInfo, WWW::DuckDuckGo::ZeroClickInfo, Moo::Object
        public methods (3) : is_cached, new, ttl
        private methods (0)
        internals: {
            answer   14,
            answer_type   "chars",
            is_cached   1
        }
    }
    ```

    There can be a lot of debugging output. Pay special attention to the **internals** section.

    ```shell
        internals: {
            answer   14,
            answer_type   "chars",
            is_cached   1
        }
    ```

    Here you can see the answer returned, as well as any **zci** keywords (by default there will be an **answer\_type** and **is\_cached** value).

    A blank query will exit interactive mode.

    ```shell
    Query:

    \_o< Thanks for testing!
    ```
