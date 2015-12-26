# How to Make a Programming Cheat Sheet

It's always delightful when search results answer our question in fewer steps than we expected. Programming language Cheat Sheets are no exception. Naturally, our community would love to encourage more of them ([we even made a table](https://github.com/duckduckgo/duckduckgo/wiki/Programming-IA-Coverage)).

Cheat Sheets are the easiest type of Instant Answer to contribute. There are several kinds you can make: reference cheat sheets, language cheat sheets, key bindings, in addition to programming cheat sheets. In this tutorial, we'll learn how the Regular Expressions Cheat Sheet was made. 

![](http://docs.duckduckhack.com/assets/regex cheat sheet.png)

## How Cheat Sheets Work

Cheat Sheets trigger when users search for their topic together with keywords such as "help", "commands", "guide", "reference", and "syntax" (check out the [full list of terms](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/CheatSheets.pm#L14)). For example, searching for "regex help" would trigger the Regex Cheat Sheet Instant Answer.

Learn more about [how to trigger your Cheat Sheet](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html#how-are-cheat-sheets-triggered) in the reference.

## Anatomy of a Cheat Sheet

Cheat sheets only require you to add one file with the information to present. In our case, that would be `regex.json`.

File | Purpose | Location
-----|---------|---------
[`regex.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/regex.json)|Specify cheat sheet info and display settings|Placed inside the Cheat Sheets Goodie directory: [`zeroclickinfo-goodies/share/goodie/cheat_sheets/json/`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/)

## Set Up Your Development Environment

Before we begin coding, we'll need to set up our development environment. There are three main steps:

1. Fork the Goodie repository on Github.com. ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#1-fork-the-appropriate-repository-on-githubcom))
2. Set up the DuckDuckHack environment on Codio.com ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#2-set-up-the-duckduckgo-environment-on-codiocom))
3. Clone your Github fork onto the Codio environment. ([How?](http://docs.duckduckhack.com/welcome/setup-dev-environment.html#3-clone-your-github-fork-onto-the-codio-environment))

If this is your first time developing an Instant Answer, check out our [detailed, step-by-step guide](http://docs.duckduckhack.com/welcome/setup-dev-environment.html) to getting your development environment set up.


## Create a JSON File

In Codio, use the left-hand panel to navigate to the `/zeroclickinfo-goodies` repository directory. Then use the file tree to click into the `/share/goodie/cheat_sheets` directory. Finally, click the **json** folder. 

Up in the **File menu**, click **"Create New File"**, and enter the name of your cheat sheet as a JSON file (make sure it's saving to the `cheat_sheets/json` directory). In our case, since our topic is 'regex', we'll name our file `regex.json`.

Erase any pre-filled contents that Codio might have inserted, and replace with the open and close brackets, indicating a JSON object.

```javascript
{
    
}
```

## Add Metadata

Let's add the metadata for our cheat sheet - the information that helps classify, organize, and display our Instant Answer. Start by entering a unique `id` for your Cheat Sheet:

```javascript
{
    "id": "regex_cheat_sheet",
}
```

Next, add a name and description for your Instant Answer:

```javascript
{
    "id": "regex_cheat_sheet",
    "name": "Regex Cheat Sheet",
    "description": "Regular expression syntax",
}
```

Let's cite a source and link for our information, whenever possible, under `metadata`:

```javascript
{
    ...
    "metadata": {
        "sourceName": "Cheatography",
        "sourceUrl": "http://www.cheatography.com/davechild/cheat-sheets/regular-expressions/"
    },
}
```

## Add Cheat Sheet Settings

Right now, since we named our file `regex.json`, our Cheat Sheet will trigger on phrases like 'regex guide' or 'regex syntax'. If we want it to trigger on words other than 'regex,' we can specify aliases. Add the following property under `metadata`:

```javascript
{
	...
	"aliases": [
	    "regexp", "regular expression", "regular expressions"
	]
}
```

Next, we decide the form in which the cheat sheet will be displayed. There are four cheat sheet template types:

![Cheat sheet template types](http://docs.duckduckhack.com/assets/cheatsheet-template-types.png)

We'll choose the 'code' template, because it fits our content the best:

```javascript
{
	...
	"template_type": "code",
}
```

## Fill Out Content

Now it's time to fill in our Cheat Sheet's helpful content. This is done as an object, under the `sections` property. Each section is a key-value pair of the section's name, and an array:

```javascript
{
	...
	"sections": {
	    "Assertions": [
    
	    ],
	    "POSIX Classes": [
    
	    ]
	}
}
```

Each section's array lists objects, each with `key` and `val` properties. These contain our visible content:

```javascript
{
	...
	"sections": {
	    "Assertions": [
	        {
	            "val": "Lookahead assertion",
	            "key": "?="
	        }, {
	            "val": "Negative lookahead",
	            "key": "?!"
	        },
			...
	    ],
		...
	}
}
```

You can see (and copy-paste) the full contents of the `sections` property in the [`regex.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/regex.json) file on Github. The full JSON syntax for entering this information is documented in the [Cheat Sheets reference page](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html).

Finally, we can specify precisely in what order to display sections using the `section_order` property.

```javascript
{
	...
	"section_order": ["Anchors", "Character Classes", "POSIX Classes", "Pattern Modifiers", "Escape Sequences", "Quantifiers", "Groups and Ranges", "Assertions", "Special Characters", "String Replacement"]
}
```

*Important note: In order to be displayed, every section in `sections` must appear in `section_order`.*

## Validate Your Cheat Sheet

Let's make sure our contribution is formatted properly and follows [all rules](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html). If something should fail, please refer to the [Cheat Sheet reference page](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html).

1. **Validate your JSON** - You can easily do this by copying your file contents and pasting it into [jsoneditoronline.org](http://jsoneditoronline.org/) to make sure it's valid JSON.

2. **Validate your Cheat Sheet Code** - the following command will check the file formatting and make sure everything is consistent, and all required properties are present. For example, in addition to formatting, it will check that all sections declared also exist, and vice versa.

	Since the Cheat Sheet Goodie already exists, the test file is already written. All you need to do is enter the following into your Codio terminal:
	
	```
	prove t/CheatSheets/CheatSheetsJSON.t :: vim
	```

That's it! You're ready to try out your cheat sheet.

## Interactively Test Your Cheat Sheet

Let's see our Cheat Sheet in action. To do this, we'll create a test server that will allow you to view your Instant Answer as it would appear above DuckDuckGo search results.

1. In Codio, open your Terminal by clicking on **Tools > Terminal**.

	![](http://docs.duckduckhack.com/assets/terminal menu.png)

2. Change into the `zeroclickinfo-goodies` directory by typing `cd zeroclickinfo-goodies` at the command line.
3. Next, type **`duckpan server`** and press "**Enter**". The Terminal should print some text and let you know that the server is listening on port 5000.

    ```
    Starting up webserver...
    You can stop the webserver with Ctrl-C
    HTTP::Server::PSGI: Accepting connections at http://0:5000/
    ```

4. Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type **"regex cheat sheet"** and press "**Enter**".

	![](http://docs.duckduckhack.com/assets/duckpan server.png)	

5. You should see your cheat sheet show up in the search results! **Make sure it displays correctly; check that all escaped characters and code blocks appear as you intended.**

6. When you're done testing, go back to the Terminal, and press "**Ctrl+C**" to shut down the DuckPAN Server. The Terminal should return to a regular command prompt.

7. Run the Test File

Congrats - you've made a working Instant Answer! 

If you've made an original cheat sheet, find out how to [make it live on DuckDuckGo.com](http://docs.duckduckhack.com/submitting/submitting-overview.html).

[![slack](http://docs.duckduckhack.com/assets/slack.png) Have questions? Talk to us on Slack](mailto:QuackSlack@duckduckgo.com?subject=AddMe) or [email us](mailto:open@duckduckgo.com).
