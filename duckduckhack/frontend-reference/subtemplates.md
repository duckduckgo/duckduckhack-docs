# Using Sub-templates

Many [templates](/duckduckhack/frontend-reference/templates-reference.html) allow you to pass *sub-templates* to fill out particular features. For example, to render custom calls-to-action, render content, or decide how to display lists of values.

The [templates reference](/duckduckhack/frontend-reference/templates-reference.html) indicates which features can be passed a sub-template, and which can only be passed simple types.

## Specifying a Sub-template

Sub-templates are specified when [displaying your Instant Answer](/duckduckhack/frontend-reference/display-reference.html#templates-object-required), under the `options` object of the [`templates` property](/duckduckhack/frontend-reference/display-reference.html#templates-object-required). 

- The **name** of the property is the template feature where you're inserting the sub-template. 
- The **value** is the reference to the template.

For example, for the [Kwixer](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/kwixer.js) Instant Answer, the `buy` feature of the [`products_detail` template](/duckduckhack/frontend-reference/templates-reference.html#productsdetail-template) is set to the custom [`Spice.kwixer.buy` sub-template](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/buy.handlebars):

```javascript
templates: {
    ...
    options: {
        ...
        buy: Spice.kwixer.buy
    }
}
```

*Note that built-in sub-templates are specified as string values, and custom sub-templates are directly referenced as a function. More on these differences below.*

### Built-In Sub-templates

The Instant Answer framework provides several sub-templates which are available to use in particular templates. These are indicated, where relevant, in the [templates reference](/duckduckhack/frontend-reference/templates-reference.html).

For example, the [`list_detail` template](/duckduckhack/frontend-reference/templates-reference.html#list_detail-template) works well when the built-in [`record` template](/duckduckhack/frontend-reference/templates-reference.html#list_detail-template) is set as its `content` feature.

**Built-in sub-templates are referenced using strings.** For example, the [WHOIS Instant Answer](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js) sets the `content` feature of the [`list_detail` template](/duckduckhack/frontend-reference/templates-reference.html#list_detail-template) by naming it as a string:

```javascript
templates:{
    ...
    options:{
        ...
        content: 'record' // a string, because the record template is built-in
    }
}
```

### Custom Sub-templates

Your Instant Answer can supply its own custom-made sub-templates.

Custom handlebar sub-templates are placed in the `share/INSTANT_ANSWER_TYPE/INSTANT_ANSWER_NAME/` folder, right next to any JavaScript or CSS files. That way, they are accessible to be compiled in the frontend. For example, the path to the [Kwixer Instant Answer](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/kwixer.js) `buy.handlebars` template file is [`share/spice/kwixer/buy.handlebars`](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/kwixer).

**Custom sub-templates are set as function references.** Continuing our Kwixer example, the `buy.handlebars` sub-template is referenced in [kwixer.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/kwixer.js) like this:

```javascript
templates: {
    ...
    options: {
        ...
        buy: Spice.kwixer.buy // a function reference 
    }
}
```

Wondering why this is a variable path - and no '.handlebars' extension? That's because *handlebars* files are compiled into JavaScript functions so they can be used with data. Instead of referencing the file itself, we reference the resulting function. In this example, `share/spice/kwixer/buy.handlebars` is compiled and becomes available as `Spice.kwixer.buy`.

## Using Style Guide Elements

## Using Available Helpers

There are a variety of helper functions available to you to make creating sub-templates easier. Learn more about [handlebars helpers](/duckduckhack/frontend-reference/handlebars-helpers.html).
