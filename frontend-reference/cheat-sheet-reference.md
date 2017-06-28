# Cheat Sheets

A popular (and perfect) use of Goodies is to create cheat sheets which are available right from the DuckDuckGo search bar. To make adding a cheat sheet as quick as possible, we've brought all cheat sheets together under one Instant Answer, called the [Cheat Sheets Goodie](https://duck.co/ia/view/cheat_sheets).

![tmux cheat sheet](http://docs.duckduckhack.com/assets/tmux_cheat_sheet.png)

For detailed instructions on how to create a Cheat Sheet, follow any of the [Cheat Sheet Walkthroughs](http://docs.duckduckhack.com/walkthroughs/programming-syntax.html).

## Cheat Sheet Ideas

A cheat sheet is not always the best representation for your data. Sometimes, an Instant Answer is better built as a full Goodie or another type of Instant Answer. When thinking about your cheat sheet idea, think about what is useful to a searcher. Keyboard shortcuts, video game cheat codes, and similar data can be wonderfully useful as a cheat sheet.

Here are some other cheat sheet Instant Answers we love:

[Regex cheatsheet](https://duckduckgo.com/?q=regex+cheatsheet&ia=cheatsheet&iax=1)
[Anniversary cheatsheet](https://duckduckgo.com/?q=anniversary+cheatsheet&ia=cheatsheet)
[Cryptography cheatsheet](https://duckduckgo.com/?q=cryptography+cheatsheet&ia=cheatsheet&iax=1)
[Harry Potter cheatsheet](https://duckduckgo.com/?q=harry+potter+spells+cheatsheet&ia=cheatsheet)
[Tennis cheatsheet](https://duckduckgo.com/?q=tennis+cheatsheet&ia=cheatsheet)

You can also [check out all the Cheat Sheets that others have made](https://duck.co/ia?q=cheat+sheet) to inspire you for another topic.

Finally, the community has worked together on a [table showing programming-related IAs](https://github.com/duckduckgo/duckduckgo/wiki/Programming-IA-Coverage) - some great opportunities for cheat sheets!

## Creating a Cheat Sheet

*For detailed instructions on how to create a Cheat Sheet, follow any of the [Cheat Sheet Walkthroughs](http://docs.duckduckhack.com/walkthroughs/programming-syntax.html).*

All DuckDuckGo cheat sheets actually fall under one single Instant Answer - the Cheat Sheet Goodie. Each cheat sheet is defined in its own JSON file, in the [`/json`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/cheat_sheets/json) folder of the Cheat Sheet Goodie directory.

That means there's no need to create a new Instant Answer. There is also no need to edit the `CheatSheets.pm` file, `cheat_sheets.js`, or `cheat_sheets.css`. Simply save your new JSON file, and proceed to test your work.

## Easily Generate a Cheat Sheet Boilerplate File

[The `duckpan` tool](http://docs.duckduckhack.com/resources/duckpan-overview.html) helps make and test Instant Answers. To conveniently create the boilerplate specific to a cheatsheet, run **`duckpan new --cheatsheet`**:

```
[01:08 PM codio@border-carlo zeroclickinfo-goodies {master}]$ duckpan new --cheatsheet
Creating a new Cheat Sheet Instant Answer...
Please enter a name for your Instant Answer:
```

Type the name of your cheat sheet. The tool will do the rest:

```
Creating a new Cheat Sheet Instant Answer...
Please enter a name for your Instant Answer: regex1
Created files:
    share/goodie/cheat_sheets/json/regex1.json
Success!
```

That's convenient: The single file we need has been created, named, and located in the proper place in the repository. Internally, it contains correct boilerplate to save us time.

## How Are Cheat Sheets Triggered?

The [template type](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html#cheat-sheet-templates) along with the name and
aliases for your cheat sheet, determine how your cheat sheet can be triggered.

For example, the *vim* text editor cheat sheet uses the `keyboard` template type and can be triggered with the queries:

- "vim *cheatsheet*"
- "vim *cheat sheet*"
- "vim *shortcuts*"
- "vim *key bindings*"
- ...and so on.

*If you're curious you can view all terms listed in [triggers.yaml](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/triggers.yaml).*

If you'd like to add more names for the subject of your cheat sheet (in addition to the file name), you can specify them in the `aliases` property of your cheat sheet JSON file. For example, if your cheat sheet file is `lord-of-the-rings.json`, a natural alias is 'LOTR'. For details check out the [Cheat Sheet JSON Reference](#cheat-sheet-json-reference).

> Only use `aliases` to specify additional *names* for your topic (e.g. 'LOTR') and not trigger phrases (e.g. 'LOTR guide'). This is because any aliases will be automatically combined with the standard set of [cheat sheet trigger words](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/triggers.yaml).

If the default configuration for your cheat sheet does not provide the required triggering, additional customizations can be made in the [triggers file](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/triggers.yaml) where it is further documented.

> Not every cheat sheet will require this level of customization for the triggers. Please get in touch on [Slack]({{ book.slackURL }}) or [raise an issue](https://github.com/duckduckgo/zeroclickinfo-goodies/issues/new) if you wish to discuss additional triggering.

## Cheat Sheet JSON Reference

Below is a summary of the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json) file, which displays a cheat sheet when searching for ["vim cheat sheet"](https://duckduckgo.com/?q=vim+cheat+sheet&ia=answer).

![vim cheat sheet](http://docs.duckduckhack.com/assets/vim_cheat_sheet.png)

The above Instant Answer was created by simply adding [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json), explained below.

**For convenience, we encourage you to copy the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json) code into your new file, as a starting point.** Copy the [raw file](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json), as the JSON below won't work due to inline comments.

```javascript
{
    // Must match the id of the cheat sheet's IA page (Required)
    // For example, https://duck.co/ia/view/vim_cheat_sheet
    "id": "vim_cheat_sheet",

    // Displayed as title of AnswerBar (Required)
    "name": "Vim",

    // Displayed as subtitle of AnswerBar (Optional)
    "description": "Text Editor",

    // Displayed at bottom of AnswerBar, favicon shown automatically
    // (Required if cheat sheet has a source; useful to link users to further information.)
    "metadata": {
        "sourceName": "VimCheatSheet",
        "sourceUrl": "https://..." // Should be SSL if possible
    },

	// Add additional names for your cheat sheet (Optional)
	// Only use for additional *names* for your topic, as these will be automatically
	// combined with the standard set of cheat sheet triggers
	"aliases": [
        "vim", "vi improved", "vi text editor"
    ],

    // Pick the cheat-sheet template - explained below (Required)
    "template_type": "keyboard",

    // Controls which sections appear and in what order (Required)
    "section_order": [
        "Cursor movement",
        "Insert mode - inserting/appending text",
        // ...additional sections
        "Tabs"
    ],

    // Section names must match those in section_order in order to appear (Required)
    "sections": {
        "Tabs": [ // Section names should be Title Cased
            {
                "key": "#gt",
                "val": "move to tab number #"
            },
            {
                "key": "[Ctrl] [wt]",
                "val": "move the current split window into its own tab"
            }
            //...
        ],
        //...
    }
}
```

## Cheat Sheet Templates

We've seen a wonderfully wide variety of cheat sheets; we realized that one visual format doesn't fit all ideas. We've created a `template_type` property so you can pick the best display for your cheat sheet.

The `template_type` property also determines the [trigger terms](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html#how-are-cheat-sheets-triggered)
for your cheat sheet topic. These are in addition to several terms which trigger *all* cheat sheets (e.g. "cheat sheet").

Here are the available `template_type` values:

- `keyboard` - (see it live at ["vim cheatsheet"](https://duckduckgo.com/?q=vim+cheatsheet&ia=cheatsheet))

    * Example Triggers: "keyboard shortcuts", "key bindings", etc.

	![](https://docs.duckduckhack.com/assets/keyboard_template.png)

- `terminal` - (see it live at ["git cheatsheet"](https://duckduckgo.com/?q=git+cheatsheet&ia=cheatsheet))

    * Example triggers: "characters", "commands", etc.

	![](https://docs.duckduckhack.com/assets/terminal_template.png)

- `code` - (see it live at ["regex cheatsheet"](https://duckduckgo.com/?q=regex+cheat+sheet&ia=cheatsheet))

    * Example triggers: "syntax", "code snippets", etc.

	![](https://docs.duckduckhack.com/assets/code_template.png)

- `reference` - (see it live at ["wu-tang cheatsheet"](https://duckduckgo.com/?q=wu-tang+cheat+sheet&ia=cheatsheet))

    * Example triggers: "quick reference", "reference", etc.

	![](https://docs.duckduckhack.com/assets/reference_template.png)

- `language` - similar to reference, but with transliteration (`trn`) property (see it live at ["malayalam cheat sheet"](https://duckduckgo.com/?q=malayalam+cheat+sheet&ia=cheatsheet)).

    * Example triggers: "phrases", "translations", etc.

	![](https://docs.duckduckhack.com/assets/language_template.png)

- `link` - similar to reference, but with `link` URL property instead of `val`, which turns the `key` into a link (see it live at ["node tutorials cheat sheet"](https://duckduckgo.com/?q=node+tutorials+cheat+sheet&t=osx&ia=cheatsheet)).

    * Example triggers: "links", "sites", etc.

	![](https://docs.duckduckhack.com/assets/link_template.png)

The triggers given above are only a representative sample of the actual triggers that are applied by each template.
To see more of the triggers, check out the [triggers](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/triggers.yaml) file.

### The Language Template Transliteration (`trn`) Property

In addition to `key` and `val`, the Language template allows you to specify a third property: `trn`. This is intended for transliterations (see [full code](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/language/malayalam.json#L20) and [live example](https://duckduckgo.com/?q=malayalam+cheat+sheet&ia=cheatsheet)):

```javascript
{
    "key" : "I'm sorry",
    "val" : "എന്നോട് ക്ഷമിക്കൂ",
    "trn" : "Ennod kshamiku"
},
```

### The Link Template `link` Property

The Link template allows you to specify a `link` URL property *instead of `val`*. This turns the text in the `key` into a link (see [full code](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/nodejs-tutorials.json#L30) and [live example](https://duckduckgo.com/?q=node+tutorials+cheat+sheet&t=osx&ia=cheatsheet)):

```javascript
{
    "link": "http://nodeschool.io/",
    "key": "NodeSchool.io"
},
```

## Special Characters

### Escaping JSON Syntax Characters

Your cheat sheet might include characters which are themselves part of JSON syntax. To express these literally, escape them using backslashes, like [standard JSON](http://json.org):

- To express a double quote, use a single backslash: `\"`
- To express a forward slash, use a single backslash: `\/`
- To express a backslash, use a double backslash: `\\`
- For full list of characters, see the diagram on the right on [the official JSON documentation](http://json.org).

> See this [live example](https://duckduckgo.com/?q=common+escape+sequences+cheat+sheet&ia=cheatsheet&iax=1) of common escape sequences and its [corresponding code](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/common-escape-sequences.json).

### Code Blocks in the `key` Property

Cheat sheets display brackets `[ ]` and braces `{ }` as code blocks *when they are used in the `key` property*. To express those characters literally in the `key` property, using a **double backslash**:

- If you want to express a literal bracket, use a double backslash `[Ctrl]  {\\[}`.
- If you want to express a literal brace, use a double backslash `[Ctrl] [\\{]`.
- To express a **single literal backslash within a code block**, type four backslashes in a row: `[Ctrl] [\\\\]`.

*Note: It does not matter whether you use brackets or braces - they both wrap text in code blocks.*

> Note that an odd number of sequential backslashes will throw a parsing error, causing your cheat sheet not to display.

### Line Breaks and Tabs in the `key` Property

Newlines and tabs can be useful in many cases, including code blocks. The following work when used in the `key` property:

- Any literal `\n` in the JSON will be converted to a `<br>` in the generated HTML
- Any literal `\t` in the JSON will be converted to `&nbsp;&nbsp;` in the generated HTML

To display a literal `\n` or `\t` in your JSON, you need to escape the slash: `\\n` or `\\t`.

> See this [live example](https://duckduckgo.com/?q=common+escape+sequences+cheat+sheet&ia=cheatsheet&iax=1) of common escape sequences and its [corresponding code](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/common-escape-sequences.json).

### Arrow Keys

We've found the best way to express arrow keys is directly using ASCII characters (&larr;, &uarr;, &rarr;, &darr;). Feel free to copy and paste the characters from here.

For example, instead of **[Shift] [Up]** we recommend **[Shift] [&uarr;]**.

## Key Press Style Suggestions

Cheat sheets often list key combinations, which you can express in any way you choose. The following are only suggestions; choose the appropriate convention for your subject.

### Single Keys or Commands

There is no special syntax required for the string - for example, `"x"` or `":set color"`. The entire string will be shown in one code block.

### Simultaneous Keys (e.g., pressing A and B together)

We recommend expressing simultaneous key presses as follows:

- As adjacent code blocks, e.g. `"[Ctrl] [v]"`
- For "*nix-style" cheat sheets (like Emacs), as a single code block with a dash, e.g. `"[C-v]"`

### Consecutive Keys (e.g., pressing Ctrl+A, then pressing B)

We recommend expressing consecutive key presses as separate code blocks separated by a comma, e.g. `"[Ctrl] [A], [B]"`

### Alternative Keys (e.g., pressing either A or B)

We recommend displaying alternatives as follows:

- For single-key alternatives, wrap in parentheses, e.g. `[Ctrl] ( [L] / [P] )`
- For complete alternatives, we recommend replicating the key-value pair. Make an indication in the `val` that it's an alternative:

	```
	{
        "key": "[Ctrl] [j]",
        "val": "Jump"
    },
	{
        "key": "[Ctrl] [Spacebar]",
        "val": "Jump (alternative)"
    },
	```

