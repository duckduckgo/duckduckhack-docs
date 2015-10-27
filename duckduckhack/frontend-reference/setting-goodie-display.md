# Displaying Your Goodie Instant Answer

*Making a Cheat Sheet? Skip to the [Cheat Sheet Reference](#).*

The final step in every Instant Answer is displaying it to the user. All Instant Answers display in the "AnswerBar", which is the area above the organic search results. The way each Instant Answer is displayed and behaves is determined by a set of [display options](#) and [events](https://duck.co/duckduckhack/display_reference#events). This document shows you how to set these options for a Goodie.

[Screenshot of answerbar just like spice]

## Easy Structured Responses

*If your answer requires html templates and special interactions, consider [setting display properties](#setting-display-properties-in-a-goodie).*

Many Goodies are simple operations that return a string response. For example, the [Flip Text Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/FlipText.pm):

![flip text goodie](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fflip_text_goodie.png&f=1)

Displaying such Goodies is easy. Instead of setting display properties, simply return three properties:

- Input (what the user typed in, perhaps highlighting how it was parsed)
- Operation (the term for what happened)
- Result (the final answer)

For example, for the Flip Text Goodie:

![flip text goodie diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fflip_text_goodie_diagram.png&f=1)

### Passing Structured Responses

Here is the return statement of the [Flip Text Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/FlipText.pm):

```perl
my $result = upside_down($input);

return $result, # text-only Goodie result, for the API
    structured_answer => {
        input     => [html_enc($input)],
        operation => 'Flip text',
        result    => html_enc($result),
    };
```

The following properties are returned in the `structured_answer` hash:

#### `input` [required, but can be empty] *array*

- Make sure to `html_enc()` any user input to prevent [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting)
- To avoid displaying an input, pass an empty array: `[]` (see the [GUID Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GUID.pm#L49))

#### `operation` [required] *string*

- Stated as a command, e.g. "Calculate", "Flip text", "URL decode", etc.

#### `result` [required] *string*

- Make sure to `html_enc()` input to display characters properly
- **Do not pass custom HTML in this string**; instead [specify](#setting-goodie-display-properties-in-the-frontend) a [template](https://duck.co/duckduckhack/templates_overview).

### Further Examples

Here are some more Goodies that make use of simple, structured responses:

- [URLDecode](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/URLDecode.pm#L49-L55)

	![goodie urldecode](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fgoodie_url_decode.png&f=1)

- [GUID](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GUID.pm#L46-L52)

	![goodie guid](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fgoodie_guid.png&f=1)
	
- [Calculator](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Calculator.pm)

	![goodie calculator](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fgoodie_calculator.png&f=1)

## Setting Display Properties in a Goodie

*If your Goodie is very simple, consider passing a [structured response](#easy-structured-responses) instead.*

When developing a Goodie, display options can be set either in your backend (Perl) or frontend (JavaScript) code. Most display properties can be set in either. Some Display properties, by their nature, can only [be set in the frontend](#setting-goodie-display-properties-in-the-frontend). 

Here is a quick summary of the break down of [display options](#):

<table class="table table-condensed">
    <thead>
        <tr>
            <th>Display Property</th>
            <th>Can Set in Perl (Backend)</th>
            <th>Can Set in JavaScript (Frontend)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>id</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>name</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>data</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>meta</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>templates</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>view</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>model</td>
            <td>&#10003;</td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>normalize</td>
            <td></td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>relevancy</td>
            <td></td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>sort_fields</td>
            <td></td>
            <td>&#10003;</td>
        </tr>
        <tr>
            <td>Events</td>
            <td></td>
            <td>&#10003;</td>
        </tr>      
    </tbody>
</table>

<!-- Markdown version

[Display Property](https://duck.co/duckduckhack/display_reference)|[Can Set in Perl (Backend)](#setting-display-properties-in-a-goodies-perl)|[Can Set in JavaScript (Frontend)](#setting-goodie-display-properties-in-the-frontend)
|--------------|:---:|:---:|
[`id`](https://duck.co/duckduckhack/display_reference#codeidcode-emstringem-required)|&#10003;|&#10003;
[`name`](https://duck.co/duckduckhack/display_reference#codenamecode-emstringem-required)|&#10003;|&#10003;
[`data`](https://duck.co/duckduckhack/display_reference#codedatacode-emobjectem-required)|&#10003;|&#10003;
[`meta`](https://duck.co/duckduckhack/display_reference#codemetacode-emobjectem-required)|&#10003;|&#10003;
[`templates`](https://duck.co/duckduckhack/display_reference#codetemplatescode-emobjectem-required)|&#10003;|&#10003;
[`view`](https://duck.co/duckduckhack/display_reference#codeviewcode-emstringem-optional)|&#10003;|&#10003;
[`model`](https://duck.co/duckduckhack/display_reference#codemodelcode-emstringem-optional)|&#10003;|&#10003;
[`normalize`](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional)| |&#10003;
[`relevancy`](https://duck.co/duckduckhack/display_reference#coderelevancycode-emobjectem-optional)| |&#10003;
[`sort_fields`](https://duck.co/duckduckhack/display_reference#codesortfieldscode-emobjectem-optional)| |&#10003;
[Events](https://duck.co/duckduckhack/display_reference#events)| |&#10003;
-->

## Setting Display Options on the Backend

*If your Goodie is very simple, consider passing a [structured response](#easy-structured-responses) instead.*

Most options can be defined in the Goodie's backend, the Perl file. These options are set by returning as a hash called `structured_answer` when the Perl file finishes running. This hash is returned alongside the `$plaintext` string version of your Goodie result, used for the API):

```perl
return $plaintext,
    structured_answer => {
        ...
    };
```

For an example of how this works, take a look at the final return statement of the [BPM to ms](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) Goodie Perl file.

Specifying options in Perl is the most straightforward method, but there are several optional properties that cannot be specified on the server-side. These must be [specified in the Goodie's frontend](#setting-goodie-display-properties-in-the-frontend), in a JavaScript file.

The following is a code summary of how the options covered in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference) are returned in your Goodie Perl file:

```perl
return $plaintext,
    structured_answer => {
        id => String,
        name => String,
        data => Array or Hash (in the case of a single item),
        meta => {
            searchTerm => String,
            itemType => String,

            primaryText => String,
            secondaryText => String,

            sourceName => String,
            sourceLogo => String,
            sourceUrl => String (url),
            sourceIcon => Boolean,
            sourceIconUrl => String (url),

            snippetChars => Integer
        },
        templates => {          
            group => String,
            options => Hash,

            # Note that while the following may reference JavaScript variables, 
            # they are still specified as strings in Perl

            item => String,
            item_custom => String,
            item_mobile => String,

            detail => String,
            detail_custom => String,
            detail_mobile => String,
            item_detail => String,

            variants => Hash,

            elClass => Hash,
        }

        view => String,
        model => String,
    };

```

For more information on each property and its usage, visit the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference).

## Setting Goodie Display Options on the Frontend

While most display properties can be set in a Goodie's Perl file, others by their nature must be specified in the frontend part of the code. These are:

- [Normalize function](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional)
- [Events](https://duck.co/duckduckhack/display_reference#events)
- [Relevancy](https://duck.co/duckduckhack/display_reference#coderelevancycode-emobjectem-optional)
- [Sort fields](https://duck.co/duckduckhack/display_reference#codesortfieldscode-emobjectem-optional)

To specify any of these, simply create a javascript file in `share/goodie/INSTANT_ANSWER_ID/INSTANT_ANSWER_ID.js`. For example, using the ["BP to ms" Instant Answer](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) as an example (where the `id` is set to `'bpmto_ms'`):

Create a file at `share/goodie/bpmto_ms/bpmto_ms.js`, which creates a namespace and a build function. 

```javascript
DDH.bpmto_ms = DDH.bpmto_ms || {}; // create the namespace in case it doesn't exist

DDH.bpmto_ms.build = function(ops) {
    
    return {
        // Specify any frontend display properties here
    };
    
};
```

The build function takes `ops` as an argument; this represents the `structured_answer` hash from the Perl as a JavaScript object.

Your build function returns an object with any frontend display properties you want to set. For example, you could set an [event](https://duck.co/duckduckhack/display_reference#events):

```javascript
return {
    onShow: function() {
        console.log("onShow for bpmto_ms");
    },
}
```

Or you could set a [`normalize` function](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional) - and so on:

```javascript
return {
	...
    normalize: function(item){
        return {
            title: item.heading
        };
    }
}
```

Additionally, it is worth noting that all of the display options specified in Perl could instead be specified in your JavaScript - if you so desired. 

For example:

```javascript
return {
    ...
    templates: {
        group: 'base',
        detail: false,
        options: {
            // Note that because this is JavaScript, sub-templates are specified
            // as function references rather than strings. 
            content: DDH.bpmto_ms.content
        }
    }
}
```

## Fun with Goodie JavaScript

Goodie's frontend components allow you to do much more than set display properties and events. You may also execute any JavaScript you'd like to do interesting and delightful things.

Continuing from the example above from the *BP to ms* Instant Answer, we created a JavaScript file at `share/goodie/bpmto_ms/bpmto_ms.js`. Inside this file, we declare a `build` function.

Everything *returned* by your `build` function is used to extend your `structured_answer` Perl hash (from your Goodie's .pm file). However, you can use the function to **run other JavaScript**, making use of JQuery.

```javascript
DDH.bpmto_ms.build = function(ops) {
    
    // Execute delightful JavaScript here
    // with access to JQuery 

    return {
        // Specify any frontend display properties here
		onShow: function(){
			// Consider using an event, such as onShow, to run your code at the right time
		}
    };

};
```

Consider using [events](https://duck.co/duckduckhack/display_reference#events) as the starting points for your code. You can also create a css file to reference, for example `share/goodie/bpmto_ms/bpmto_ms.css`.

You might use Goodie JavaScript to create an in-browser game related to certain search results. Or an easter egg, for fun. The community is excited to review pull requests for fun and delightful additions to DuckDuckGo's Instant Answers.

Feel free to reach out and ask us any questions, over at [open@duckduckgo.com](mailto:open@duckduckgo.com)


	
