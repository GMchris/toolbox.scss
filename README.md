# toolbox.scss

`toolbox.scss` provides a number of utility classes, mixins and functions. It's an unopinionated library
meant to save you time when starting new projects, and is best used in conjunction with another CSS framework
or writing methodology.

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
of them, every time you begin a new project, and that's where `toolbox` comes in.

## The config file

At the heart of `toolbox`, lies the config. A file consisting of only commented variables,
with some sensible defaults in case you don't care much about customizing the library.
The settings are divided in categories, and comments in the source code describe
their functionality, however let's go over them in more detail here.

#### **General**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`namespace` | Any valid selector or `null` | `null` | A namespace to apply to all classes from the library.
`dashed-names` | `true`, `false` |  `true` | Whether to include the `-` character in class names. For instance `.float-left` or `.floatleft`.
`visualize-errors` | `true`, `false` | `true` | Whether to show `toolbox` errors as a pseudo element in the HTML or not.

#### **Media queries**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`breakpoints` | A list of (`key`, `value`) pairs | `(large, 1235px) (medium, 1024px) (small, 768px) (mobile, 320px)` | The described list will be used in conjunction with the `breakpoint` mixin, to easily create `@media` rules.
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
