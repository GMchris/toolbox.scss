# toolbox.scss

`toolbox.scss` is the result of frustration from having to rewrite a lot of CSS at
the start of new projects. It aims to provide developers with a basic library of
utility classes, functions and mixins to speed up the development process as well
as result in more readable, reliable and performant code. Despite it's strengths
this library isn't meant to be a sole framework or only external CSS tool.

## Toolbox doesn't

- Add vendor prefixes. Use tools like Autoprefixer to achieve cross-browser compatibility.
- Style common components such as buttons, inputs or navigation.
- Make assumptions about the layout of the your page.

## Toolbox does

- Offer many common utility classes, mixins and functions.
- Promote simple selectors and optimized pages.

## So what's the idea?

Lets look at a common scenario. You're styling a component and you've used a few
classes to make it look just right.

```
  <div class="component">
    <div class="component-heading"></div>
    <div class="component-body">
      <div><span>One</span></div>
      <div><span>Two</span></div>
      <div><span>Three</span></div>
    </div>
  </div>
```
But the `span` element inside the second `div` needs to be `uppercase` and has to
be painted in the company color, let's say `pink`. How would you approach that?
You could add a `.component-body-fancy-text` class to it. That way your selector is still fast.
But with this approach you'll soon find it harder and harder to invent new names for
these classes, as well as notice a considerable bulk in your code. What else?
Pseudo-selectors of course! `n-th` child is just what we need. We'll grab the most
specific class we have and add some stuff to the back and voila:

`.component-body div:nth-child(2) span`

This will work, for sure, but while you're not creating a new class, it's actually
a much worse solution, and I'm sad to say, one I've seen quite often. Not only
is your selector many times slower now, but minor changes to the markup will force
you to make changes to the CSS as well.

What I suggest, and what this library excels at are the aforementioned lightweight
utility classes. Things like `position: absolute` and `float: left` are written a
billion times a day and very often they are the only thing applied to a certain
specific selector. In addition to that, functions and mixins are copy/pasted in
droves get some code to work. Toolbox.scss wraps them all in an extremely small
package.

If you're still not convinced this library is neccessary for you or your projects,
you might be right. As I mentioned, it promotes a certain kind of styling, and
if you're not using a preprocessor a lot of it's functionality may be lost to you,
however I firmly believe that any project, or more accurately any developer can benefit
from using it.

## The config file

At the heart of `toolbox`, lies the config. A file consisting of only commented variables,
with some sensible defaults in case you don't care much about customizing the library.
The settings are divided in categories, and comments in the source code describe
their functionality, however let's go over them in more detail here.

#### **General**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`$tb-namespace` | Any valid selector or `null` | `null` | A namespace to apply to all classes from the library.
`$tb-dashed-names` | `true`, `false` |  `true` | Whether to include the `-` character in class names. For instance `.float-left` or `.floatleft`.
`$tb-visualize-errors` | `true`, `false` | `true` | Whether to show `toolbox` errors as a pseudo element in the HTML or not.

#### **Media queries**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`$tb-breakpoints` | A list of (`key`, `value`) pairs | `(large, 1235px) (medium, 1024px) (small, 768px) (mobile, 320px)` | The described list will be used in conjunction with the `breakpoint` mixin, to easily create `@media` rules.
`$tb-breakpoint-offset` | integer |  `0` | A pixel value offset to account for any static content.

#### **Dimensions**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`$tb-padding-iterator` | integer | 10 | The offset between two padding classes.
`$tb-padding-min` | integer | 10 | The minimum padding class value.
`$tb-padding-max` | integer | 50 | The maximum padding class value.
`$tb-margin-iterator` | integer | 10 | The offset between two margin classes.
`$tb-margin-min` | integer | 10 | The minimum margin class value.
`$tb-margin-max` | integer | 50 | The maximum margin class value.

#### **Text**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`$tb-font-sizes` | A list of (`key`, `value`) pairs | `('base', 16)` | Used to generate `font-size` classes. For instance `.base-font { font-size: 16px; font-size: 1.6rems; }`
`$tb-rem-friendly` | `true`, `false` | `true` | Whether to try and set the values to `rem` units. Note that this will add some styling to the `html` and `body` elements.

#### **Colors**

**Property** | **Parameter** | **Default** | **Description**
--- | --- | --- | ---
`$tb-colors` | A list of (`key`, `value`) pairs | `('white', #fff), ('black', #000)` | Used to generate color classes.
`$tb-background-color-classes` | `true`, `false` | `true` | Whether to generate color classes for `background-color`. For instance `.white-background { background-color: #fff; }`.
`$tb-text-color-classes` | `true`, `false` | `false` | Whether to generate color classes for `color`. For instance `.white-text { color: #fff; }`.
`$tb-border-color-classes` | `true`, `false` | `false` | Whether to generate color classes for `border-color`. For instance `.white-borders { border-color: #fff; }`.
