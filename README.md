# Sass Basics

*Click <img src="assets/star.png" width="18" height="18" align="absmiddle" title="Star" /> if you like the project. Pull Request are highly appreciated.*

<br/>

## Q. What is Sass?

When stylesheets are getting larger, more complex, and harder to maintain. This is where a CSS pre-processor can help. Sass (which stands for 'Syntactically awesome style sheets) is an extension of CSS that enables you to use things like variables, nested rules, inline imports and more. It also helps to keep things organised and allows you to create style sheets faster.

Sass works by writing your styles in .scss (or .sass) files, which will then get compiled into a regular CSS file. The newly compiled CSS file is what gets loaded to your browser to style your web application. This allows the browser to properly apply the styles to your web page.

<p align="center">
  <img src="assets/sass-process.png" alt="Sass Process" width="300px;" />
</p>

**&#9885; [Try this example on CodeSandbox](https://codepen.io/learning-zone/pen/RwVprvO)**

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What are the SCSS basic features?

**1. Variables:**

Variables are useful for things like colors, fonts, font sizes, and certain dimensions, as you can be sure always using the same ones. Variables in SCSS start with `$` sign

**SCSS Style:**

```scss
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

**CSS Style:**

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

When the Sass is processed, it takes the variables we define for the `$font-stack` and `$primary-color` and outputs normal CSS with our variable values placed in the CSS. This can be extremely powerful when working with brand colors and keeping them consistent throughout the site.

**&#9885; [Try this example on CodeSandbox](https://codepen.io/learning-zone/pen/LYyWNGM)**

**2. Nesting:**

Basic nesting refers to the ability to have a declaration inside of a declaration.

**SCSS Style:**

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

**CSS Style:**

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

**&#9885; [Try this example on CodeSandbox](https://codepen.io/learning-zone/pen/qBmrZmv)**

**3. Partials:**

The partial Sass files contain little snippets of CSS that can be included in other Sass files. This is a great way to modularize your CSS and help keep things easier to maintain. A partial is a Sass file named with a leading underscore. You might name it something like `_partial.scss`.

The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. Sass partials are used with the `@use` rule.

**4. Modules:**

This rule loads another Sass file as a module, which means we can refer to its variables, mixins, and functions in our Sass file with a namespace based on the filename. Using a file will also include the CSS it generates in your compiled output!

**SCSS Style:**

```scss
// _base.scss
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```scss
// styles.scss
@use 'base';

.inverse {
  background-color: base.$primary-color;
  color: white;
}
```

**CSS Style:**

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

.inverse {
  background-color: #333;
  color: white;
}
```

**5. Mixins:**

A mixin provide to make groups of CSS declarations that you want to reuse throughout your site. You can even pass in values to make your mixin more flexible.

**SCSS Style:**

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box { @include transform(rotate(30deg)); }
```

**CSS Style:**

```css
.box {
  -webkit-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  transform: rotate(30deg);
}
```

**&#9885; [Try this example on CodeSandbox](https://codepen.io/learning-zone/pen/xxdqVPM)**

**6. Inheritance:**

Using `@extend` lets you share a set of CSS properties from one selector to another.  

**SCSS Style:**

```scss
/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

**CSS Style:**

```css
/* This CSS will print because %message-shared is extended. */
.message, .success, .error, .warning {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}
```

**&#9885; [Try this example on CodeSandbox](https://codepen.io/learning-zone/pen/ExmWKLG)**

**7. Operators:**

Sass has a handful of standard math operators like `+`, `-`, `*`, `/`, and `%`. In our example we're going to do some simple math to calculate widths for an aside & article.  

**SCSS Style:**

```scss
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```

**CSS Style:**

```css
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 62.5%;
}

aside[role="complementary"] {
  float: right;
  width: 31.25%;
}
```

*Note: Only Dart Sass currently supports `@use`. Users of other implementations must use the `@import` rule instead.*

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Explain the @include, @mixin, @function functions and how they are used. What is %placeholder?

**1. @mixin:** A mixin lets you make groups of CSS declarations that you want to reuse throughout your site

```scss
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}
```

```scss
.box { @include border-radius(10px); }
```

**2. @extend:** directive provides a simple way to allow a selector to inherit/extend the styles of another one.

```scss
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}
```

**3. %placeholder:** are classes that aren\'t output when your SCSS is compiled

```scss
%awesome {
    width: 100%;
    height: 100%;
}
body {
    @extend %awesome;
}
p {
    @extend %awesome;
}
```

```scss
/* Output */
body, p {
    width: 100%;
    height: 100%;
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. List out the differences between LESS and Sass?

|LESS                                 |Sass                         |
|-------------------------------------|-----------------------------|
|LESS compiler is coded in Javascript |Sass compiler is coded in Dart
|Variable names are prefaced with the @symbol |Variable name are prefaced with $ symbol
|LESS does not inherit multiple selectors with one set of properties | Sass inherits multiple selectors with one set of properties |
|LESS does not work with "unknown" units neither it returns syntax error notification for incompatible units or maths related syntax error|	Sass allows you to work with "unknown" units also returns a syntax error notification for incompatible units|

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. Why Sass is considered better than LESS?

* Saas allows you to write reusable methods and use logic statements, e., loops, and conditionals
* Saas user can access Compass library and use some awesome features like dynamic sprite map generation, legacy browser hacks * and cross-browser support for CSS3 features
* Compass also allows you to add an external framework like Blueprint, Foundation or Bootstrap on top
* In LESS, you can write a basic logic statement using a "guarded mixin", which is equivalent to Sass if statements
* In LESS, you can loop through numeric values using recursive functions while Sass allows you to iterate any kind of data
* In Sass, you can write your own handy functions

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What are Sass, Less, and Stylus?

They are CSS preprocessors. They are an abstraction layer on top of CSS. They are a special syntax/language that compile down into CSS. They make managing CSS easier, with things like variables and mixins to handle vendor prefixes (among other things). They make doing best practices easier, like concatenating and compressing CSS.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is file splitting and why should you use it?

File splitting helps organize your CSS into multiple files, decreasing page load time and making things easier to manage. How you decide to split them up is up to you, but it can be useful to separate files by component. For example, we can have all button styles in a file called `_buttons.scss` or all your header-specific styles in a file called `_header.scss`, main file, say _app.scss, and we can import those files by writing @import 'buttons';

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is Sass Partials?

By default, Sass transpiles all the **.scss** files directly. However, when you want to import a file, you do not need the file to be transpiled directly. If you start the filename with an underscore, Sass will not transpile it. Files named this way are called partials in Sass.

**Example:**

The following example shows a partial Sass file named "_colors.scss".

```css
/**
 * "_colors.scss
 */
$myPink: #EE82EE;
$myBlue: #4169E1;
$myGreen: #8FBC8F;
```

Now, if you import the partial file, omit the underscore. Sass understands that it should import the file "_colors.scss":

```css
/**
 * Sass Partials
 */
@import "colors";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: $myBlue;
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the @content directive used for?

The **@content** directive allows us to pass a content block into a mixin.

**SCSS Style:**

```scss
/**
 * @content directive
 */
@mixin media($width) {
  @media only screen and (max-width: $width) {
    @content;
  }
}

@include media(320px) {
  background: red;
}
```

**CSS Style:**

```css
@media only screen and (max-width: 320px) {
  background: red;
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is variable interpolation in Sass?

Interpolation allows us to interpolate sass expressions into a simple SASS or CSS code. Means, you can define selector name, property name, CSS at-rules, quoted or unquoted strings etc, as a variable.

**Syntax:**

```scss
#{$variable_name}
```

**SCSS Style:**

```scss
@mixin corner-icon($name) {
  /* using interpolation */
  .icon-#{$name} {
    background-image: url("/icons/#{$name}.svg");
  }
}

/* calling the above mixin */
@include corner-icon("mail");
```

**CSS Style:**

```css
.icon-mail {
  background-image: url("/icons/mail.svg");
}
```

Here, the value of the **$name** variable is added wherever we used **#{$name}** in our stylesheet.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the use of the @import function in Sass?

The SASS **@import** function helps us to import multiple SASS or CSS stylesheets together such that they can be used together. Importing a SASS file using the @import rule allows access to mixins, variables, and functions to the other file in which the other file is imported.

**Example:**

```scss
/**
 * common/_button.scss
 */
button {
  padding: .25em;
  line-height: 0;
}
```

```scss
/**
 * common/_lists.scss
 */
ul, ol {
  text-align: left;

  & & {
    padding: {
      bottom: 0;
      left: 0;
    }
  }
}
```

```scss
/**
 * style.scss
 */
@import 'common/button', 'common/lists';
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the meaning of DRY-ing out a mixin?

**DRY-ing** out a mixin means splitting it into **static** and **dynamic** parts. The dynamic mixin is the one the user is going to call, and the static mixin is only going to contain the pieces that would otherwise get duplicated.

**Example:**

```scss
@mixin button($color) {
		@include button-static;

	background-color: $color;
	border-color: mix(black, $color, 25%);
  
	&:hover {
		background-color: mix(black, $color, 15%);
		border-color: mix(black, $color, 40%);
	}
}

@mixin button-static {
	border: 1px solid;
	border-radius: 5px;
	padding: .25em .5em;
	
	&:hover {
		cursor: pointer;
	}
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the use of Sass Maps functions?

SASS provides the data type called map which represents one or more pairs of key values. The map, which returns a map, provides a new map and does not modify the initial map.

**Example:**

```scss
/**
 * map.get()
 */
$font-weights: ("regular": 400, "medium": 500, "bold": 700);

@debug map.get($font-weights, "medium"); // 500
@debug map.get($font-weights, "extra-bold"); // null
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. When can you use the %placeholders in Sass?

Placeholder is special kind of selector which is used for writing own SASS library. Its work is very similar to mixin without arguments. Placeholder selector starts with a **%** sign. Placeholder selectors are excluded in the compilation of the SASS file

**Syntax:**

```scss
@extend %( name_of_selector );
```

**SCSS Style:**

```scss
%button-format {
    padding: 10px 20px;
    border-radius: 15px;
    color: black;
}

.toolbar-button {
    @extend %button-format;
    background-color: lightpink;

    &:hover {
        background-color: rgb(155, 106, 114);
    }
}

.status-bar-button {
    @extend %button-format;
    background-color: lightblue;

    &:hover {
        background-color: blue;
    }
}
```

**CSS Style:**

```css
.status-bar-button, .toolbar-button {
    padding: 10px 20px;
    border-radius: 15px;
    color: black;
}

.toolbar-button {
  background-color: lightpink;
}
.toolbar-button:hover {
  background-color: #9b6a72;
}

.status-bar-button {
  background-color: lightblue;
}
.status-bar-button:hover {
  background-color: blue;
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What is the use of &combinator?

A combinator is something that explains the relationship between the selectors. A CSS selector can contain more than one simple selector. Between the simple selectors, we can include a combinator.

There are four different combinators in CSS:

* Descendant selector (space)
* Child selector (>)
* Adjacent sibling selector (+)
* General sibling selector (~)

**Example 01:** Without the combined child selector

```scss
card {
  outer {
    inner {
    	color: red;
    }
  }
}
```

**Example 02:** Using **>** selector

```scss
card {
 > outer {
   > inner {
     color: red;
   }
 }
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. What are number operations in Sass?

SASS allows for mathematical operations such as addition, subtraction, multiplication and division. They automatically convert between compatible units.

**SCSS Style:**

```scss
/**
 * style.scss
 */
$size: 25px;

h2 {
   font-size: $size + 5;
}

h3 {
   font-size: $size / 5;
}

.para1 {
   font-size: $size * 1.5;
}

.para2 {
   font-size: $size - 10;
}
```

**CSS Style:**

```css
h2 {
   font-size: 30px;
}

h3 {
   font-size: 5px;
}

.para1 {
   font-size: 37.5px;
}

.para2 {
  font-size: 15px;
}
```

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

#### Q. Explain @if, @else, @for, @include, @at-root, @extend, @error, @debug directives?
#### Q. Which directive displays an error message in SASS?
#### Q. How many output styles are there in sass?
#### Q. Which symbol is used to refer parent selector in sass?
#### Q. List out the data types that Sass supports?

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>
