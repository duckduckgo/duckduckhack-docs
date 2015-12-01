
# Variants

If you'd like to modify a template to fit your needs, the Instant Answer framework offers preset options called Variants. Variants are passed as the `variants` property of `templates`, in your Instant Answer display options.

Variants correspond to pre-determined css classes (or combinations of classes) from the [DDG style guide](https://duckduckgo.com/styleguide) that work particularly well in each context.

*We strongly recommend using variants since they make it easy to quickly customize the appearance in a standardized way. However, if variants do not meet your needs, you may consider [directly specifying classes](#directly-specifying-classes).*

## `tile` Variants

If the default tile dimensions are not perfect for your Instant Answer result, you can use tile variants to modify the containers of your `item` template.

![tile variant diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/tile_variant.png)

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

![tileTitle variant diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/tiletitle_variant.png)

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

![tileSnippet diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/tilesnippet_variant.png)

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

![tileFooter variant diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/tilefooter_variant.png)

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

![tileRating variant diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/tilerating_variant.png)

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

![iconImage variant diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/iconimage_variant.png)

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

![iconBadge variant diagram](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/variant_diagrams/iconbadge_variant.png)

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

Because `elClass` properties apply to the same properties as `variants`, its properties are applicable to the respective templates. For example, if you are directly specifying a class for [`tileFooter`](#tilefooter-variants), the applicable templates are `text_item` and `media_item`.

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

To create a rounded icon, the [Chinese Zodiac Goodie](https://duck.co/ia/view/chinese_zodiac) uses both `elClass` and `variants` together.

![chinese zodiac IA](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/chinese_zodiac.png)

This is a Goodie, and these properties were [set in Perl, on the server](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/frontend-reference/setting-goodie-display.html#setting-display-properties-in-a-goodie):

```perl
templates => {
    group => "icon",
    elClass => {
        iconImage => "bg-clr--blue-light circle"
    },
    variants => {
         iconImage => 'large'
    }
}
```

You can learn more about [setting Goodie display options in Perl](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/frontend-reference/setting-goodie-display.html#setting-display-properties-in-a-goodie).

### Example

- Tor Node: ["tor node 198.96.155.3"](https://duckduckgo.com/?q=tor+node+198.96.155.3&ia=tornode)  ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/zaahir/tor-node-refine/share/spice/tor_node/tor_node.js#L185))
