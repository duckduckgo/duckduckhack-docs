# Template Groups

Template groups are preset properties for `template` and its `options` that work well together. In most cases at least one group will be a good fit for your Instant Answer.

**We strongly recommend using a template group in your Instant Answer.** Of course, if you cannot use an available template for your Instant Answer, definitely let us know. E-mail us at open@duckduckgo.com and we'll help you. We may find that a custom template is necessary, and we'll work with you to create an awesome one. (Who knows, your idea may inspire the next official template group!)

## How Template Groups Work

Setting a template group automatically sets the `item` and `detail` templates for you. Some template groups also set an `item_detail` template and a few default `options`. 

You can easily customize the appearance of the template group by overriding the default `options` in your Instant Answer frontend code. The appearance will also be affected by which data is returned with each item.

## Picking a Template Group

The best template group for your Instant Answer depends on what your Instant Answer is returning. Below are a few suggestions to help you narrow down your options.

A quick way to get a feel for the different template groups is to [browse the Instant Answer directory](https://duck.co/ia). You can filter by the template group used on the right of the page.

### My Instant Answer returns "things" where visuals are important 

The [Media](#media-template-group) template group works well when an image is a significant part of the display of an item, as might be a title and a rating. Also consider the [Movies](#movies-template-group) template group.

Examples that make a great fit for the Media or Movies template groups include:

- TV shows/[Movies](https://duckduckgo.com/?q=currently+in+theaters)
- Games
- [Courses](https://duckduckgo.com/?q=computer+science+online+course)

If your Instant Answer results *are* themselves images or videos, consider the [Images](#images-template-group) or [Videos](#videos-template-group) template groups.

### My Instant Answer returns detailed "lookup" information

The [Info](#info-template-group) template group is designed for Instant Answers that feature in-depth information about one item. It also provides an auxiliary section to display further detail in table or list format. 

Examples include:

- [Recipes](https://duckduckgo.com/?q=how+to+mix+a+tom+collins&ia=recipes)
- [Cards](https://duckduckgo.com/?q=mtg+Boros+Reckoner&ia=magicthegathering)
- [Books](https://duckduckgo.com/?q=book+reviews+moonwalking+with+einstein&ia=books)
- [Bands](https://duckduckgo.com/?q=weezer+band)
- [Addresses](https://duckduckgo.com/?q=1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa)
- [Characters](https://duckduckgo.com/?q=bulbasaur+pokemon)

The [List](#list-template-group) template group works well for lookups that don't need an image; this group is excellent for displaying attributes in just a list or table format. Take a look at the following example:

- [WhoIs](https://duckduckgo.com/?q=whois+google.com)

### My results are mainly text, with a possible icon or logo

The [Text](#text-template-group) and [Icon](#icon-template-group) template groups are simple templates for presenting text results. They both share the same `item` template, while the Icon group's `detail` template is better suited to displaying an icon image. 

These results fit this format well:

- [Software](https://duckduckgo.com/?q=alternative+to+notepad&ia=software)
- [Code blocks](https://duckduckgo.com/?q=Fizz+Buzz+in+C&ia=codesnippet)
- [Jobs](https://duckduckgo.com/?q=perl+jobs+in+san+francisco&ia=jobs)
- [Records](https://duckduckgo.com/?q=bugid+234&ia=launchpad)
- [Simple answers](https://duckduckgo.com/?q=namecheap+http%3A%2F%2Finstantanswerparty.com&ia=domain)
- [Long blocks of text](https://duckduckgo.com/?q=baconipsum+4&ia=baconipsum)

### My Instant Answer returns products with prices, ratings, and brands/authors/artists

The [Products](#product-template-group) template group is great for items characterized by a price, brand, and rating. This is a good template group where images are important. 

Examples of results that work well with the Products template group include:

- [Magazines issues](https://duckduckgo.com/?q=newint&ia=magazines)
- [Parts](https://duckduckgo.com/?q=ne555+specs&ia=parts)
- [Apps](https://duckduckgo.com/?q=tiny+piano+for+iphone&ia=apps)
- [Events](https://duckduckgo.com/?q=live+show+weezer&ia=concerts)
- [Books](https://duckduckgo.com/?q=amazon+ray+bradbury&ia=products)
- [Physical products](https://duckduckgo.com/?q=amazon+ninja+costume&ia=products)

### My Instant Answer returns location-based results

The [Places](#places-template-group) template group is perfect for results where location is an important aspect. This template group displays single and multiple items on a map.

Results that would make a good fit for the Places template group include:

- [Parking](https://duckduckgo.com/?q=parking+in+philadelphia&ia=parking)
- [Local businesses](https://duckduckgo.com/?q=restaurant+in+laguna+beach)
- Hiking trails
- Historical sites
- Surf spots
- Shark GPS locations

### My Instant Answer is amazingly unique and existing template groups won't meet my needs

We encourage you to think hard about using an existing template group. For example, many `detail` templates accept custom handlebars sub-templates. Additionally, many template features can be toggled. 

If working within existing template groups feels too constraining, we're happy to help you figure out how your vision could be accomplished using existing templates. **E-mail us at [open@duckduckgo.com](mailto:open@duckduckgo.com) and we'll work with you to find the best way to express your idea.**

In this context, the [Base](#base-template-group) template group is a minimal container template that accepts totally custom markup. Because of this, the Base template group is **a complete last-resort** because of the amount of work up front, and difficult maintenance over time. 

**Please hold off from using the Base template group until you've contacted us.** We hope to save you from ongoing, manual maintenance of your Instant Answer display. Additionally, knowing where our templates fall short helps us understand where we can improve our existing set of templates.

<!--
Examples of Instant Answers that do not fit into any template groups:

- [Ducksay](https://duckduckgo.com/?q=ducksay+quack!&ia=ducksay)
- [Flight itineraries](https://duckduckgo.com/?q=Jetblue+Boston+to+Los+Angeles&ia=route)
- [Site functionality](https://duckduckgo.com/?q=is+reddit.com+working%3F&ia=answer)
- [Nutrition facts](https://duck.co/ia/view/nutrition)
- [Webcomics](https://duck.co/ia/view/xkcd_display)
-->

------

# Template Groups Reference

This reference explains what each template group looks like, how it works, and what content works fits it best. Each template group is accompanied by live examples, layout diagrams, code links, and available features.

These are the currently available template groups:

- [Text](#text-template-group)
- [Info](#info-template-group)
- [Products](#products-template-group)
- [Media](#media-template-group)
- [Icon](#icon-template-group)
- [Images](#images-template-group)
- [Movies](#movies-template-group)
- [Videos](#videos-template-group)
- [Places](#places-template-group)
- [Base](#base-template-group)

<!-- /summary -->

## A Note on Default Template Options

When no `options` are specified and no template `group` has been selected, the `options` are implicitly set as follows:

```javascript
    options: {
        price: true,
        brand: true,
        priceAndBrand: true,
        rating: true,
        ratingText: true,
        moreAt: true,
        content: false
    }
```

------

## Important Notes

1. Before using these templates in your code, please familiarize yourself with the method for displaying your Instant Answer type (for example, [Spice Display](https://duck.co/duckduckhack/spice_displaying) or [Goodie Display](https://duck.co/duckduckhack/goodie_displaying)). This will help understand the **proper usage of both the `templates` block and the `options` block**.

2. For your desired template features to display correctly, each item's data must contain the corresponding properties. Generally these are set with the aid of a [`normalize` function](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional), if they do not already exist in your [`data` object](https://duck.co/duckduckhack/display_reference#codedatacode-emobjectem-required).

Understanding these is crucial to implementing templates properly and effectively.

------

## Text Template Group

This template group is best used for results which are mostly text, where any images are icons or small logos. This template offers a title, description and footer.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'text'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'text'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'text_detail'
}
```

#### Default Templates Used

- [`text_item`](https://duck.co/duckduckhack/templates_reference#codetextitemcode-template)
- [`text_detail`](https://duck.co/duckduckhack/templates_reference#codetextdetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example Uses

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
    ![DuckDuckGo search for "github duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgithub_duckduckgo.png&f=1)

- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
    ![DuckDuckGo search for "what rhymes with awesome"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhat_rhymes_with_awesome.png&f=1)

- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js))
    ![DuckDuckGo search for "reddit duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Freddit_duckduckgo.png&f=1)


------

## Info Template Group

The `info` template group is designed for Instant Answers that feature in-depth information about one item. This includes an image, title, and a description or arbitrary content. It also provides an auxiliary section to display further detail in table or list format (to the right).

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'info'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'info'
// does this for you!
templates: {
    item: 'basic_image_item',
    detail: 'basic_info_detail',
    options: {
        moreAt: true,
        aux: false
    }
}
```

#### Default Templates Used

- [`basic_image_item`](https://duck.co/duckduckhack/templates_reference#codebasicimageitemcode-template)
- [`basic_info_detail`](https://duck.co/duckduckhack/templates_reference#codebasicinfodetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example Uses

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
    ![DuckDuckGo search for "green day band"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgreen_day_band.png&f=1)

- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
    ![DuckDuckGo search for "bitcoin price"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbitcoin_price.png&f=1)

- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))
    ![DuckDuckGo search for "gravatar matt"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgravatar_matt.png&f=1)


------

## Products Template Group

Best used to showcase products with an image, rating, review, brand and/or price. An optional `buy` sub-template can be used to provide a compelling call-to-action (i.e. button).

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'products'
}
```

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'products'
// does this for you!
templates: {
	item: 'products_item',
	detail: 'products_detail',
	item_detail: 'products_item_detail',
	wrap_detail: 'base_detail',
	options: {
	    rating: true,
	    price: true,
	    brand: true
	}
}
```

Using the Products template group also automatically makes the Product [model](https://duck.co/duckduckhack/display_reference#codemodelcode-emstringem-optional) available.

#### Default Templates Used

- [`products_item`](https://duck.co/duckduckhack/templates_reference#codeproductsitemcode-template)
- [`products_detail`](https://duck.co/duckduckhack/templates_reference#codeproductsdetailcode-template)
- [`products_item_detail`](https://duck.co/duckduckhack/templates_reference#codeproductsitemdetailcode-template)
- [`base_detail`](https://duck.co/duckduckhack/templates_reference#codebasedetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example Uses

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
    ![DuckDuckGo search for "buy batman lego"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbuy_batman_lego.png&f=1)

- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
    ![DuckDuckGo search for "flight tracking apps"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fflight_tracking_apps.png&f=1)

- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))
    ![DuckDuckGo search for "octopart 1770019-2"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Foctopart_1770019-2.png&f=1)


------

## Media Template Group

The `media` template group works well when an image is a significant part of the display of an item. Items can also have a title and a rating. 

The `item` template is essentially a simplified version of the Products template group. It also uses the same `detail` template as the Products template group.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'media'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'media'
// does this for you!
templates: {
    item: 'media_item',
    detail: 'basic_info_detail',
    item_detail: 'media_item_detail',
    options: {
		moreAt: true,
		aux: false
    }
}
```

#### Default Templates Used

- [`media_item`](https://duck.co/duckduckhack/templates_reference#codemediaitemcode-template)
- [`basic_info_detail`](https://duck.co/duckduckhack/templates_reference#codebasicinfodetailcode-template)
- [`media_item_detail`](https://duck.co/duckduckhack/templates_reference#codemediaitemdetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example Uses

- ["dogo news"](https://duckduckgo.com/?q=dogo+news&ia=kidsnews&iai=2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dogo_news/dogo_news.js))

<!--
- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))
    ![DuckDuckGo search for "BBC schedule"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbbc_schedule.png&f=1)
-->

------

## Icon Template Group

This template is similar to the **text** group, since it uses the same `item` template. However, the detail view is better suited to displaying an icon image.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'icon'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'icon'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'basic_icon_detail',
    item_detail: 'products_item_detail'
}
```

#### Default Templates Used

- [`text_item`](https://duck.co/duckduckhack/templates_reference#codetextitemcode-template)
- [`basic_icon_detail`](https://duck.co/duckduckhack/templates_reference#codebasicicondetailcode-template)
- [`products_item_detail`](https://duck.co/duckduckhack/templates_reference#codeproductsitemdetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example Uses

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))
    ![DuckDuckGo search for "alternative to photoshop"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Falternative_to_photoshop.png&f=1)
- ["oil production in Saudi Arabia"](https://duckduckgo.com/?q=oil+production+in+saudi+arabia&ia=answer) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/zanran/zanran.js))

------
## Images Template Group

A template group for displaying image results. This group is ideal when the Instant Answer result *is* an image, and the image's attributes are important (such as its dimensions, source, and original file).

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'images'
}
```

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'images'
// does this for you!
templates: {
    item: 'images_item',
    detail: 'images_detail'
}
```

Using the Images template group also automatically makes the Image [model](https://duck.co/duckduckhack/display_reference#codemodelcode-emstringem-optional) available.

#### Default Templates Used

- [`images_item`](https://duck.co/duckduckhack/templates_reference#codeimagesitemcode-template)
- [`images_detail`](https://duck.co/duckduckhack/templates_reference#codeimagesdetailcode-template)

### Example Uses

- ["duck images"](https://duckduckgo.com/?q=duck+images&ia=images) (built-in images search)

------
## Movies Template Group

An ideal template group for displaying movie results, but also great for other types of media such as books.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'movies'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'movies'
// does this for you!
templates: {
    item: 'basic_image_item',
    detail: 'products_detail',
    item_detail: 'products_item_detail',
    wrap_detail: 'base_detail',
    options: {
        price: false,
        brand: false,
        rating: false,
        ratingText: true
    },
    variants: {
        tile: 'poster'
    },
    elClass: {
        tileBody: 'is-hidden'
    }
}
```

#### Default Templates Used

- [`basic_image_item`](https://duck.co/duckduckhack/templates_reference#codebasicimageitemcode-template)
- [`products_detail`](https://duck.co/duckduckhack/templates_reference#codeproductsdetailcode-template)
- [`products_item_detail`](https://duck.co/duckduckhack/templates_reference#codeproductsitemdetailcode-template)
- [`base_detail`](https://duck.co/duckduckhack/templates_reference#codebasedetailcode-template)

### Example Uses

- ["dogobooks harry potter"](https://duckduckgo.com/?q=dogobooks+harry+potter&ia=kidsbooks) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dogo_books/dogo_books.js))
- ["movies with keira knightley"](https://duckduckgo.com/?q=movies%20with%20Keira%20Knightley&ia=movies) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/kwixer.js))
- ["jiro dreams of sushi rotten tomatoes"](https://duckduckgo.com/?q=jiro+dreams+of+sushi+rotten+tomatoes&ia=movies)([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/ea61d47ef8639cf4fb282b51e2185e3a807d1bd5/share/spice/movie/movie.js))

------
## Videos Template Group

A template group for displaying online video results. This group is ideal when the Instant Answer result *is* a video, and [can be viewed](https://duckduckgo.com/?q=gopro+videos&ia=videos&iai=hCsigWVqA-M) on the search results page.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'videos'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'videos'
// does this for you!
templates: {
    item: 'videos_item',
    detail: 'videos_detail'
}
```

Setting the Videos template group also automatically makes the Video [model](https://duck.co/duckduckhack/display_reference#codemodelcode-emstringem-optional) available.

#### Default Templates Used

- [`videos_item`](https://duck.co/duckduckhack/templates_reference#codevideositemcode-template)
- [`videos_detail`](https://duck.co/duckduckhack/templates_reference#codevideosdetailcode-template)

### Example Uses

- ["gopro videos"](https://duckduckgo.com/?q=gopro+videos&ia=videos&iai=hCsigWVqA-M) (built-in videos search)

------
## Places Template Group

This template group is ideal for displaying results where location is an important factor to the searcher. The Places template group makes it easy for searchers to view a map showing all results, or highlighting a particular item without leaving the search page.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'places'
}
```

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'places'
// does this for you!
templates: {
    item: 'places_item',
    detail: 'places_detail'
}	
```

Using the Places template group also automatically makes the Place [model](https://duck.co/duckduckhack/display_reference#codemodelcode-emstringem-optional) available.

#### Default Templates Used

- [`places_item`](https://duck.co/duckduckhack/templates_reference#codeplacesitemcode-template)
- [`places_detail`](https://duck.co/duckduckhack/templates_reference#codeplacesdetailcode-template)

#### Alternative Templates

Specify these *item* templates to replace the default `places_item` template, while maintaining the unique 'flip' behavior of `places_item`. 

- [`basic_flipping_item`](https://duck.co/duckduckhack/templates_reference#codebasicflippingitemcode-template)
- [`base_flipping_item`](https://duck.co/duckduckhack/templates_reference#codebaseflippingitemcode-template)

#### Places Model and View

The Places template group works together with the Places **model** and Places **view**. The Places model and view enable special map functionality and behaviors that make Instant Answers using Places valuable and delightful.

The model and view are specified alongside the template group property in your Instant Answer [display options](https://duck.co/duckduckhack/display_reference#views).

To work correctly, the places model requires **additional values** passed that do not appear directly in the templates. Make sure that each item includes the attributes required by the places model. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

The available attributes for the Places Model are:

- `id` *string* 
	Unique identifier for the location
- `name` *string*
	Name of the location
- `address` *string*
	Display address of the location
- `city` *string*
- `neighborhood` *string*
	If neighborhood and city are both passed in, it will use neighborhood for the tile and fall back to the city when it's not there
- `image` *string* 
	Path to image thumbnail to be used for the location, will use default marker image if none is provided
- `polygonPoints` *array*
	If the location represents a region, array of lat/lon coordinates that create the shaded outline in queries like 'Paris map'
- `lat` *number* 
	Latitude of the location
- `lon` *number* 
	Longitude of the location
- `rating` *number* 
	Number from [0-5], supports half's, i.e. `3.5`
- `ratingImageURL` *string*
	Optional, use custom rating image URL (i.e. Yelp)
- `reviews` *number* 
	Number of reviews
- `price` *number* 
	Integer from [0-4], will be converted to up to four `$` symbols, for example `$$$$`
- `hours` *object* 
	Hash where three-char days are the keys and the values are a string of hours for that day, i.e.: `{ 'Mon': '8am - 5pm', 'Thu': '1pm - 5pm' }`
- `phone` *string*

Below are examples of the objects passed to the `data` property in your Instant Answer display options (in this case, `Spice.add()`). These might be directly found in your `api_result` or created by defining a [`normalize`](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional) function.

```javascript
Spice.add({
    id: 'landmarks',
    name: 'Landmarks',
    model: 'Place',
    view: 'Map',
    templates: {
        group: 'places'
    },
    meta: {
        sourceName: 'Wikipedia',
        sourceUrl: 'https://wikipedia.org'
    },
    data: [
        {
        	id: 'uniqueid-1',
	        name: 'Empire State Building',
	        url: 'https://en.wikipedia.org/wiki/Empire_State_Building',
	        image: 'https://upload.wikimedia.org/...480px-Empire_State_Building_by_David_Shankbone.jpg',
	        rating: '3.5',
	        address: '350 Fifth Ave',
	        neighborhood: 'Midtown',
	        city: 'New York City',
	        price: 3,
	        lat: 40.7484324,
	        lon: -73.98566413,
	        hours: {
	            Thu: '8am - 5pm'
	        }
	    }
    ]
});
```

Example of rendering multiple locations as tiles with an expandable map:

```javascript
Spice.add({
    id: 'landmarks',
    name: 'Landmarks',
    model: 'Place',
    view: 'Places',
    templates: {
        group: 'places'
    },
    meta: {
        type: 'Landmarks',
        sourceName: 'Wikipedia',
        sourceUrl: 'https://wikipedia.org'
    },
    data: [
            {
                id: 'uniqueid-1',
                name: 'Empire State Building',
                url: 'https://en.wikipedia.org/wiki/Empire_State_Building',
                image: 'https://upload.wikimedia.org/...480px-Empire_State_Building_by_David_Shankbone.jpg',
                rating: '3.5',
                address: '350 Fifth Ave',
                neighborhood: 'Midtown',
                city: 'New York City',
                price: 3,
                lat: 40.7484324,
                lon: -73.98566413,
                hours: {
                    Thu: '8am - 5pm'
                }
            }, 
            {
                id: 'uniqueid-2',
                name: 'Central Park',
                url: 'https://en.wikipedia.org/wiki/Central_Park',
                image: 'https://upload.wikimedia.org/...240px-Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg',
                rating: 5,
                address: '86th Street, Traverse Road',
                neighborhood: 'Midtown',
                city: 'New York City',
                lat: "40.78257765",
                lon: "-73.9654435614027",
                phone: '867-5309',
                reviews: 327,
                polygonPoints: [
                    ["-73.9812971", "40.7685782"],
                    ["-73.9812422", "40.7686381"],
                    ["-73.9808211", "40.7692536"],
                    ...
                    ["-73.9810729", "40.7683834"],
                    ["-73.9811234", "40.7684477"],
                    ["-73.9811992", "40.7685112"],
                    ["-73.9812971", "40.7685782"]
                ]
            }
        ]
});
```

### Example use of the 'places' template group

- ["events in new york"](https://duckduckgo.com/?q=events+in+new+york&ia=events)
- ["parking panda"](https://duckduckgo.com/?q=parking+in+philadelphia) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js))
    ![DuckDuckGo search for "parking in philadelphia"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fparking_panda.png&f=1)


------

## List Template Group

The List template group was designed for displaying in-depth attributes of one item. These attributes can be displayed as either a bulleted list of properties, *or* a table of key-value pairs. 

Multiple items are displayed using the same `text_item` template used by Text and Icon template groups. As a result, this template group is mainly useful for Instant Answers designed to **return a single item** with detailed properties.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'list'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'list'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'list_detail'
}
```

#### Default Templates Used

- [`text_item`](https://duck.co/duckduckhack/templates_reference#codetextitemcode-template)
- [`list_detail`](https://duck.co/duckduckhack/templates_reference#codelistdetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example use of the `list` template group

- ["whois"](https://duckduckgo.com/?q=whois+mozilla.org) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js))
	![DuckDuckGo search for "whois mozilla.org"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhois_results.png&f=1)

------

## Base Template Group

This is the most rudimentary template group. It provides a minimal container template that accepts totally custom markup.

Using this template group requires a *large amount of work* up front, and *difficult maintenance* over time. As a result, **this template should be a last resort.**

If you feel that other template groups do not meet your needs, please **contact us at [open@duckduckgo.com](mailto:open@duckduckgo.com) *before* using the Base Template Group**. We'll work with you to find the best way to express your idea and avoid ongoing, manual maintenance for your Instant Answer.

### Usage

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'base'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'base'
// does this for you!
templates: {
    item: 'base_item',
	detail: 'base_detail',
	options: {
	    price: false,
	    brand: false,
	    rating: false,
	    ratingText: false,
	    rowHighlight: false,
	    keySpacing: false,
	    moreAt: false
	}
}
```

#### Default Templates Used

- [`base_item`](https://duck.co/duckduckhack/templates_reference#codebaseitemcode-template)
- [`base_detail`](https://duck.co/duckduckhack/templates_reference#codebasedetailcode-template)

See the **[important notes](#important-notes)** for making this template display correctly.

### Example Uses

- ["gandhi quote"](https://duckduckgo.com/?q=gandhi+quote) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/brainy_quote/brainy_quote.js))
    ![DuckDuckGo search for "gandhi quote"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgandhi_quote.png&f=1)

- ["cpan App::cpanminus"](https://duckduckgo.com/?q=cpan+App::cpanminus) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js))
    ![DuckDuckGo search for "cpan App::cpanminus"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fcpan_app_cpanminus.png&f=1)

- ["define indelible"](https://duckduckgo.com/?q=define+indelible) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js))
    ![DuckDuckGo search for "define indelible"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fdefine_indelible.png&f=1)
