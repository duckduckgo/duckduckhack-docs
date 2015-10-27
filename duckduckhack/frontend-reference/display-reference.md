# Instant Answer Display Reference

The Instant Answer framework gives you many options for displaying your results in the DuckDuckGo AnswerBar. Below is a detailed reference of the properties and usage of each.

Each Instant Answer has its own ways of declaring these options. We strongly recommend starting with the appropriate usage section, depending on your Instant Answer type:

- [Goodie Display](https://duck.co/duckduckhack/goodie_displaying)
- [Spice Display](https://duck.co/duckduckhack/spice_displaying)

These sections explain how to display each Instant Answer, as well as code samples involving the options in this reference.

## Display Properties

Each Instant Answer is added to the AnswerBar by passing a set of properties to the Instant Answer Framework.

The following properties are **required**:

- [id](#codeidcode-emstringem-required) - A unique identifier for your Spice. The `id` should match the name of your callback function
- [name](#codenamecode-emstringem-required) - The name that will be used for your Spice's AnswerBar tab
- [data](#codedatacode-emobjectem-required) - The object containing the data to be used by your templates
- [meta](#codemetacode-emobjectem-required) - Used to define elements of the **MetaBar** including the "More at" link
- [templates](#codetemplatescode-emobjectem-required) - Used to specify the template group and all other templates that are being used

The following properties are **optional**:

- [normalize](#codenormalizecode-emfunctionem-optional) - This allows you to normalize the `data` before it is passed on to the template
- [relevancy](#coderelevancycode-emobjectem-optional) - Used to ensure the relevancy of your Spice's result
- [sort_fields](#codesortfieldscode-emobjectem-optional)
- [view](#codeviewcode-emstringem-optional) - This allows you to explicitly specify the view class used for displaying the Instant Answer
- [model](#codemodelcode-emstringem-optional) - This allows you to use one of our predefined data models that include domain specific helpers/normalization/formatting.
- You may also optionally handle several of the AnswerBar's frontend [events](#events).

------

## `id` *string* [required]

A unique identifier for your Instant Answer. 

### Notes for Spice Instant Answers

The `id` should match the name of your callback function. For example, if your callback function is named `ddg_spice_name`, your `id` should be `spice_name`.

------

## `name` *string* [required]

The name that will be used **in the tab** above the Instant Answer, in the AnswerBar. 

**Tab names should ideally be one word nouns** (Images, Videos, Products, Audio, Answer, News, etc.) that describe the type of content being shown. 

**We will not accept brand names for tabs.** Instead, it's best to use the general topic name. For example, 'videos' for YouTube, 'gaming' for Twitch, 'products' for Amazon, and so on.

If none of the topics below apply to your results, or need help, we recommend choosing "Answer" for the time being, and [contacting us](mailto:open@duckduckgo.com) to brainstorm.

To get an idea for choosing a good name, here are some examples:

<table class="table table-condensed"> 
    <thead>
        <tr>
            <th>Spice IA</th>
            <th>`name`</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>GitHub</td>
            <td>'Software'</td>
        </tr>
        <tr>
            <td>Last.fm</td>
            <td>'Music'</td>
        </tr>
        <tr>
            <td>HackerNews</td>
            <td>'News'</td>
        </tr>
        <tr>
            <td>Twitter</td>
            <td>'Social'</td>
        </tr>
        <tr>
            <td>Amazon</td>
            <td>'Products'</td>
        </tr>
    </tbody>
</table>

Ideally your Instant Answer `name` should be one of the existing topics:

- Answer
- Apps
- Audio
- Computing
- Cryptography
- Currency
- Dictionary
- Domain
- Entertainment
- Finance
- Food & drink
- Games
- Geek 
- Geography
- Health 
- Images 
- Jobs
- Literature
- Local
- Math
- Movies
- Music
- News
- Politics
- Productivity
- Products
- Programming
- Recipes
- Reference
- Science
- Social
- Software
- Special interest
- Sports
- Statistics
- Sysadmin
- Tools
- Travel
- Tv
- Videos
- Weather
- Web design
- Words & games

------

## `data` *object* [required]

The object containing the data to be used by your templates. In most cases, it is best to pass along `api_result` to `data`, so that all of your API response is accessible to your templates.

------

## `meta` *object* [required]

The following options are used to define elements of the MetaBar including the "More at" link. 

![metabar example](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fmetabar.png&f=1)

![metabar item example](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fmetabar_item.png&f=1)

The following are all properties of the `meta: {}` object.

- ### `sourceName` *string* [required for Spice, optional for Goodie]

    The name of the source as it should be shown in the "More at" link. For example, in "More at Quixey", "Quixey" [is specified](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js#L77) as `sourceName`.

	#### Notes for Goodie Instant Answers
	
	While Goodies don't, by definition, have external data sources, you may still decide to specify `sourceName` and `sourceUrl` (below). For example, the [BPM to ms](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) instant answer ([search for "120 bpm to ms"](https://duckduckgo.com/?q=120+bpm+to+ms&ia=music)) specifies Wikipedia as the source, and links to an article that explains the calculation performed by the Goodie.
	
	**For the best experience, if a relevant Wikipedia page, or authoritative explanation, exists for your Goodie, you should provide it as a `sourceName` and `sourceUrl`.**

- ### `sourceUrl` *url string* [required for Spice, optional for Goodie]

	The URL to follow when the "More at" link is clicked. This value is the `href` attribute of the "More at" link. This can refer to the main page of the source, or better yet, the specific page relevant to the user's query. 
	
	A secure **https://** connection should be used whenever possible.

	#### Examples
	
	- In [rand_word.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rand_word/rand_word.js#L14), the `sourceUrl` is a hardcoded address.
	- In [is_it_up.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/is_it_up/is_it_up.js#L15), the `sourceUrl` is dynamically generated to direct to a specific page relating to the search query.

- ### `searchTerm` *string* [optional]

	Determines the **modifier** in the MetaBar's description: "Showing 15 `itemType` for `searchTerm`".
	
    The `searchTerm` is used to describe the `itemType` and it can be determined by removing any skip words from the original query.

	For example, searching ["alternatives to emacs"](https://duckduckgo.com/?q=alternative+to+emacs&ia=software), will display the description "Showing 12 Alternatives for **GNU Emacs**" in the MetaBar. In this case, the phrase "GNU Emacs" is the `searchTerm`.
	
	![metabar description](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fmetabar_description.png&f=1)
	
	If no `searchTerm` is specified, the description will simply read "Showing 12 Movies" or, if no `itemType` specified, "Showing 12 Items".
	
	#### Examples 

	- In [news.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/news/news.js#L89), `searchTerm` is passed the search query after some basic cleanup.
	- In [images.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/images/images.js#L19), `searchTerm` is passed the original query as-is.
	- In [alternative_to.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js#L16), `searchTerm` is passed a name provided by the API.
	- In [songkick_geteventid.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/songkick/geteventid/songkick_geteventid.js#L38), `searchTerm` is passed a city name.

- ### `itemType` *string* [optional]

    Determines the **noun** in the MetaBar's description: "Showing 15 `itemType` for `searchTerm`". In other words, `itemType` is the type of item being shown (e.g., Videos, Images, Recipes).
	
	Searching for ["alternatives to emacs"](https://duckduckgo.com/?q=alternative+to+emacs&ia=software), "Showing 12 **Alternatives** for GNU Emacs", the word "Alternatives" is the `itemType`.
	
	If no `itemType` is specified, the default itemType is 'Items'. For example, the MetaBar description will read "Showing 12 Items", or "Showing 12 Items for Electronics" when a `searchTerm` is provided.
	
	#### Examples
	
	- In [news.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/news/news.js#L90), the `itemType` is `'News articles'`.
	- In [alternative_to.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js#L17), the itemType is `'Alternatives'`.

- ### `primaryText` *string* [optional]

    If defined, this text will replace the MetaBar's "Showing **n** Items" text. 

	#### Example

	- In [parking.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js#L89), the `primaryText` is set to `'Parking near'` plus the location.

- ### `secondaryText` *string* [optional]

    This is an optional text label, displayed to the left of the "More at" link. For example, a weather forecast Instant Answer might use this to indicate the temperature unit, such as "Temperature in F&deg;".

- ### `sourceLogo` *url string* [optional]

    If defined, the image provided will replace the `sourceName` with a logo. Generally this is not necessary; in rare cases, API providers require that a specific image be used to represent their brand.

	#### Example
	
	From [quixey.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js#L79):
	
    ```javascript
    meta:{
        ...
        sourceLogo: {
            url: DDG.get_asset_path('quixey','quixey_logo.png'),
            width: '45',
            height: '12'
        }
    }
    ```
	
	This is the [result](https://duckduckgo.com/?q=money+apps&ia=apps):
	
	![sourcelogo](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fsourcelogo.png&f=1)

- ### `sourceIcon` *boolean* [optional]

    A boolean flag that determines if a favicon should be shown to the left of the "More at" link. The favicon is determined automatically by DuckDuckGo based on the `sourceUrl`. 

	When a `sourceUrl` is given, this will default to `true`. It should only be set to `false` when the `sourceUrl` domain does not have a favicon.

- ### `sourceIconUrl` *url string* [optional]

    If the `sourceUrl` domain has no favicon (or if a different favicon is preferred), you can explicitly set a url path for the favicon shown to the left of the "More at" link. This value, if set, will take precedence any favicons pulled from the `sourceUrl` domain.

- ### `snippetChars` *integer* [optional]

    For blocks of text that require truncation, `snippetChars` allows you to specify the maximum number of characters before truncation (to whole words with ellipses). This applies mainly to `description` elements in templates.

	This property is expected to be used in rare cases. Each template comes with its own optimal, default `snippetChars` value.
	
- ### `pinIcon` *string* [optional]

	Specifies the class of the [built-in icon](https://duckduckgo.com/styleguide#icons) to use as the map pin. If you are using the [Places Template Group](https://duck.co/duckduckhack/template_groups#places-template-group), which displays an interactive map, use this to specify which built-in icon you'd like used to mark locations.
	
	This takes a CSS class name of the built-in icon to use. You can find the icons listed in the [style guide](https://duckduckgo.com/styleguide#icons). For example: 
	
	```javascript
	meta: {
	    ...
	    pinIcon: 'ddgsi-circle',
	    pinIconSelected: 'ddgsi-star'
	}
	```

- ### `pinIconSelected` *string* [optional]

	Same as `pinIcon`, but for selected pins. When focusing on a particular location, use this icon to highlight the corresponding pin on the map.
	
------

## `templates` *object* [required]

A `templates: {}` property should be used to specify the [template group](https://duck.co/duckduckhack/template_groups#template-groups-reference), and/or other templates that are being used. 

Template `options` can also be provided to enable or disable features depending on the chosen template group. 

More about how templates work can be found in the [Template Overview](https://duck.co/duckduckhack/templates_overview).

***Note for Goodie Instant Answers:** Several properties below allow you to specify a function datatype, in order to reference a custom handlebars template. However, if you intend to do this in a Goodie Perl file, you must pass the name *as a string* in order to work.*

<!-- /summary -->

- ### `group` *string* [required, unless `item` and `detail` are specified]

    Setting the `group` property specifies a preset group of default templates and options (for example, `item`, `detail`, `options` etc.). These presets can be customized and manually overridden. The template groups available are described in the [Template Groups Overview](https://duck.co/duckduckhack/template_groups).

    For example, `group: 'info'` will implicitly set:

    ```javascript
    templates:{
        item: 'basic_item',
        item_detail: 'basic_info_item_detail',
        detail: 'basic_info_detail'
    }
    ```

- ### `item` *string (template name)* or *function (template reference)* [required if no `group` is specified]

    The template to be used for each item in a tile view.

    **Note:** The `item` template is only used when your Instant Answer returns multiple items (like the [recipe](https://duckduckgo.com/?q=quinoa+recipes&ia=recipes) or [BPM to ms](https://duckduckgo.com/?q=120+bpm+to+ms&ia=music) Instant Answers). This means the object passed to `data` is **an array with more than one element**.

    - Generally, a string is provided to indicate the name of the built-in template to be used, e.g., "products_item"

    - In rare cases, where necessary, a function referencing a custom template can be passed. Passing a custom template is a measure of last resort due to maintenance difficulty. Learn more about [picking templates](https://duck.co/duckduckhack/template_groups#picking-a-template-group); if you feel that no current templates fit your idea, please contact us at [open@duckduckgo.com](mailto:open@duckduckgo.com) and we'll happily help you find a solution.

- ### `item_mobile` *string (template name)* or *function (template reference)* [optional]

    An alternative `item` template to be used when displaying on smaller screens, such as mobile and hand-held devices.

- ### `detail` *string (template name)* or *function (template reference)* [required if no `group` is specified]

    The template to be used for the detail area. Find out more about when the `detail` template is displayed in the [templates overview](https://duck.co/duckduckhack/templates_overview#specifying-codeitemcode-and-codedetailcode-templates)

	    If your Instant Answer only returns a single item, a `detail` template is **required**. If your Instant Answer usually returns multiple items, the `detail` template is **optional**.

- ### `detail_mobile` *string (template name)* or *function (template reference)* [optional]

    An alternative `detail` template to be used when displaying on smaller screens, such as mobile and hand-held devices.

- ### `item_detail` *string (template name)* or *function (template reference)* [optional]

    An alternative `detail` template to be used when a tile is clicked. Learn more about when `item_detail` is used in the [templates overview](https://duck.co/duckduckhack/templates_overview#clicking-on-an-item).

- ### `options` *object* [optional]

    Allows you to explicitly disable or enable the [available features](https://duck.co/duckduckhack/templates_reference) of your template using boolean values or by specifying sub-templates to include.

	For example, you might set the the `content` feature of the [`basic_info_detail`](https://duck.co/duckduckhack/templates_reference#codebasicinfodetailcode-template) template to a particular sub-template, and enable the `rowHighlight` feature.
	
	For example:
	
	```javascript
    templates: {
        group: 'info',
        options: {
            content: 'record',
            rowHighlight: true
        }
    }
	```

	Available features will vary with each chosen template (see the [templates reference](https://duck.co/duckduckhack/templates_reference) for details on each template). For example, the `basic_info_detail` template doesn't have a `brand` feature, so setting `brand: true` or `brand: false` will have no effect.
	
	It's important to note that **there are implicit [default options](https://duck.co/duckduckhack/templates_overview#a-note-on-default-template-options)** which apply in the absence of an `options` object or a templates `group`.
	
	- ### `moreText` *string* or *object* or *array* [optional]

		Display additional text or link content adjacent to the ['More at' link](#codemetacode-emobjectem-required).
		Note that `moreText` is nested under the `options` property.

		For text alone, pass a string:

	    ```javascript
	    templates: {
	        ...
	        options: {
	            moreText: "Movie showtimes are shown in PST time zone"
	        }
	    }
	    ```

	    To display a link, pass an object:

	    ```javascript
	    templates: {
	        ...
	        options: {
	            moreText: {
	                text: "See a 10-day surf forecast"
	                href: "https://..." // Use SSL when possible
	            }
	        }
	    }
	    ```

	    To display multiple values (either text or links), pass an array:

	    ```javascript
	    templates: {
	        ...
	        options: {
	            moreText: [
	                {
	                    text: "See a 10-day surf forecast"
	                    href: "https://..." // Use SSL when possible
	                },
	                {
	                    text: "Global Swell Chart"
	                    href: "https://..."
	                },
	                "Subject to local conditions"
	            ]
	        }
	    }
	    ```

		Multiple values will be separated by a '|' and display as follows:

		[More at Surfline](http://example.com) | [See a 10-day surf forecast](http://example.com) | [Global Swell Chart](http://example.com) | Subject to local conditions


- ### `variants` *object* [optional]

	If you'd like to modify a template's visual appearance to fit your needs, the Instant Answer framework offers preset options called [Variants](https://duck.co/duckduckhack/templates_reference#variants). Variants are passed as the `variants` property of `templates`. 
	
	Variants correspond to pre-determined css classes (or combinations of classes) from the [DDG style guide](https://duckduckgo.com/styleguide) that work particularly well in each context.
	
	For more on the options and usage of `variants`, visit the [templates reference](https://duck.co/duckduckhack/templates_reference#variants).

- ### `elClass` *object* [optional]

	When variants don't suffice in customizing your templates' appearance, you may [directly specify classes](https://duck.co/duckduckhack/templates_reference#directly-specifying-classes) from the [DDG style guide](https://duckduckgo.com/styleguide) through the `elClass` property of `templates`. *This feature is mainly used for specifying text size and color.*

	These custom classes can be directly specified on the same template features available to Variants; the locations are identical. If you are specifying both `variants` and `elClass`, both will be applied together.
	
	For more on the options and usage of `elClass`, visit the [templates reference](https://duck.co/duckduckhack/templates_reference#directly-specifying-classes).

------

## `normalize` *function* [optional]

Specifying this optional function allows you to normalize each item in the `data` object before it is used by the template. You can use this function to rename properties, add new properties, or modify values.

This function is applied both for single results or multiple results. When dealing with multiple items returned in the `data` object, the normalize function iterates over each item. Each item is individually normalized and passed to its own instance of the `item` template.

#### Notes for Goodie Instant Answers

Because Goodies have no external sources and run on the server, a `normalize` function is not completely necessary to normalize data for templates. However, it is possible (and conceivable) to use a `normalize` function in a Goodie Instant Answer.

**Defining a `normalize` function in a Goodie, must be done in the frontend part of the code, as JavaScript.** For more information about Goodie JavaScript visit the [Goodie Display](https://duck.co/duckduckhack/goodie_displaying#setting-goodie-display-properties-in-the-frontend) section.

### Usage

The function set for `normalize` is expected to return an object with the properties to be rendered for each item. 

The object returned by the `normalize` function is *combined* with the original respective item from `data`.  

The `normalize` function will **extend the original `data` item** instead of replacing it. (This uses jQuery's `$.extend()` method, shallow copy.) Each normalized item will contain its original properties unless they were explicitly overwritten in the `normalize` function.

#### Use with Built-In Templates

Normalize can be particularly useful if you are using a [built-in template](https://duck.co/duckduckhack/templates_reference#templates) (for example, `basic_image_item`). 

Built-in templates expect that certain properties will be present (such as `title` and `image`). The `normalize` function allows you to provide those (or normalize their values if the property already existed in your `data`).

For example, if you have a `data` object that looks like this:

```javascript
// original data object from API
{
    heading: "My awesome title",
    image:   "http://website.com/image.png"
}
```

You will likely want to pass the `heading` property as the `title` for the **basic_image_item** template, so your `normalize` function would need to look like this:

```javascript
normalize: function(item){
    return {
        title: item.heading
    };
}
```

This would result in your `data` object looking like this once it gets passed along to the template:

```javascript
// normalized data object
{
    heading: "My awesome title",
    image:   "http://website.com/image.png",
    title:   "My awesome title"
}
```

Now, your object has all the required properties for the **basic_image_item** template and everything will be displayed as expected.

#### Important Note on Enabling Features

If you intend to use a [template feature](https://duck.co/duckduckhack/templates_reference) that is [disabled by default](https://duck.co/duckduckhack/templates_overview#a-note-on-default-template-options) or [disabled by a template group defaults](https://duck.co/duckduckhack/template_groups#template-groups-reference), that feature must be **enabled in the `options`** to display.

Even if the property exists in the `data` object, the template system will ignore it if the feature is disabled. 

In this example:

```javascript
normalize: function(item){
    return {
        // these won't work!
        rating: item.customerRating,
        brand: item.brandname
    };
},
templates: {
    group: 'products_simple'
}
```

The template **will *not* display** the `rating` or `brand` as they are **disabled** by default in the `products_simple` group default options. Only once they are explicitly enabled in an `options` object will they work:

```javascript
normalize: function(item){
    return {
        // now they'll show, because they're enabled below
        rating: item.customerRating,
        brand: item.brandname
    };
},
templates: {
    group: 'products_simple',
    options: {
        rating: true,
        brand: true
    }
}
```

### `exactMatch` *boolean* and `boost` *boolean*

Two special properties, `exactMatch` and `boost`, can also be set in the `normalize` function to add particular items to the list of exact matches or boosted items. 

When the tile view displays, the **exact match** items will come **first**, followed by the **boosted** items and then the rest of the items.

Example:

```javascript
normalize: function(item) {
    if (item.name === DDG.get_query()){
        item.exactMatch = true;
    } else if (item.developer.name === DDG.get_query()) {
        item.boost = true;
    }

    return { ... }
}
```

------

## `relevancy` *object* [optional]

When dealing with multiple items, the `relevancy` property can be used to ensure the relevancy of each individual item. It can also be used to de-duplicate the returned items if desired.

In most cases you will only need to specify relevancy properties for the `primary` relevancy block. However, if your Instant Answer is capable of dealing with different types of queries though, where different relevancy checks are necessary, you can supply additional relevancy blocks. 

For example, the Quixey Spice (app search) handles two distinct types of app searches: 

- **Categorical** searches, such as "social networking apps"
- **Named** searches such as "free angry birds apps" 

When dealing with **categorical** searches, the name of the app doesn't need to be checked against the query for relevancy. However, the app's category *does* need to be checked and so two separate relevancy blocks, `primary` and `category`, are used to define the different relevancy constraints.

Sample code from [quixey.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js#L129):

```javascript
relevancy: {
    ...
    category: [
        { required: 'icon_url' },
        { key: 'short_desc' },
        { key: 'name' },
        { key: 'custom.features.category', match: category_match_regexp, strict:false } // strict means this key has to contain a category phrase or we reject
    ],

    primary: [
        { required: 'icon_url' }, // would like to add  alt: 'platforms.0.icon_url'
        { key: 'name', strict: false },
    ]
}
```

#### Notes for Goodie Instant Answers

The `relevancy` property is unlikely to be used in a Goodie Instant Answer, although it is completely functional. Potential use in a Goodie might involve large data sets to search through.

If using `relevancy` in a Goodie, it must be specified in the frontend part of the code, as JavaScript. For more information about Goodie JavaScript visit the [Goodie Display](https://duck.co/duckduckhack/goodie_displaying#setting-goodie-display-properties-in-the-frontend) section.

### Relevancy Blocks

A relevancy block is comprised of an array of simple objects. For each object, the properties are used to indicate certain constraints. The concept of a relevancy block is best explained with an example:

<!-- /summary -->

```javascript
// First we provide the name for the relevancy block, "primary"
primary: [

    { required: 'icon_url' },
    // "required" means the item must have a defined property matching the
    // given name, in this case and "icon_url" must be defined for each Quixey
    // item
    //
    // Note: "required" only ensures the presence of a property. It does NOT
    // perform a relevancy check

    { key: 'name', strict: true },
    // "key" indicates a property which will be checked for relevancy. If
    // the given key is determined to be relevant, the item as a whole is
    // considered relevant and no other keys in the relevancy block are
    // checked for the current item
    //
    // The "strict" key allows you to turn on the "strict mode"
    // for DDG.isRelevant

    { key: 'short_desc' }
    // this is an extra "key" which serves as a fallback. This means if
    // either the 'name' or 'short_desc' or relevant the item is considered
    // relevant
],

// here we provide a secondary relevancy block with a chosen name of "category"
category: [
    { required: 'icon_url' },
    { key: 'name' },
    { key: 'short_desc' },
    { key: 'custom.features.category', match: category_regexp }
    // the "match" key allows you to specify a regular expression which the
    // given "key" must match
    //
    // Note: "match" only ensures the property matches the given regex. It
    // does NOT perform a relevancy check
],
```

**Note:** The relevancy checking is done using the `DDG.isRelevant()` function.

- ### `type` *string*

    The name of the relevancy block to use. If no value is provided, the default `primary` block will be used.

    For example, the Quixey spice determines the `type` based on the query. If the query matches against our category regex (i.e. the query contains a category word), we set `type` to "category", otherwise we use "primary".

- ### `skip_words` *array*

    A list of words to ***skip*** when comparing the specified text against the current query. Generally these words should include any trigger words for your Instant Answer. The skip words list is **not** dependent on the chosen relevancy block.

- ### `primary` *array* [required if using `relevancy`]

    The list of relevancy terms for this particular relevancy block

- ### `<additional_relevancy_block>` *array*

    An additional list of relevancy terms, using the same format as `primary`. This object (and other relevancy blocks) can be named arbitrarily.

- ### `dup` *string*

    This indicates which property should be used to check for de-duplication. The given string supports dot path formatting, e.g., "item.foo.bar"

------

## `sort_fields` *object* [optional]

In some cases, the order of the tiles is important (e.g., price, rating, popularity) and you can use the sorting properties to specify the default ordering of the tiles. You can also specify additional sorting fields that will allow users to re-order the tiles using a different sort method.

This object specifies sorting fields (e.g., name, price, rating, reviews) and their respective comparison functions, which will be passed along to JavaScript's `sort()` method.

Example:

```javascript
sort_fields: {
    name: function(a,b) {
        return a.name < b.name ? -1 : 1;
    },
    rating: function(a,b) {
        return a.rating < b.rating ? -1 : 1;
    }
}
```

#### Notes for Goodie Instant Answers

When setting `sort_fields` properties in a Goodie, you must specify them in the frontend part of the code, as javascript. For more information about Goodie javascript visit the [Goodie Display](https://duck.co/duckduckhack/goodie_displaying#setting-goodie-display-properties-in-the-frontend) section.

### `sort_default` *string or object*

A string specifying the default `sort_field` to be used for initial sorting of the tiles.

```javascript
sort_default: 'name';
```

If you have used **more than one** relevancy block, `sort_default` can be given an `object` specifying the default `sort_field` for each relevancy block.

For example, if we had two relevancy blocks named `primary` and `category` our `default_sort` could look like this:

```javascript
//because we have two relevancy blocks...
sort_default: {
    primary: 'name',
    category: 'rating'
}
```

------

## `view` *string* [optional]

Typically you don't need to specify a view for Instant Answers unless you're using special functionality like the playable Audio tiles for the SoundCloud IA, or the Maps used in our Places IA.

Available Views:

- Audio
- Detail (default view for IAs with a single item)
- Images
- Map
- Places
- Tiles (default view for IAs with multiple items)
- TilesWithTopics
- Videos

------

## `model` *string* [optional]

Some Instant Answers use data to display results which is not directly displayed in a template. For example, the latitude and longitude of a Place, or the dimensions of an Image. The Instant Answer framework comes with built-in models to manage these data. Some [views](#codeviewscode-emstringem-optional) require a model - such as Audio or Places.

**If you are specifying a template group, the `model` property is automatically set for you.**

Available models:

- Audio
- Image
- Place
- Product
- Video

More about using models and their properties can be found in their respective [template groups](https://duck.co/duckduckhack/template_groups#template-groups-reference).

------

## Events

If you need to fire off an event handler when a tile is clicked or when your Instant Answer's tab initially opens, you can handle these events with a callback function.

- ### `onItemSelected` *function*

	This event occurs each time a tile is selected with a click.

	Example:

	```javascript
	onItemSelect: function(item) {
	   player.play(item);
	}
	```

	Learn more about the [`item` argument](#the-codeitemcode-argument) below.

	**Note:** If a tile-view result returns a single result, this event will also fire when the tab is opened/clicked, so you don't need to use both `onItemSelected` and `onShow` to handle the case of a single-result tile view

- ### `onItemUnselect` *function*

	This event occurs each time a tile is unselected - i.e., the user clicks somewhere else on the page.
	
	```javascript
	onItemUnselect: function(item) {
		// Pause playing media, change appearance, etc.
	}
	```
	
	Learn more about the [`item` argument](#the-codeitemcode-argument) below.

	**Note:** If a tile-view result returns a single result, this event will also fire when the tab is closed, so you don't need to use both `onItemSelected` and `onShow` to handle the case of a single-result tile view

- ### `onShow` *function*

	This event occurs each time an Instant Answer tab is displayed. This event fires when the Instant Answer is initially shown. It also fires when a user clicks another AnswerBar tab, then clicks to show it again.
	
- ### `onItemShown` *function*

	Same behavior as `onShow`, but fired on a per-item basis. This is useful for separately requesting and updating information relevant to each tile - e.g. secondary API calls. For example, the [Amazon Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js) uses this event to render product ratings, and the [Movie Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js) sets each tile's image element using this event.
	
	```javascript
	onItemShown: function(item) {
		// Do something to the item, such as update latest info
	}
	```
	
	Learn more about the [`item` argument](#the-codeitemcode-argument) below.

- ### `onHide` *function*

	This event occurs when a Instant Answer tab is closed i.e. when another tab is selected.
	
### The `item` Argument

Events relevant to specific items pass an `item` to their handler functions. This is a reference to the item's data object, rendered to the template. Modifying the properties will not update the DOM.

An added `item.$html` property references the respective item DOM element as a jQuery object.

### Notes for Goodie Instant Answers

When creating a Goodie, you must declare event handlers in the frontend part of the code, as JavaScript. For more information about Goodie JavaScript visit the [Goodie Display](https://duck.co/duckduckhack/goodie_displaying#setting-goodie-display-properties-in-the-frontend) section.




