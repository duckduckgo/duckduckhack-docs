# Goodie Cheat Sheets

A popular (and perfect) use of Goodies is to create cheat sheets which are available right from the DuckDuckGo search bar. To make adding a cheat sheet as quick as possible, we've brought all cheat sheets together under one Instant Answer, called the [Cheat Sheets Goodie](https://duck.co/ia/view/cheat_sheets).

![tmux cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftmux_cheat_sheet.png&f=1)

For detailed instructions on how to create a Cheat Sheet, follow any of the [Cheat Sheet Walkthroughs](#).

## Cheat Sheet Ideas

A cheat sheet is not always the best representation for your data. Sometimes, an Instant Answer is better built as a full Goodie or another type of Instant Answer. When thinking about your cheat sheet idea, think about what is useful to a searcher. Keyboard shortcuts, video game cheat codes, and similar data can be wonderfully useful as a cheat sheet. Here are some other cheat sheet Instant Answers we love: 

[Regex help](https://duckduckgo.com/?q=regex+help&ia=cheatsheet&iax=1)    
[Anniversary meanings](https://duckduckgo.com/?q=anniversary+help&ia=cheatsheet)  
[Cryptography terms and help](https://duckduckgo.com/?q=cryptography+cheat+sheet&ia=cheatsheet&iax=1)  
[Harry Potter spells](https://duckduckgo.com/?q=harry+potter+spells+cheat+sheet&ia=cheatsheet)  
[Tennis info](https://duckduckgo.com/?q=tennis+cheat+sheet&ia=cheatsheet)  

You can also [check out all the Cheat Sheets that others have made](https://duck.co/ia?q=cheat+sheet) to inspire you for another topic.

## Creating a Cheat Sheet

*For detailed instructions on how to create a Cheat Sheet, follow any of the [Cheat Sheet Walkthroughs](#).*

All DuckDuckGo cheat sheets actually fall under one single Instant Answer - the Cheat Sheet Goodie. Each cheat sheet is defined in its own JSON file, in the [`/json`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/cheat_sheets/json) folder of the Cheat Sheet Goodie directory.

That means there's no need to create a new Instant Answer. There is also no need to edit the `CheatSheets.pm` file, `cheat_sheets.js`, or `cheat_sheets.css`. Simply save your new JSON file, and proceed to test your work.

## How Are Cheat Sheets Triggered?

Triggering is already built in to the main Cheat Sheets Goodie. When the name of your cheat sheet file is searched together with any of the [built-in trigger words](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/CheatSheets.pm), your Instant Answer will be shown. 

For example, for the *vim* text editor, the Instant Answer will be triggered on: 

- "vim *cheatsheet*"
- "vim *cheat sheet*"
- "vim *commands*"
- "vim *guide*"
- "vim *shortcuts*"
- ...and so on. 

*If you're curious you can view all terms listed in [CheatSheets.pm](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/CheatSheets.pm).*

If you'd like to add more names for the subject of your cheat sheet (in addition to the file name), you can specify them in the `aliases` property of your cheat sheet JSON file. For example, if your cheat sheet file is `lord-of-the-rings.json`, a natural alias is 'LOTR'. For details check out the [Cheat Sheet JSON Reference](#cheat-sheet-json-reference).

## Cheat Sheet JSON Reference

Below is a summary of the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json) file, which displays a cheat sheet when searching for ["vim cheat sheet"](https://duckduckgo.com/?q=vim+cheat+sheet&ia=answer).

![vim cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvim_cheat_sheet.png&f=1)

The above Instant Answer was created by simply adding [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json), explained below. 

**For convenience, we encourage you to copy the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json) code into your new file, as a starting point.** Copy the [raw file](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/json/vim.json), as the JSON below won't work due to inline comments.

```javascript
{
    // Required; must match the id of the cheat sheet's IA page
    // For example, https://duck.co/ia/view/vim_cheat_sheet
    "id": "vim_cheat_sheet", 

    // Required; displayed as title of AnswerBar
    "name": "Vim",

    // Optional; displayed as subtitle of AnswerBar
    "description": "Text Editor", 
    
    // Required if cheat sheet has a source; useful to link users to further information.
    // Displayed at bottom of AnswerBar, favicon shown automatically
    "metadata": { 
        "sourceName": "VimCheatSheet",
        "sourceUrl": "https://..." // Should be SSL if possible
    },

	// Optional; add additional search triggers for your cheat sheet
	"aliases": [
        "vim", "vi improved", "vi text editor"
    ],

    // Optional; pick the cheat-sheet template (explained below)
    "template_type": "keyboard",

    // Required; controls which sections appear and in what order
    "section_order": [  
        "Cursor movement",
        "Insert mode - inserting/appending text",
        // ...additional sections
        "Tabs"
    ],

    // Required; section names must match those in section_order in order to appear
    "sections": {
        "Tabs": [
            {
                "key": "#gt", 
                "val": "move to tab number #"
            },
            {
                "key": "[Ctrl] [wt]",
                "val": "move the current split window into its own tab"
            }
            // ...additional entries
        ],        
        "Insert mode - inserting/appending text": [
            {
                "key": "i",
                "val": "insert before the cursor"               
            }, 
            {
                "key": "I",
                "val": "insert at the beginning of the line"
            }
            // ...additional entries
        ],  
        // ...additional sections
    }
}
```

### Cheat Sheet Templates

We've seen a wonderfully wide variety of cheat sheets; we realized that one visual format doesn't fit all ideas. We've created an *optional* `template_type` property so you can pick the best look for your cheat sheet.

![Cheat sheet template types](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fcheatsheet-template-types.png&f=1)

Here are the available `template_type` values:

- `keyboard` - the default (see it live at ["vim cheatsheet"](https://duckduckgo.com/?q=vim+cheatsheet&ia=cheatsheet))
- `terminal` - (see it live at ["git cheatsheet"](https://duckduckgo.com/?q=git+cheatsheet&ia=cheatsheet))
- `code` - (see it live at ["regex cheatsheet"](https://duckduckgo.com/?q=regex+cheat+sheet&ia=cheatsheet))
- `reference` - (see it live at ["wu-tang cheatsheet"](https://duckduckgo.com/?q=wu-tang+cheat+sheet&ia=cheatsheet))

### Syntax for `key` Property

Cheat sheet actions often have several key combinations, which you can indicate in the syntax of each `key` property.

**Brackets, `[ ]`, or braces, `{ }`, are used to wrap key combinations in code blocks.** For convenience, if you include no brackets or braces, the entire string will be shown in a code block.

*Note: It does not matter whether you use brackets or braces - they both wrap text in code blocks.*

#### Escaping Special Characters

Your cheat sheet might include characters which are themselves part of JSON syntax. To express these literally, escape them using backslashes, like [standard JSON](http://json.org):

- To express a double quote, use a single backslash: `\"`
- To express a forward slash, use a single backslash: `\/`
- For full list of characters, see the diagram on the right on [the official JSON documentation](http://json.org).

Because cheat sheets display brackets `[ ]` and braces `{ }` as code blocks, express those literally using a **double backslash**:

- If you want to express a literal bracket, use a double backslash `[Ctrl]  {\\[}`.
- If you want to express a literal brace, use a double backslash `[Ctrl] [\\{]`.
- To express a **single literal backslash**, type four backslashes in a row: `[Ctrl] [\\\\]`.

*Note that an uneven number of sequential backslashes will throw an error.*

### Formatting Key Presses

Cheat sheets often list key combinations, which you can express in any way you choose. The following are only suggestions; choose the appropriate convention for your subject.

#### Single Keys or Commands

There is no special syntax required for the string - for example, `"x"` or `":set color"`. The entire string will be shown in one code block.

#### Simultaneous Keys (e.g., pressing A and B together)

We recommend expressing simultaneous key presses as follows: 

- As adjacent code blocks, e.g. `"[Ctrl] [v]"`
- For "*nix-style" cheatsheets (like Emacs), as a single code block with a dash, e.g. `"[C-v]"`
	
#### Consecutive Keys (e.g., pressing A, then pressing B)

We recommend expressing consecutive key presses as separate code blocks separated by a comma, e.g. `"[Ctrl-B], [x]"`
	
#### Alternative Keys (e.g., pressing either A or B)

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

#### Arrow Keys

We've found the best way to express arrow keys is directly using arrow ASCII characters (&larr;, &uarr;, &rarr;, &darr;). Feel free to copy and paste the characters from here.

For example, instead of **[Shift] [Up]** we recommend **[Shift] [&uarr;]**.
