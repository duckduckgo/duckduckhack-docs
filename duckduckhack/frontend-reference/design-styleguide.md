# Instant Answer Design Style Guide

Being an open-source project with many contributors from all over the world, we strive for all our Instant Answers to appear aesthetically consistent. 

This means we maintain certain visual aspects across all of our Instant Answers such as the fonts and colors used, as well as the layout and placement of common elements. This helps instill a feeling of familiarity in our users when they come across new Instant Answers and improves usability and comfort with the interface.

The most current design guide for all of DuckDuckGo, including Instant Answers, can be found at the [Official DuckDuckGo Style Guide](https://duckduckgo.com/styleguide).

This section explains how the style guide affects the creation of a new Instant Answer.

---

## Templates

Nearly all Instant Answers use [templates](https://duck.co/duckduckhack/templates_overview) as the easiest way to maintain consistency and, most importantly, maintainability over time.

Templates abstract away nearly all design concerns. They allow developers to focus on their Instant Answer's results rather than deal with browser compatibility, responsiveness, fonts, colors, or CSS in general.

To learn about the wide variety of built-in templates, start with the [Templates Overview](https://duck.co/duckduckhack/templates_overview).

## Built-In Style Elements

Thanks to the use of templates, directly writing HTML is uncommon. However, some Instant Answers will use custom templates. This is usually in the form of [sub-templates](https://duck.co/duckduckhack/templates_overview), and in rare cases, the [`base` template group](https://duck.co/duckduckhack/template_groups#base-template-group).

## Built-In Style Elements

When writing custom HTML, you can directly apply the built-in style resources documented in the [DuckDuckGo Style Guide](https://duckduckgo.com/styleguide) in your HTML. Using the built-in elements allows Instant Answers to automatically stay up-to-date with any DuckDuckGo style changes.

Applying style guide elements is straightforward. For example, to [style text](https://duckduckgo.com/styleguide#txt-n-color) as a large heading, simply use that class: 

```html
<div class="h-xxl">Your Heading</div>
```

To use an [icon](https://duckduckgo.com/styleguide#icons), add a class with the icon name:

```html
<span class="ddgsi ddgsi-clock"></span>
```

To set built-in images such as flags, make a JavaScript call to obtain the image URL and pass it to your template as data:

```javascript
DDG.settings.region.getLargeIconURL("CA");
```

## Giving Credit

Instant Answers are meant to first and foremost provide users with value in an accessible way, while providing credit to the original source. Every Instant Answer template provides the display of a ["More at..."](https://duck.co/duckduckhack/display_reference#codemetacode-emobjectem-required) link, which serves as a consistent place for users to see the data source.

Using Instant Answers for other goals, such as excessive self-promotion or inserting advertisements, particularly at the expense of usability, consistency, or usefulness - is not in line with the spirit of the community.
