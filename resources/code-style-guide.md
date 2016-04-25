# Code Style Guide

As a largely open-source project, we like to keep our code as consistent as our Instant Answers. This means all code should be formatted the same way and should look and feel as though it has all been written by the same person.

This document outlines some language specific guidelines for formatting your code and also highlights best practices, and things to avoid. In any large open-source project, maintainability is of utmost importance, so a style guide is necessary to help our contributors write clean, readable and maintainable code.

## General

- **Indent with 4 spaces** (soft tabs)

    All DuckDuckHack code should be indented with four spaces. Be sure to configure your text editor to insert four spaces when you press the tab button - this is referred to as a "soft-tab". If you are correcting the indentation of a file, please submit that change in a separate pull request. It is important that code reviewers are able to easily differentiate between functional and stylistic changes.

- **Document your code**

    Well-documented code helps others understand what you've written. It's likely that someone else will read your code and might even need to change it at some point in the future. Comments should primarily document the intent of the code. Reviewers are much more effective when they know exactly what you were trying to do. Meaningful variable names also help to document your intent.

- **Writing meaningful commits**

    Commit messages should be concise and informative. If the specific commit fixes a bug on GitHub, note that by saying `fixes #123`, where `123` is the issue number. Doing this will automatically close the specified issue when your pull request is merged.

    Usually pull requests only deal with a single Instant Answer. If however your pull request modifies more than one Instant Answer, please preface your commit messages with the name of the IA modified by your commit:

    For example, if your pull request updates the Movies, InTheaters and Kwixer IA's:

    - Commit 1: `Movies: updated title font color to match mockup`.
    - Commit 2: `InTheaters: updated title text, typo fix`.
    - Commit 3: `Movies, InTheaters, Kwixer: change title to h5 tag`.

## JavaScript

**We generally adhere to [Crockford's Code Conventions](http://javascript.crockford.com/code.html)**. Most importantly:

- Use semicolons;

- Use the ["One True Brace Style"](https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS) (opening brace on the same line)

    ```javascript
    // Bad
    if ( ... )
    {
        ...
    }
    else
    {
        ...
    }

    // Good
    if ( ... ) {
        ...
    } else {
        ...
    }
    ```

- Use `{}` instead of `new Object()`, and `[]` instead of `new Array()`.

    ```javascript
    // Bad
    var obj = new Object();
    var arr = new Array();

    // Good
    var obj = {};
    var arr = [];
    ```

- Use `===` instead of `==`, and `!==` instead of `!=`. [Why?](http://stackoverflow.com/a/359509/1998450)

    ```javascript
    // Bad
    if (foo == bar) { ... }
    if (foo != bar) { ... }

    // Good
    if (foo === bar) { ... }
    if (foo !== bar) { ... }
    ```

- Declare variables with var, chaining multiple declarations -- one per line:

    ```javascript

    // Bad
    var foo = 1;
    var bar = true;
    var baz = "string";

    // good
    var foo = 1,
        bar = true,
        baz = "string";

    // when initializing undefined variables
    var foo, bar, baz;
    ```

    Note: We're using ECMAScript's [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FFunctions_and_function_scope%2FStrict_mode), so you'll *need* to declare every variable with `var`.

- Avoid trailing commas

    We support all modern browsers, including IE 9, which breaks when it reaches a trailing comma in objects. It also treats trailing commas in arrays [differently than you might expect](http://www.akawebdesign.com/2011/06/23/the-curious-case-of-trailing-commas-in-ie/).

    ```javascript
    // Bad
    var foo = {
        a: 'b',
        c: 42, //<-- trailing comma
    };

    // Good
    var foo = {
        a: 'b',
        c: 42 //<-- no trailing comma
    };
    ```

- Use [`$.map()`](http://api.jquery.com/jQuery.map/) and [`$.each()`](http://api.jquery.com/jQuery.each/) instead of `Array.prototype.map()` and `Array.prototype.forEach()`, again for IE support.

- Avoid modifying object prototypes

    Do not modify the prototypes of objects which are defined outside of your code. For example, modifications to `Array.prototype` or `Spice` will affect the global scope and may cause problems. In general, we advocate the use of local, private functions instead.

- Define default properties when the object is created:

    ```javascript
    // Bad
    var bar = {};
    bar.a = 'b';
    bar.c = 42;

    // Good
    var foo = {
        a: 'b',
        c: 42
    };
    ```

- Store jQuery selectors:

    If you need to re-use a jQuery selector (e.g. `$('#myDiv')`), store it in a variable for speed and efficiency. Otherwise, jQuery will need to traverse the DOM each time you use the same selector.

    ```javascript
    // Bad
    // Traverse the DOM and find '#text_element'...
    $('#text_element').show();
    // ... now do all that work again!
    $('#text_element').html('abc');

    // Good
    // Traverse the DOM and find '#text_element', then store it in memory
    // Convention is to prefix variables with a '$' when they hold a jQuery object
    var $text_element = $('#text_element');
    $text_element.show();
    $text_element.html('abc');

    // Better
    // jQuery supports method chaining!
    $('#text_element').show().html('abc');

    ```

## Handlebars

Handlebars templates and Handlebars helpers should be easy to read and understand. Please:

- Put nested elements on new lines:

    ```html
    <!-- bad -->
    <ul>
    <li><a href="#">link text</a></li>
    <li><div><a href="#">other link text</a></div></li>
    </ul>

    <!-- good -->
    <ul>
        <li>
            <a href="#">link text</a>
        </li>
        <li>
            <div>
                <a href="#">other link text</a>
            </div>
        </li>
    </ul>
    ```

-  Define helper functions with `Spice.registerHelper`, instead of `Handlebars.registerHelper`:

    ```javascript
    // Bad
    Handlebars.registerHelper("spice_name_do_something", function(){ ... });

    // Good
    Spice.registerHelper("spice_name_do_something", function(){ ... });
    ```

- Namespace your helper functions:

    Handlebars helpers are all created in the same scope, so any two helpers with the same name will collide (we plan to fix this). This can be avoided by prepending your helpers with the name of your Spice IA.

    ```javascript
    // Bad
    Spice.registerHelper("do_something", function(){ ... });

    // Good
    Spice.registerHelper("spice_name_do_something", function(){ ... });
    ```

------

The easiest way to verify your code meets our style guide is to test it with [JSHint](http://jshint.com/).

## CSS

- All CSS should be "namespaced" with the container element.

    For Spices, use `.zci--spicename`, and for Goodies, use `.zci--answer`:

    ```css
    /* Stopwatch Spice */
    .zci--stopwatch .spice-pane {
        ...
    }

    /* Calendar Goodie */
    .zci--answer table.calendar {
        ...
    }
    ```

- Put multiple selectors on new lines for each rule:

    ```css
    /* Bad */
    .zci--stopwatch .spice-pane, .zci--stopwatch .spice-pane-right {
        ...
    }

    /* Good */
    .zci--stopwatch .spice-pane,
    .zci--stopwatch .spice-pane-right {
        ...
    }
    ```

- Avoid the use of vendor prefixes and experimental features. We strive for a uniform experience on all current browsers and your IA *must* work across them.

    When in doubt, [CanIUse](http://caniuse.com/) is a good resource for determining if prefixes are needed. We support IE 9+, and recent versions of Chrome, Firefox, Safari, and Opera.

    ```css
    /* Bad */
    .element {
        -webkit-border-radius: 45px;
        -o-border-radius: 45px;
        -moz-border-radius: 45px;
        -khtml-border-radius: 45px;
        border-radius: 45px;
    }

    /* Good */
    .element {
        border-radius: 45px;
    }
    ```

- Avoid using inline CSS. Custom CSS should be placed in a file (`/share/{goodie,spice}/my_ia/my_ia.css`) to be automatically included in the Instant Answer response.

## Perl

(This section is coming soon! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)
