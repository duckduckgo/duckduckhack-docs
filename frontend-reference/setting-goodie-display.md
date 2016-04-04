# Displaying Your Goodie Instant Answer

*Making a Cheat Sheet? Skip to the [Cheat Sheet Reference](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html).*

The final step in every Instant Answer is displaying it to the user. All Instant Answers display in the "AnswerBar", which is the area above the organic search results. The way each Instant Answer is displayed and behaves is determined by a set of [display options](http://docs.duckduckhack.com/frontend-reference/display-reference.html) and [events](http://docs.duckduckhack.com/frontend-reference/display-reference.html#events). This document shows you how to set these options for a Goodie.

![Goodie answerbar](http://docs.duckduckhack.com/assets/goodie_answerbar.png)

## Setting Display Properties in a Goodie

When developing a Goodie, display options can be set either in your back end (Perl) or frontend (JavaScript) code. Most display properties can be set in either. Some display properties, by their nature, can only [be set in the front end](#setting-goodie-display-properties-in-the-frontend).

Here is a quick summary of the break down of [display options](http://docs.duckduckhack.com/frontend-reference/display-reference.html):

<table class="table table-condensed">
    <thead>
        <tr>
            <th>Display Property</th>
            <th>Can Set in Perl (Back end)</th>
            <th>Can Set in JavaScript (Front end)</th>
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

## Setting Display Options on the Back End

Most options can be defined in the Goodie's back end, the Perl file. These options are set by returning as a hash called `structured_answer` when the Perl file finishes running. This hash is returned alongside the `$plaintext` string version of your Goodie result, used for the API):

```perl
return $plaintext,
    structured_answer => {
        ...
    };
```

Specifying options in Perl is the most straightforward method, but there are several optional properties that cannot be specified on the server-side. These must be [specified in the Goodie's front end](#setting-goodie-display-properties-in-the-frontend), in a JavaScript file.

The following is a code summary of how [display options](http://docs.duckduckhack.com/frontend-reference/display-reference.html) are set in your Goodie Perl file:

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

For an example of how this works, take a look at the final return statement of the [Unicornify](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Unicornify.pm) Goodie Perl file:

```perl
return "This is a unique unicorn for $_",
    structured_answer => {
        data => {
            subtitle => "Unique unicorn",
            title => "$_",
            url => unicornify_url(email => $_, size => "200"),
            image => unicornify_url(email => $_, size => "100")
        },
        meta => {
            sourceName => "Unicornify",
            sourceUrl => 'http://unicornify.appspot.com/'
        }, 
        templates => {
            group => "icon",
            item => 0,
            moreAt => 1,
            variants => {
                iconTitle => 'large',
                iconImage => 'large'
            }
        }
    }
```

For more information on each property and its usage, visit the [display options reference](http://docs.duckduckhack.com/frontend-reference/display-reference.html).

## Setting Goodie Display Options on the Front end

While most display properties can be set in a Goodie's Perl file, others by their nature must be specified in the front end part of the code. These are:

- [Normalize function](http://docs.duckduckhack.com/frontend-reference/display-reference.html#normalize-function-optional)
- [Events](http://docs.duckduckhack.com/frontend-reference/display-reference.html#events)
- [Relevancy](http://docs.duckduckhack.com/frontend-reference/display-reference.html#relevancy-object-optional)
- [Sort fields](http://docs.duckduckhack.com/frontend-reference/display-reference.html#sortfields-object-optional)

To specify any of these, simply create a JavaScript file in `share/goodie/INSTANT_ANSWER_ID/INSTANT_ANSWER_ID.js`. For example, using the ["BP to ms" Instant Answer](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) as an example (where the `id` is set to `'bpmto_ms'`):

Create a file at `share/goodie/bpmto_ms/bpmto_ms.js`, which creates a namespace and a build function.

```javascript
DDH.bpmto_ms = DDH.bpmto_ms || {}; // create the namespace in case it doesn't exist

DDH.bpmto_ms.build = function(ops) {

    return {
        // Specify any frontend display properties here
    };

};
```

The build function takes `ops` as an argument; this represents the `structured_answer` hash from the back end Perl file as a JavaScript object.

Your build function returns an object with any front end display properties you want to set. For example, you could set an [event](http://docs.duckduckhack.com/frontend-reference/display-reference.html#events):

```javascript
return {
    onShow: function() {
        console.log("onShow for bpmto_ms");
    },
}
```

Or you could set a [`normalize` function](http://docs.duckduckhack.com/frontend-reference/display-reference.html#normalize-function-optional) - and so on:

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

Goodie's front end components allow you to do much more than set display properties and events. You may also execute any JavaScript you'd like to do interesting and delightful things.

Continuing from the example above from the *BP to ms* Instant Answer, we created a JavaScript file at `share/goodie/bpmto_ms/bpmto_ms.js`. Inside this file, we declare a `build` function.

Everything *returned* by your `build` function is used to extend your `structured_answer` Perl hash (from your Goodie's .pm file). However, you can use the function to **run other JavaScript**, making use of jQuery.

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

Consider using [events](http://docs.duckduckhack.com/frontend-reference/display-reference.html#events) as the starting points for your code. You can also create a css file to reference, for example `share/goodie/bpmto_ms/bpmto_ms.css`.

You might use Goodie JavaScript to create an in-browser game related to certain search results. Or an easter egg, for fun. The community is excited to review pull requests for fun and delightful additions to DuckDuckGo's Instant Answers.
