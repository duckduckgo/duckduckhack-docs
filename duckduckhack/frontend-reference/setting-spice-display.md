# Displaying Your Spice Instant Answer

The final step in every Instant Answer is displaying it to the user. All Instant Answers display in the "AnswerBar", which is the area above the organic search results. The way each Instant Answer is displayed and behaves is determined by a set of [display options](#) and [events](https://duck.co/duckduckhack/display_reference#events). This document shows you how to set these options for a Spice.

Once your Instant Answer has been triggered, and the API request has returned a response to the client, the final step is to display your results onscreen.

![answerbar](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fanswerbar.png&f=1)

## Contents of the Spice Frontend Callback

The Spice frontend (Javascript) contains a callback which receives the results of the API call, and then displays your Spice. For an example of how the Spice frontend callback works, check out the [forum lookup](#) walkthrough.

The most important part of this callback, and often the only part, is calling [`Spice.add()`](#codespiceaddcode-overview). This function gives you a lot of control over your results' appearance, context, and user interactions.

## Available Options

The properties you can pass to the `Spice.add()` function are documented in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference). This document provides an in-depth overview of all that `Spice.add()` allows you to do.

In some scenarios, you may also want to handle the AnswerBar's events (for example, to stop media playing when the user hides your Instant Answer). These [events](https://duck.co/duckduckhack/display_reference#events) are covered at the end of the reference.

## Calling `Spice.add()`

The following is a code summary of how the options covered in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference) are passed to `Spice.add()`

```javascript
Spice.add({

	// Required properties:
	
    id: String,
    name: String,
    data: Array or Object (in the case of a single item),

    meta: {
        searchTerm: String,
        itemType: String,

        primaryText: String,
        secondaryText: String,

        sourceName: String,
        sourceLogo: String,
        sourceUrl: String (url),
        sourceIcon: Boolean,
        sourceIconUrl: String (url),

		snippetChars: Integer
    },

    templates: {
        group: String,

        item: String|Function,
        item_custom: String|Function,
        item_mobile: String|Function,

        detail: String|Function,
        detail_custom: String|Function,
        detail_mobile: String|Function,
        item_detail: String|Function,

        options: Object

        variants: Object
        
        elClass: Object
    },

    // Optional properties:

    normalize: Function,

    relevancy: {
        type: String,
        skip_words: [, String],
        primary: [, Object],
        dup: String,
    },

    view: String,
    model: String,

    sort_fields: Object,
    sort_default: String|Object,

    onItemSelected: Function,
    onItemUnselect: Function,
    onShow: Function,
    onHide: Function

});
```

For more information on each property and its usage, visit the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference).