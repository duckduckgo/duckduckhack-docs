# Templates and Variants Reference

The basic building blocks of displaying Instant Answers are templates and variants. Below is a detailed reference of the properties and usage of each.

To understand the context of templates and how they fit into your Instant Answer, start with the [Templates Overview](https://duck.co/duckduckhack/templates_overview).

The reference is divided into two parts:

- [Templates](#templates) - the built-in handlebars html templates
- [Variants](#variants) - preset styles available to modify their appearance

## Important Note

Before using these templates please familiarize yourself with the Instant Answer display options (for example, [Spice](https://duck.co/duckduckhack/spice_displaying) or [Goodie](https://duck.co/duckduckhack/goodie_displaying)) document to understand the proper usage of both the `templates` block and the `options` block. Understanding these is crucial to implementing templates properly and effectively.

You will be specifying these templates indirectly - as part of a Template Group. The [Templates Groups Overview](https://duck.co/duckduckhack/template_groups) will help you think about the big picture of which template groups best fit your Instant Answer.

## Templates

The list of built-in templates includes:

- [`text_item`](#codetextitemcode-template)
- [`text_detail`](#codetextdetailcode-template)
- [`basic_image_item`](#codebasicimageitemcode-template)
- [`products_item`](#codeproductsitemcode-template)
- [`products_detail`](#codeproductsdetailcode-template)
- [`products_item_detail`](#codeproductsitemdetailcode-template)
- [`basic_icon_detail`](#codebasicicondetailcode-template)
- [`basic_info_detail`](#codebasicinfodetailcode-template)
- [`places_item`](#codeplacesitemcode-template)
- [`places_detail`](#codeplacesdetailcode-template)
- [`basic_flipping_item`](#codebaseflippingitemcode-template)
- [`base_flipping_item`](#codebaseflippingitemcode-template)
- [`list_detail`](#codelistdetailcode-template)
- [`record`](#coderecordcode-template)
- [`media_item`](#codemediaitemcode-template)
- [`media_item_detail`](#codemediaitemdetailcode-template)
- [`images_item`](#codeimagesitemcode-template)
- [`images_detail`](#codeimagesdetailcode-template)
- [`videos_item`](#codevideositemcode-template)
- [`videos_detail`](#codevideosdetailcode-template)
- [`base_item`](#codebaseitemcode-template)
- [`base_detail`](#codebasedetailcode-template)

------

## `text_item` Template

Template for displaying textual information tiles, each with an optional icon.

### Template Diagram

![text_item template ](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_item.png&f=1)

```
+------------------+
icon
title, altSubtitle
subtitle
description
footer
            dateBadge
+------------------+
```

### Available Features

- `icon` [optional] *string url*

	URL path to icon image

- `url` [optional] *string url*
- `title` [required] *string url*
- `altSubtitle` [optional] *string* or *string array*
- `subtitle` [optional] *string* or *string array*
- `description` [required] *string*
- `footer` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `dateBadge` [optional] *object*

	An object with either a `text` *string* property **or** a `month` and `day` *string* properties.
	For an example of this property in action, search for ["concert in toronto"](https://duckduckgo.com/?q=concerts+in+toronto&ia=concerts) and see the [SeatGeek Events by City](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/seat_geek/events_by_city/seat_geek_events_by_city.js) Spice.


### Example Usage

- [GitHub](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js)
- [RubyGems](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/ruby_gems/ruby_gems.js)
- [RedditSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)
- [AlternativeTo](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

### Template Groups

- [Text](https://duck.co/duckduckhack/template_groups#text-template-group)

------

## `text_detail` Template

A template for displaying textual information detail, with no image or icon.

### Template Diagram

![text_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_detail.png&f=1)

```
+-------------------------------------+

title_content or title
subtitle_content or subtitle
content

+-------------------------------------+
```

### Available Features

- `title_content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `title` [optional] *string*

	Available only if `title_content` is not specified

- `subtitle_content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `subtitle` [optional] *string* or *string array*

	Available only if `subtitle_content` is not specified

- `content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

### Example Usage

- [Rhymes](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js)
- [Thesaurus](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js)

### Template Groups

- [Text](https://duck.co/duckduckhack/template_groups#text-template-group)

------

## `basic_image_item` Template

A tile template where images are the main feature, accompanied by text.

### Template Diagram

![basic_image_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_image_item.png&f=1)

```
+------------------+
image
title
description
rating
ratingText
+------------------+
```

### Available Features

- `url` [optional] *string url*
- `image` [required] *string url*

	URL path to image

- `title` [required] *string*
- `description` [optional] *string*

	Limited to 56 characters, truncated to whole words with an ellipsis

- `rating` [optional] *float*

	A positive float with one decimal point, up to 5.0

- `ratingText` [optional] *string*

### Example Usage

- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)

### Template Groups

- [Info](https://duck.co/duckduckhack/template_groups#info-template-group)
- [Media](https://duck.co/duckduckhack/template_groups#media-template-group)

------

## `products_item` Template

A tile item template where images are emphasized, with features suited for items that can be purchased.

### Template Diagram

![products_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item.png&f=1)

```
+------------------+
img
title
price
brand
rating
+------------------+
```

### Available Features

- `url` [optional] *string url*
- `img` [required] *string url*
- `title` [required] *string*
- `price` [optional] *string*
- `brand` [optional] *string*
- `rating` [optional] *float*

	A positive float with one decimal point, up to 5.0

- `reviewCount` [optional] *integer*

	The count of reviews
	Automatically formatted to include comma thousands separators

- `url_review` [optional] *string*

	URL path to reviews

### Example Usage

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

### Template Groups

- [Products](https://duck.co/duckduckhack/template_groups#products-template-group)

------

## `products_detail` Template

A detail template where image is emphasized, suited to feature for an item that can be purchased.

### Template Diagram

![products_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_detail.png&f=1)

```
+------------------------------------+
                heading
                rating, reviewCount
                price, brand
    img         subtitle_content                
                abstract
                buy
+------------------------------------+
```

### Available Features

- `img` [optional] *string url*

	URL path to image

- `url` [required] *string url*
- `heading`[required] *string*
- `rating` [optional] *float*

	A positive float with one decimal point, up to 5.0

- `reviewCount` [optional] *integer*

	The count of reviews
	Automatically formatted to include comma thousands separators

- `price` [optional] *string*
- `brand` [optional] *string*
- `subtitle_content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `abstract` [required] *string*

	Limited to 400 characters, truncated to whole words with an ellipsis

- `buy` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

	Can be used to provide a call-to-action, such as a button.

### Example Usage

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

### Template Groups

- [Products](https://duck.co/duckduckhack/template_groups#products-template-group)
- [Media](https://duck.co/duckduckhack/template_groups#media-template-group)
- [Icon](https://duck.co/duckduckhack/template_groups#icon-template-group)

------

## `products_item_detail` Template

A template for drilling-down into a particular item on the same page. Emphasizes an image, and suited to feature for an item that can be purchased. This template features an optional call-to-action.

### Template Diagram

![products_item_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item_detail.png&f=1)

```
+------------------------------------+
                heading
                price, brand
    img_m       subtitle_content
                rating, reviewCount
                abstract
                buy
+------------------------------------+
```

### Available Features

- `img_m` [optional] *string url*

	URL path to image

- `heading` [required] *string*
- `url` [required] *string url*
- `price` [optional] *string*
- `brand` [optional] *string*
- `subtitle_content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `rating` [optional] *float*

	A positive float with one decimal point, up to 5.0

- `reviewCount` [optional] *integer*

	The count of reviews
	Automatically formatted to include comma thousands separators

- `url_review` [optional] *string url* 
	
	Link to source reviews page
	
- `abstract` [required] *string*
- `buy` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

	Can be used to provide a call-to-action, such as a button.

### Example Usage

- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)

### Template Groups

- [Products](https://duck.co/duckduckhack/template_groups#products-template-group)
- [Media](https://duck.co/duckduckhack/template_groups#media-template-group)
- [Icon](https://duck.co/duckduckhack/template_groups#icon-template-group)

------

## `basic_icon_detail` Template

A template for displaying textual information detail, with a small image, icon, or character badge.

### Template Diagram

```
+------------------------------------------------+
image and/or badge      title
                        subtitle
                        altSubtitle

                        content *or* description                        

+------------------------------------------------+
```

### Available Features

- `image` [optional] *string url*

	URL path to image
	
- `badge` [optional] *string*
- `title` [optional] *string*
- `subtitle` [optional] *string* or *string array*
- `altSubtitle` [optional] *string* or *string array*
- `content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `description` [conditional on `content`] *string*

	Available and required if `content` not specified

### Example Usage

*None - yet*

### Template Groups

- [Icon](#icon-template-group)

------

## `basic_info_detail` Template

A detail template which shows in-depth information. This template includes an auxiliary area for listing properties.

### Template Diagram

![basic_info_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail.png&f=1)

The same template, with the `aux` feature:

![basic_info_detail_w_aux template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail_w_aux.png&f=1)

```
+-------------------------------------------------------+
                title
    image       subtitle                        
                content or description          infoboxData
+-------------------------------------------------------+
```

### Available Features

- `url` [required] *string url*
- `image` [optional] *string url*

	URL path to image

- `title` [optional] *string*
- `subtitle` [optional] *string* or *string array*

	Available only if `title` specified

- `content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `description` [conditional on `content`] *string*

	Available and required if `content` not specified

- `infoboxData` [optional] *array*	

	An array of objects used to render an [InfoBox](#the-infobox)

### Example Usage

- [Bitcoin](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js)
- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js)

### Template Groups

- [Info](https://duck.co/duckduckhack/template_groups#info-template-group)

### The Infobox

In the `basic_info_detail` template, the **InfoBox** floats on the right side of the AnswerBar. It presents detailed information in a table of key-value pairs:

![infobox](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Finfobox.png&f=1)

To display the InfoBox in the `basic_info_detail` template, an item must have an `infoboxData` property specified. This is an array of objects, each with the following properties:

- `label` [required] *string*
- `url` [optional] *string url*

	Used to turn `label` element into a link

- `value` [optional] *string or array*

	Use array to display [nested properties](#infobox-nested-properties))

The first object in the array can also be used solely to specify a heading for the InfoBox. This object would contain only one property:

- `heading` [optional] *string*

	Specified in its own separate object, first in the array

For example, when ["mtg nullify"](https://duckduckgo.com/?q=mtg+nullify&ia=magicthegathering) is searched, [mtg.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/mtg/mtg.js) dynamically generates the following array for `infoboxData`:

```javascript
[
    {
        heading: "Card Details"
    },
    {
        label: "Mana Cost",
        value: "UU"
    },
    {
        label: "Converted Mana Cost",
        value: 2
    },
    ...
]
```

This data shows up in the AnswerBar, to the right:

![mtg infobox](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fmtg_infobox.png&f=1)

It is also possible to specify labels alone, with or without urls. This is the `infoboxData` value generated by [urban_dictionary.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js) when searching for ["urban dictionary cool"](https://duckduckgo.com/?q=urban+dictionary+cool&ia=dictionary):

```javascript
[
    {
        heading: "Related Terms:"
    },
    {
        label: "Awesome",
        url: "https://duckduckgo.com/?q=ud+awesome&ia=dictionary"
    },
    {
        label: "Amazing",
        url: "https://duckduckgo.com/?q=ud+amazing&ia=dictionary"
    },
    ...
]
```

This appears as:

![ud infobox](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fud_infobox.png&f=1)

#### InfoBox Nested Properties

The `value` property of `infoboxData` objects can *also* be passed an array of objects. These objects have the following properties:

- `label` [required] *string*
- `value` [required] *string*

For example, the resulting array passed to `infoboxData` could be structured this way:

```javascript
[
    {
        heading: "About Me"
    },
    {
        label: "My Favorites",
        value: [
            {
                label: "Color",
                value: "Red"
            },
            {
                label: "Animal",
                value: "Duck"
            },
            ...
        ]
    },
    ...
]
```

------

## `places_item` Template

An item template which displays multiple location results on one map.

Clicking a places item both indicates its location on a map, as well as 'flips' the item to display more detailed information. The `places_item` template can conceptually be divided into its 'front' and 'back'.

### Template Diagram

#### 'Front'

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_front.png&f=1)
```
+--------------------+


        image


+--------------------+
name
ratingImageURL *or* rating
reviews
+--------------------+
```

#### 'Back'

This view is displayed when the 'front' is clicked, together with the map (below).

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_back.png&f=1)

```
+--------------------+

name (url)

price

address_lines *or* address

phone

+--------------------+
```

### Available Features

#### 'Front' of each item:
- `image` [optional] *string url*

	Path to image

- `name` [required] *string*
- `title` [optional] *string*

	Available only if `image` specified

- `ratingImageURL` [optional] *string url*
- `rating` [optional] *float*

	A positive float with one decimal point, up to 5.0
	Available only if `ratingImageURL` is not specified

- `reviews` [optional] *integer*

	The count of reviews
	Automatically formatted to include comma thousands separators

#### 'Back' of each item: (displayed upon click)
- `name` [required] *string*
- `url` [required] *string url*
- `price` [optional] *integer*

	Integer between 1 and 4; converted to a dollar-sign rating (such as '$' or '$$$$')

- `address_lines` [optional] *array*

	An array of strings, one for each line

- `address` [optional] *string*

	Available only if `address_lines` not specified
	Limited to 65 characters, truncated to whole words with an ellipsis

- `phone` [optional] *string*

#### Map View

This view is displayed when the 'front' is clicked, together with the 'back' (above).

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_map.png&f=1)

### Example Usage

- Local results (built-in to DDG): search for [cafes near Ann Arbor](https://duckduckgo.com/?q=cafes+near+ann+arbor).

### Template Groups

- [Places](https://duck.co/duckduckhack/template_groups#places-template-group)

------

## `basic_flipping_item` Template

This template is used to replace `places_item` on the front and back of the item tile. This template maintains the unique 'flip' behavior of `places_item`.

### Template Diagram

#### 'Front'

These properties are passed to the template inside a `data_front` object (e.g. `data_front.title`).

```
+--------------------+


    icon
    title, altsubtitle
    subtitle
    footer_content


+--------------------+
```

#### 'Back'

This view is displayed when the 'front' is clicked, together with the map (below). These properties are passed to the template inside a `data_back` object (e.g. `data_back.title`).

```
+--------------------+


    icon
    title, altsubtitle
    subtitle
    footer_content


+--------------------+
```

### Available Features

#### 'Front' of each item:

These properties are passed to the template inside a `data_front` object (e.g. `data_front.title`).

- `icon` [optional]
- `title` [optional]
- `altsubtitle` [optional]
- `subtitle` [optional]
- `footer_content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

#### 'Back' of each item: (displayed upon click)

These properties are passed to the template inside a `data_back` object (e.g. `data_back.title`).

- `icon` [optional]
- `title` [optional]
- `altsubtitle` [optional]
- `subtitle` [optional]
- `footer_content` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

#### Map View

As with `places_item`, map view is displayed when the 'front' is clicked, as it displays the 'back'.

### Example Usage

- [GetEvents](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/get_events/get_events.js): search for [events in new york](https://duckduckgo.com/?q=events+in+new+york&ia=list)

	In [`get_events.js`](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/get_events/get_events.js), the `places` template group is specified, and overrides the `item` template. 

    ```javascript
    templates: {
        group: 'places',
        item: 'basic_flipping_item'
    }
    ```

	The `normalize` function returns the data for each side, contained within the `data_front` and `data_back` properties:
	
	```javascript
	return {
		data_front: {
		    showPin: true,
		    title: item.name,
		    venue: item.venue,
		    image: item.image_large_url,
		    altSubtitle: formatSubtitleString(item),

		    footer_content: Spice.get_events.foot_front,

		    footLines: '4',
		    titleClass: 'tile__title--3 tx--16 tx--bold mg--none',
		    altSubClass: 'tx--13 tx-clr--grey'
		},
		data_back: {
		    title: item.name,
		    url: buildUrl(item.id),
		    description: item.description ? DDG.strip_html(item.description) : 'No description available.',

		    footer_content: Spice.get_events.foot_back,

		    titleClass: 'tile__title--1 tx--16 tx--bold'
		},
		city: item.venue.city,
		place: item.venue.name,
		lat: item.venue.lat,
		lon: item.venue.lng
	};
	```

### Template Groups

- Used with [Places](https://duck.co/duckduckhack/template_groups#places-template-group)

------

## `base_flipping_item` Template

This template is used to replace `places_item` with custom sub-templates for the front and back of the item tile. This template maintains the unique 'flip' behavior of `places_item`, while allowing full customization of both sides.

**Use as a last resort** due to the large amount of upfront work and ongoing maintenance involved. Please contact us at [open@duckduckgo.com](mailto:open@duckduckgo.com) *before* using this template.

### Template Diagram

#### 'Front'

```
+--------------------+



    front_content



+--------------------+
```

#### 'Back'

This view is displayed when the 'front' is clicked, together with the map (below).

```
+--------------------+



    back_content



+--------------------+
```

### Available Features

#### 'Front' of each item:

- `front_content` [required] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

#### 'Back' of each item: (displayed upon click)

- `back_content` [required] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

#### Map View

As with `places_item`, map view is displayed when the 'front' is clicked, as it displays the 'back'.

### Example Usage

- [Parking Panda](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js): search for [parking in new york](https://duckduckgo.com/?q=parking+in+new+york).
	
	In `parking.js`, the `places` template group is specified, and override the `item` template. Then the two [custom sub-templates](https://duck.co/duckduckhack/subtemplates) are specified under `options`.

    ```javascript
    templates: {
        group: 'places',
        item: 'base_flipping_item',
        options: {
            front_content: Spice.parking.item_front,
            back_content: Spice.parking.item_back
        }
    }
    ```

### Template Groups

- Used with [Places](https://duck.co/duckduckhack/template_groups#places-template-group)

------

## `places_detail` Template

A detail template for displaying information about a single location on a map backdrop.

### Template Diagram

![DuckDuckGo search for "espresso italiano maui"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_detail.png&f=1)

```
+--------------------------------+------------+
|   name (url)                   |            |
|                                | image (url)|
|   ratingImageURL *or* rating   |            |
|   reviews                      |            |
|   price                        |            |
|   address_lines *or* address   |            |
|   phone                        |            |
|                                |            |
|                                |            |
+--------------------------------+            |
|                                |            |
|    hours                       |            |
|                                |            |
+--------------------------------+------------+
```

### Available Features

- `url` [required] *string url*
- `name` [required] *string*
- `image` [optional] *string url*

	URL path to image

- `title` [optional]

	Used at `alt` attribute of the `image` element

- `hours` [optional] *array*

	Array of objects, each containing `day` and `hours` properties

- `ratingImageURL` [optional]
- `rating` [optional] *float*

	A positive float with one decimal point, up to 5.0
	Available only if `ratingImageURL` not specified

- `reviews` [optional] *integer*

	The count of reviews
	Automatically formatted to include comma thousands separators

- `price` [optional] *integer*

	Integer between 1 and 4; converted to a dollar-sign rating (such as '$' or '$$$$')- `address_lines` [optional] *array*

	An array of strings, one for each line

- `address` [optional] *string*

	Available only if `address_lines` not specified

- `phone` [optional] *string*

### Example Usage

- Local results (built-in to DDG): search for [a particular business](https://duckduckgo.com/?q=espresso+italiano+maui).

### Template Groups

- [Places](https://duck.co/duckduckhack/template_groups#places-template-group)

------

## `list_detail` Template

A detail template for displaying of a title and subtitle above a bulleted list, or a table of key-value pairs.

### Template Diagram

![DuckDuckGo search for "whois mozilla.org"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhois_results.png&f=1)

```
+-------------------+

title
subtitle

content, record_data
*or*
list_content, list

+-------------------+
```

### Available Features

- `title` [optional] *string*
- `subtitle` [optional] *string* or *string array*

#### If Displaying Table of Key-Value Pairs:

- `content` [required] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

	Recommended to set this value to `'record'` (a string) to specify the built-in [`record`](#coderecordcode-template) sub-template. Learn more about [built-in sub-templates](https://duck.co/duckduckhack/subtemplates).

- `record_data` [required] *object*

	Includes the key-value pairs to display

#### If Displaying Bulleted List of Values:

- `list_content` [required] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

	Supply a custom handlebars sub-template. The sub-template will be rendered, enclosed by a `li` element. Learn more about [sub-templates](https://duck.co/duckduckhack/subtemplates).

- `list` *array*

	Array of objects, each contains the properties used by `list_content` sub-template

### Usage

To display a bulleted list, pass a sub-template to the `list_content` property. To display a table of key-value pairs, pass the [`record`](#coderecordcode-template) template to the `content` property.

When displaying a bulleted list, the simplest case would be to pass `list` an array of objects like `{value: 'foo'}` and specify `list_content` to be a sub-template which only reads `{{value}}`.

### Example Usage

- [Whois](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js) (search for ['whois mozilla.org'](https://duckduckgo.com/?q=whois+mozilla.org))

### Template Groups

- [List](https://duck.co/duckduckhack/template_groups#list-template-group)

------

## `record` Template

A special template that is ideal for key-value data. It generates a `<table>` where each row contains a key and value. Often used as a sub-template, for example by the [`list_detail`](#codelist_detailcode-template) template.

### Template Diagram

![record template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Frecord.png&f=1)

```
+---------------------------------------------+
*key*           *value*
*key*           *value*     (of record_data)
*key*           *value*
...
+---------------------------------------------+
```

### Available Features

- `record_data` [required] *object*

	Contains key-value pairs to display in table format
	Values limited to 350 characters, truncated to whole words with an ellipsis

### Usage

This template requires that a `record_data` property, which should contain the key-value data to be displayed. All the properties of the `record_data` object will be used as the keys for the table.

However, if you want to specify exactly which properties of the `record_data` object should be displayed, you can define an optional `record_keys` property. This is an array of strings, specifying which key-value pairs of `record_data` will be included.

An optional property called `rowHighlight` can be added to `options` to turn on alternating row highlighting.

### Sample Code

```javascript
data: {
    record_data: {
        name: 'Bob',
        phone: '123-456-7890',
        email: 'bob@bobstheman.com',
        address: '123 First Street'
    }
},
normalize: function(item){
    return {
        record_keys: ["name", "phone", "email"]
    }
},
templates: {
    group: 'base',
    options: {
        content: 'record',
        /* optional - highlight alternate rows */
        rowHighlight: true
    }
}
```

### Example Usage

- [UrbanDictionary](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js)
- [MetaCpan](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)
- [CodeSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/code_search/code_search.js)
- [Whois](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js)

### Template Groups

- Can be used as a sub-template by the [List](https://duck.co/duckduckhack/template_groups#list-template-group) template group (under the [`list_detail`](#codelistdetailcode-template) template)

------

## `media_item` Template

### Template Diagram

```
+----------------------+

        image


title
altSubtitle
subtitle
description
footer
dateBadge   

+----------------------+
```

### Available Features

- `title` [required] *string*
- `altSubtitle` [optional] *string* or *string array*
- `subtitle` [optional] *string* or *string array*
- `description` [optional] *string*
- `footer` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)
- `dateBadge` [optional] *object*

	An object with either a `text` *string* property **or** a `month` *string* and `day` *string* properties. 
	For an example of a `dateBadge` in action, search for ["concert in toronto"](https://duckduckgo.com/?q=concerts+in+toronto&ia=concerts) and see the [SeatGeek Events by City](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/seat_geek/events_by_city/seat_geek_events_by_city.js) Spice. (The example uses the `text_item` template, but the dateBadge is the same.)

### Example Usage

- [Dogo News](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dogo_news/dogo_news.js)

### Template Groups

- [Media](https://duck.co/duckduckhack/template_groups#media-template-group)

------

## `media_item_detail` Template

### Template Diagram

```
+------------------------------------------------------------------+
						title, altSubtitle
	image				subtitle
						description
						callout
+------------------------------------------------------------------+
```

### Available Features

- `image` [optional] *string url*
- `title` [required] *string*
- `altSubtitle` [optional] *string* or *string array*
- `description` [optional] *string*
- `callout` [optional] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

	Can be used to provide a call-to-action, such as a button.

### Example Usage

- [Dogo News](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dogo_news/dogo_news.js)

### Template Groups

- [Media](https://duck.co/duckduckhack/template_groups#media-template-group)

------

## `images_item` Template

### Template Diagram

#### Regular State

```
+-------------------+

    thumbnail

+-------------------+
```

#### Hover State

```
+-------------------+

   width × height

+-------------------+
```


### Available Features

- `thumbnail` [required] *string url*
- `tileWidth` [required] *integer*

	The pixel width of the **thumbnail** image - may vary among tiles
	
- `title` [optional] *string*

	The `alt` html attribute of the image element
	
- `width` [required] *integer*

	The pixel width of the **original** image.

- `height` [required] *integer*

	The pixel height of the **original** image.

### Example Usage

- Search for ["duck images"](https://duckduckgo.com/?q=duck+images&ia=images) (built-in images Instant Answer)

### Template Groups

- [Images](https://duck.co/duckduckhack/template_groups#images-template-group)

------

## `images_detail` Template

### Template Diagram

```
+------------------------------------------------------------------+


    thumbnail                   title
    or                          url
    highResImage                width × height
                                image

+------------------------------------------------------------------+
```

### Available Features

- `thumbnail` [required] *string url*
- `highResImage` [optional] *string url*
- `title` [required] *string*
- `url` [required] *string url*
	
	Path to image source page (the page on which the image was originally embedded)
	
- `width` [required] *integer*

	The pixel width of the **original** image.

- `height` [required] *integer*

	The pixel height of the **original** image.

- `image` [required] *string url*

	Path to image source file (the original image file path)

### Example Usage

- Search for ["duck images"](https://duckduckgo.com/?q=duck+images&ia=images) and click on any item (built-in images Instant Answer)

### Template Groups

- [Images](https://duck.co/duckduckhack/template_groups#images-template-group)

------

## `videos_item` Template

### Template Diagram

```
+----------------------+

    images.medium

    duration


    title
    viewCount

+----------------------+
```

### Available Features

- `images` [required] *object*

	Object with paths to various image sizes. This template requires a `medium` property.
	
- `duration` [required] *string url*

	Duration of the video, in HH:MM:SS format (e.g. '5:32' or '2:01:59')
	
- `title` [required] *string* 
- `viewCount` [required] *string* 

	Number of video views, preferably with commas as the thousands separator (value not formatted automatically)

### Example Usage

- Search for ["gopro videos"](https://duckduckgo.com/?q=gopro+videos&ia=videos&iai=vutn7IUCKck) (built-in videos search)

### Template Groups

- [Videos](https://duck.co/duckduckhack/template_groups#videos-template-group)

------

## `videos_detail` Template

### Template Diagram

```
+------------------------------------------------------------------+


    [video content]             title
                                username
                                viewCount
                                published

+------------------------------------------------------------------+
```

### Available Features

- `title` [required] *string*
- `url` [required] *string url*
- `username` [required] *string*
- `viewCount` [required] *string*
- `published` [required] *string*

	A date string in any format recognized by the JavaScript [`Date.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse) method

### Example Usage

- ["gopro videos"](https://duckduckgo.com/?q=gopro+videos&ia=videos&iai=vutn7IUCKck) and click on any item (built-in videos Instant Answer)

### Template Groups

- [Videos](https://duck.co/duckduckhack/template_groups#videos-template-group)

------

## `base_item` Template

An item template for containing fully customized markup.

**Use as a last resort** due to the large amount of upfront work and ongoing maintenance involved. Please contact us at [open@duckduckgo.com](mailto:open@duckduckgo.com) *before* using this template.

### Template Diagram

![base_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item.png&f=1)

```
+---------------------------------+


        content (template)


+---------------------------------+
```

### Available Features

- `url` [required] *string*
- `content` [required] [*sub-template*](https://duck.co/duckduckhack/subtemplates)

### Example Usage

- [GithubJobs](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github_jobs/github_jobs.js)
- [Airlines](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

### Complex Example

Here is an example of a more complex `content` sub-template passed to the `base_item` template.

![base_item template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item_complex.png&f=1)

### Template Groups

- [Base](https://duck.co/duckduckhack/template_groups#base-template-group)

------

## `base_detail` Template

A detail template for containing fully customized markup.

**Use as a last resort** due to the large amount of upfront work and ongoing maintenance involved. Please contact us at [open@duckduckgo.com](mailto:open@duckduckgo.com) *before* using this template.

### Template Diagram

![base_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail.png&f=1)

```
+---------------------------------+


        content (template)


+---------------------------------+
```

### Available Features

- `content` *string* or [*sub-template*](https://duck.co/duckduckhack/subtemplates)

### Example Usage

- [FlashVersion](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js)
- [NPM](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/npm/npm.js)
- [XKCD](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/xkcd/xkcd.js)

### Complex Example

![base_detail template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail_complex.png&f=1)

### Template Groups

- [Base](https://duck.co/duckduckhack/template_groups#base-template-group)

------

# Variants

If you'd like to modify a template to fit your needs, the Instant Answer framework offers preset options called Variants. Variants are passed as the `variants` property of `templates`, in your Instant Answer display options.

Variants correspond to pre-determined css classes (or combinations of classes) from the [DDG style guide](https://duckduckgo.com/styleguide) that work particularly well in each context.

*We strongly recommend using variants since they make it easy to quickly customize the appearance in a standardized way. However, if variants do not meet your needs, you may consider [directly specifying classes](#directly-specifying-classes).*

## `tile` Variants

If the default tile dimensions are not perfect for your Instant Answer result, you can use tile variants to modify the containers of your `item` template.

![tile variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftile_variant.png&f=1)

### Applicable Templates

- `base_item` template
- `basic_image_item` template
- `products_item` template

### Options

- `narrow` - narrower tile width, normal height (["alarm clock apps"](https://duckduckgo.com/?q=alarm+clock+apps), ["pa representatives"](https://duckduckgo.com/?q=pa+representatives))
- `wide` - increased width, normal height
- `xwide` - super wide, normal height (["flight aa102"](https://duckduckgo.com/?q=flight+aa102))
- `video` - shorter height, increased width
- `poster` - tall and thin, like a movie poster (["the dark knight movie"](https://duckduckgo.com/?q=the+dark+knight+movie), ["currently in theaters"](https://duckduckgo.com/?q=currently+in+theaters))

### `tile` Preset Options

The following four values for `tile` variant act as presets for [`tileTitle`](#tiletitle-variants) and [`tileSnippet`](#tilesnippet-variants) variant. These are combinations that our design team has found to work particularly well together.

- `basic1` - equivalent to setting `tileTitle: '2line'` and `tileSnippet: 'small'` (["rubygems cucumber"](https://duckduckgo.com/?q=rubygems+cucumber))
- `basic2` - equivalent to setting `tileTitle: '3line-small'` and `tileSnippet: 'large'`
- `basic3` - equivalent to setting `tileTitle: '3line-large'` and `tileSnippet: 'small'`
- `basic4` - equivalent to setting `tileTitle: '1line-large'` and `tileSnippet: 'large'` (["github zeroclickinfo"](https://duckduckgo.com/?q=github+zeroclickinfo))

### Usage

```javascript
templates: {
    ...
    variants: {
        tile: 'poster'
    }
 }
```

------

## `detail` Variants

This variant allows you to modify the `detail` template of your Instant Answer. Currently there is only one detail variant outside the default styling.

### Applicable Templates

- All tile containers (which wrap `item` templates)

### Options

- `light` - gives the detail area a lighter (white) background, ideally when displaying images with white backgrounds (["electronics coupons"](https://duckduckgo.com/?q=electronics+coupons))

#### Usage

```javascript
templates: {
    ...
    variants: {
        detail: 'light'
    }
 }
```

------

## `tileTitle` Variants

This variant changes the size of the title element, if it exists in the chosen template.

![tileTitle variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftiletitle_variant.png&f=1)

### Applicable Templates

- `text_item` template

### Options

- `1line`
- `1line-large`
- `2line` - (["perl jobs in san francisco"](https://duckduckgo.com/?q=perl+jobs+in+san+francisco&ia=jobs))
- `3line`
- `3line-small` - (["reddit baking"](https://duckduckgo.com/?q=reddit+baking&ia=social))
- `3line-large`

Another way to set a `tileTitle` variant is to use [`tile` preset options](#tile-preset-options). These are combinations of `tileTitle` and `tileSnippet` values that our design team has found to work particularly well together.

### Usage

```javascript
templates: {
    ...
    variants: {
        tileTitle: '1line'
    }
 }
```

------

## `iconTitle` Variants

This variant changes the size of the title element, specifically for the `basic_icon_detail` template.

### Applicable Templates

- `basic_icon_detail` template

### Options

- `large`

### Usage

```javascript
templates: {
    ...
    variants: {
        iconTitle: 'large'
    }
 }
```

------

## `tileSubtitle` Variants

This variant changes the amount of lines available in the subtitle element, for the `text_item` template.

### Applicable Templates

- `text_item` template
- `basic_icon_detail` template

### Options

- `2line`

### Usage

```javascript
templates: {
    ...
    variants: {
        tileSubtitle: '2line'
    }
 }
```

------

## `tileSnippet` Variants

This variant changes the amount of space used for the description or content sub-template, if it exists in the chosen template.

![tileSnippet diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftilesnippet_variant.png&f=1)

### Applicable Templates

- `text_item` template

### Options

- `small`
- `large` (["global mobile data usage"](https://duckduckgo.com/?q=global+mobile+data+usage&ia=answer), ["rubygems cucumber"](https://duckduckgo.com/?q=rubygems+cucumber&ia=software))

Another way to set a `tileSnippet` variant is to use [`tile` preset options](#tile-preset-options). These are combinations of `tileTitle` and `tileSnippet` values that our design team has found to work particularly well together.

### Usage

```javascript
templates: {
    ...
    variants: {
        tileSnippet: 'small'
    }
 }
```

------

## `tileFooter` Variants

This variant changes the amount of space allowed for the footer sub-template, if it exists in the chosen template.

![tileFooter variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftilefooter_variant.png&f=1)

### Applicable Templates

- `text_item` template
- `media_item` template

### Options

- `2line` (["reddit baking"](https://duckduckgo.com/?q=reddit+baking&ia=social))
- `3line` (["people in space"](https://duckduckgo.com/?q=people+in+space&ia=answer))
- `4line` (["live shows in london"](https://duckduckgo.com/?q=live+shows+in+london&ia=concerts))

### Usage

```javascript
templates: {
    ...
    variants: {
        tileFooter: '2line'
    }
 }
```

------

## `tileRating` Variants

This variant sets the css float direction of the star rating element, if it exists in the template. As you can see in the examples, it only affects the float behavior of the stars themselves - not any accompanying elements.

![tileRating variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftilerating_variant.png&f=1)

### Applicable Templates

- `basic_image_item`

### Options

- `starsLeft` (["amazon ninja costume"](https://duckduckgo.com/?q=amazon+ninja+costume&ia=products))
- `starsRight` (["recipes quinoa"](https://duckduckgo.com/?q=recipes+quinoa&ia=recipes))

### Usage

```javascript
templates: {
    ...
    variants: {
        tileRating: 'starsLeft'
    }
 }
```

------

## `iconImage` Variants

For templates containing an icon element, this variant sets its size.

![iconImage variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ficonimage_variant.png&f=1)

### Applicable Templates

- `basic_icon_detail` template

### Options

- `small` (["alternative to emacs"](https://duckduckgo.com/?q=alternative+to+emacs&ia=software))
- `medium`
- `large`

### Usage

```javascript
templates: {
    ...
    variants: {
        iconImage: 'small'
    }
 }
```

------

## `iconBadge` Variants

For templates containing an icon badge (an inline colored container with text), this variant sets its size.

![iconBadge variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ficonbadge_variant.png&f=1)

### Applicable Templates

- `basic_icon_detail` template

### Options

- `small`
- `medium` (["UV Index"](https://duckduckgo.com/?q=UV+index), US searches only)
- `large`

### Usage

```javascript
templates: {
    ...
    variants: {
        iconBadge: 'small'
    }
 }
```

------

# Directly Specifying Classes

When [variants](#variants) don't suffice, you can directly choose classes based on the [DDG style guide](https://duckduckgo.com/styleguide) through the `elClass` property of `templates`, in your Instant Answer display options. This feature is mainly used for specifying text size and color.

Classes can be directly specified to the same elements as [Variants](#variants); the locations are identical. If you are specifying both `variants` and `elClass`, both will be applied together.

### Applicable Templates

Because `elClass` properties apply to the same properties as `variants`, its properties are applicable to the respective templates. For example, if you are directly specifying a class for [`tileFooter`](#codetilefootercode-variants), the applicable templates are `text_item` and `media_item`.

### Options

The values that can be used in the elClass are found in the [Text and Colors](https://duckduckgo.com/styleguide#txt-n-color) section of the DuckDuckGo Style Guide. Currently, you can pass the following types of classes:

- Precision font sizes (classes which begin with `.tx--`, such as `.tx--25`)
- Text colors (classes which begin with `.tx-clr--`, such as `.tx-clr--dk`)

### Usage

`elClass` is parallel to `variants` in syntax, and both options can be specified under `templates` simultaneously. The properties are the same as those documented as [Variants](#variants).

```javascript
templates: {
    ...
    elClass: {
        tileSubtitle: 'tx--25',
        tileFooter: 'tx--11',
        ...
    }
 }
```

### Example

- Tor Node: ["tor node 198.96.155.3"](https://duckduckgo.com/?q=tor+node+198.96.155.3&ia=tornode)  ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/zaahir/tor-node-refine/share/spice/tor_node/tor_node.js#L185))
