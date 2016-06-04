# toolbox.scss

`toolbox.scss` provides a number of utility classes, mixins and functions. It's an unopinionated library
meant to save you time when starting new projects, and is best used in conjunction with another CSS framework
or writing methodology.

## How do I get it?

Just download and include `toolbox.scss` and `toolbox-config.scss` in your project. Modify the config to your liking,
by following the information in the comments or in the guide below. If you're not using Sass, just download `toolbox.css` -
a CSS compiled version of the library using default settings. It should be fine for most projects.

## Toolbox does

- Offer many common utility classes, mixins and functions.
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

`toolbox` provides some of the most common properties and values, described with sane names, and mixins and functions that
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
`dashed-names` | `true`, `false` |  `true` | Whether to include the `-` character in class names. For instance `.float-left` or `.floatleft`.
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

## Mixins and functions

The library comes packaged with several mixins and functions. Some are strictly for internal usage (as they use config variables),
while others are used in the library or in conjunction with it, but can be usually used externally
by your program.

#### *Functions*

`str-replace(stringToSearch, searchQuery, replaceWith: '')` - Recursively replaces all instances of a substring in a string.
If the optional, third parameter is not passed, all instances will be replaced by an emtry string(`''`).

#### *Mixins*

`error(message)` - Logs a warning in the terminal which compiles Sass, and if `$tb-visualize-errors` is set to true,
prepends an error message to the `body` element via the `::before` pseudoclass.

`namespace() { //content }` - Wraps all given content under a namespace, if one is set under `$tb-namespace`.

`tb-class(name, shortName: null) { //content }` - Used for declaring all `toolbox` classes. If you define your classes
using this mixin, they will pass through all transformative operations such a removing dashes.

## Classes

Finally, and most importantly - all classes featured in `toolbox`.

**Name** | **Short** | **Styles**
--- | --- | --- | ---
.relative | .rel | position: relative;
.absolute | .abs | position: absolute;
.fixed | .fix | position: fixed;
.inline-block | .in-bl | display: inline-block;
.inline | .in | display: inline;
.block | .bl | display: block;
.hidden| .hide | display: none;
.flex| .fl | display: flex;
.inline-flex | .in-fl | display: inline-flex;
.float-left | .flo-l | float: left;
.float-right | .flo-r | float: right;
.clear | .cl | content: ''; display: block; clear: both;
.centered | .cen | margin-right: auto; margin-left: auto;
.vertical-margin | .v-mar | margin-left: initial; margin-right: initial;
.horizontal-margin | .h-mar | margin-top: initial; margin-bottom: initial;
.vertical-padding | .v-pad | padding-left: initial; padding-right: initial;
.horizontal-padding | .h-pad | padding-top: initial; padding-bottom: initial;
.#-padding | .#-pad | padding: #px;
.#-margin | .#-mar | margin: #px;