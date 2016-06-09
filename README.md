# toolbox.scss

`toolbox.scss` provides a number of utility classes and mixins. It's an unopinionated library
meant to save you time when starting new projects, and is best used in conjunction with another CSS framework
or writing methodology.

## How do I get it?

If you're using npm:

  `npm install toolbox-css`

Then include the `toolbox.scss` file from within the `node-modules` directory. Don't forget to edit the `toolbox-config`
file for your needs. Its in the same directory.

Otherwise download and include `toolbox.scss` and `toolbox-config.scss` in your project. Modify the config to your liking,
by following the information in the comments or in the guide below. If you're not using Sass, just download `toolbox.css` -
a CSS compiled version of the library using default settings. It should be fine for most projects.

## Toolbox does

- Offer many common utility classes.
- Simplify responsive design.
- Promote simple selectors and performant CSS.

## Toolbox doesn't

- Add vendor prefixes. Use tools like Autoprefixer to achieve cross-browser compatibility.
- Style common components such as buttons, inputs or navigation.
- Make assumptions about the layout of the your page.

## What's the point?

Often I've found that I need to create new classes to apply a single, often common style to an element. Or worse
I've seen people try to just use whatever they have available to style very nested elements, resulting in things like
`.component > div span:nth-child(2)`, this is both inefficient and very dependent on the HTML structure. The best
solution I've found is using simple utility methods for common properties and values, but it's tedious to write all
of them, every time you begin a new project, and here are we.

`toolbox` provides some of the most common properties and values, described with sane names, and mixins that
work in unison with a config file to suit every project's need.

## The config file

At the heart of `toolbox`, lies the config. A file consisting of only commented variables,
with some sensible defaults in case you don't care much about customizing the library.
The settings are divided in categories, and comments in the source code describe
their functionality, however let's go over them in more detail here.

#### **General**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`namespace` | Any valid selector or `null` | `null` | A namespace to apply to all classes from the library.
`short-names` | `true`, `false` | `false` | Whether the class names should use their short variant. For example `.absolute` or `.abs`.
`dashed-names` | `true`, `false` |  `true` | Whether to include the `-` character in class names. For example `.float-left` or `.floatleft`.
`prefix` | `null` or `string` | `null` | A prefix to prepend to all class names. For example `.pre-relative`.
`suffix` | `null` or `string` | `null` | A suffix to append to all class names. For example `.relative-suf`.
`visualize-errors` | `true`, `false` | `true` | Whether to show `toolbox` errors as a pseudo element in the HTML or not.

#### **Media queries**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`breakpoints` | A map of `key`: `value` pairs | `(large, 1235px, medium: 1024px, small: 768px, mobile: 320px)` | The described list will be used in conjunction with the `breakpoint` mixin, to easily create `@media` rules.
`breakpoint-offset` | integer |  `0` | A pixel value offset to account for any static content.

#### **Dimensions**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`padding-iterator` | integer | 10 | The offset between two padding classes.
`padding-min` | integer | 10 | The minimum padding class value.
`padding-max` | integer | 50 | The maximum padding class value.
`margin-iterator` | integer | 10 | The offset between two margin classes.
`margin-min` | integer | 10 | The minimum margin class value.
`margin-max` | integer | 50 | The maximum margin class value.

#### **Text**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`font-sizes` | A list of (`key`, `value`) pairs | `('base', 16)` | Used to generate `font-size` classes. For instance `.base-font { font-size: 16px; font-size: 1.6rems; }`
`rem-friendly` | `true`, `false` | `true` | Whether to try and set the values to `rem` units. Note that this will add some styling to the `html` and `body` elements.

#### **Colors**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`colors` | A list of (`key`, `value`) pairs | `('white', #fff), ('black', #000)` | Used to generate color classes.
`background-color-classes` | `true`, `false` | `true` | Whether to generate color classes for `background-color`. For instance `.white-background { background-color: #fff; }`.
`text-color-classes` | `true`, `false` | `false` | Whether to generate color classes for `color`. For instance `.white-text { color: #fff; }`.
`border-color-classes` | `true`, `false` | `false` | Whether to generate color classes for `border-color`. For instance `.white-borders { border-color: #fff; }`.

## Classes

The classes are all generated through a Sass compiler, based on the settings in your config. While some have static names,
others are more dynamic, usually using keywords or even numeric values, denoted below with `#`. If you want to define your
own class, which will be treated with the same manipulations from the config file, use the `class` mixin like so:

  `@include class('long-name', 'short-name'(optional))`
  
If you've set a string for the `$tb-namespace` variable in the config, you can use the `namespace` mixin, which will wrap all
it's `@content` in the passes selector string. This is particularly useful when the code you want to namespace is spread out
through several files, as changing the namespace becomes much easier and less error prone.

As for the full list of classes and their properties, they are as follows:

**Name** | **Short** | **Styles**
--- | --- | --- | ---
.static | .sta | position: static;
.relative | .rel | position: relative;
.absolute | .abs | position: absolute;
.fixed | .fix | position: fixed;
.inline-block | .in-bl | display: inline-block;
.inline | .in | display: inline;
.block | .bl | display: block;
.table | .tb | display: table;
.table-row | .tr | display: table-row;
.table-cell | .td | display: table-cell;
.hidden| .hide | display: none;
.flex| .fl | display: flex;
.inline-flex | .in-fl | display: inline-flex;
.float-left | .flo-l | float: left;
.float-right | .flo-r | float: right;
.flip-horizontal | .f-h | transform: scaleX(-1); filter: FlipH;
.flip-vertical | .f-v | transform: scaleY(-1); filter: FlipV;
.clear | .cl | content: ''; display: block; clear: both;
.centered | .cen | margin-right: auto; margin-left: auto;
.border-box | .b-bo | box-sizing: border-box;
.vertical-margin | .v-mar | margin-left: initial; margin-right: initial;
.horizontal-margin | .h-mar | margin-top: initial; margin-bottom: initial;
.vertical-padding | .v-pad | padding-left: initial; padding-right: initial;
.horizontal-padding | .h-pad | padding-top: initial; padding-bottom: initial;
.#-padding | .#-pad | padding: #px;
.#-margin | .#-mar | margin: #px;
.full-width | .f-wi | width: 100%;
.half-width | .h-wi | width: 50%;
.third-width | .t-wi | width: 33.33%;
.quarter-width | .q-wi | width: 25%;
.full-height | .f-he | height: 100%;
.half-height| .h-he | height: 50%;
.third-height | .t-he | height: 33.33%;
.quarter-height | .q-he | height: 25%;
.text-center | .t-cen | text-align: center;
.text-left | .t-le | text-align: left;
.text-right | .t-ri | text-align: right;
.text-middle | .t-mid | vertical-align: middle;
.bold | .b | font-weight: bold;
.italic | .i | font-style: italic;
.underlined | .un | text-decoration: underlined;
.line-through | .li-t | text-decoration: line-through;
.uppercase | .up | text-transform: uppercase;
.lowercase | .low | text-transform: lowercase;
.capitalize | .cap | text-transform: capitalize;
.small-caps | .sm-cap | text-variant: small-caps;
.#-font | .#-f | font-size: #px; font-size: #rem;
.#-background | .#-bg | background-color: #;
.#-text | .#-t | color: #;
.#-borders | .#-b | border-color: #;
.#-hide | .#-h | display: none;
.#-show | .#-s | display: none;

### Breakpoints

When working on responsive design, you can use the `breakpoint`, `below` and `above` mixins, by passing the first a keyword
from the `$tb-breakpoints` list, and the other two a pixel width they should apply styles to. Additionally they take
a `@content` block, which are the rules they'll apply. For instance:

`@include breakpoint(small) {
  .element-to-modify-on-small-screens {
    background-color: red;
  }
}`

You also have the listed above media classes, ending in `-show` and `-hidden`. These classes
will be generated for each element in your breakpoints list, and when added to an element will either show or hide it based
on the screen width.
