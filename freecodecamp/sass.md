# variables
In Sass, variables start with a `$` followed by the variable name.
```css
$main-fonts: Arial, sans-serif;
$headings-color: green;

And to use the variables:

h1 {
  font-family: $main-fonts;
  color: $headings-color;
}
```

# nesting
Normally, each element is targeted on a different line to style it, like so:
```scss
nav {
  background-color: red;
}

nav ul {
  list-style: none;
}

nav ul li {
  display: inline-block;
}
```
For a large project, the CSS file will have many lines and rules. This is where nesting can help organize your code by placing child style rules within the respective parent elements:
```scss
nav {
  background-color: red;

  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }
}
```

# Mixins
In Sass, a mixin is a group of CSS declarations that can be reused throughout the style sheet.

Mixins are like functions for CSS.

useful for vendor prefix rules
```scss
@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}

div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
```
A mixin is called with the `@include` directive

# @if and @else
The `@if` directive in Sass is useful to test for a specific case - it works just like the `if` statement in JavaScript.
```scss
@mixin text-effect($val) {
  @if $val == danger {
    color: red;
  }
  @else if $val == alert {
    color: yellow;
  }
  @else if $val == success {
    color: green;
  }
  @else {
    color: black;
  }
}
```

# @for
The `@for` directive adds styles in a loop, very similar to a `for` loop in JavaScript.

`@for` is used in two ways: "start through end" or "start to end". The main difference is that the "start to end" excludes the end number as part of the count, and "start through end" includes the end number as part of the count.
```scss 
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}

// produces:

.col-1 {
  width: 8.33333%;
}

.col-2 {
  width: 16.66667%;
}

...

.col-12 {
  width: 100%;
}
```

# @each

Sass also offers the `@each` directive which loops over each item in a list or map. On each iteration, the variable gets assigned to the current value from the list or map.
```scss
@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}

// maps work like:

$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
```
Note that the `$key` variable is needed to reference the keys in the map. Otherwise, the compiled CSS would have `color1`, `color2`... in it. Both of the above code examples are converted into the following CSS:
```css
.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}
```
# @while
The `@while` directive is an option with similar functionality to the JavaScript `while` loop. It creates CSS rules until a condition is met.
```scss
$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}
```

# Partials

*Partials* in Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized.

Names for partials start with the underscore (`_`) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the `.scss` file extension. To bring the code in the partial into another Sass file, use the `@import` directive.

For example, if all your mixins are saved in a partial named `"_mixins.scss"`, and they are needed in the `"main.scss"` file, this is how to use them in the main file:
```scss
@import 'mixins'
```
Note that the underscore and file extension are not needed in the import statement

# extend
Sass has a feature called `extend` that makes it easy to borrow the CSS rules from one element and build upon them in another.

```scss
.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}

.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
```

The .big-panel will have the same properties as .panel in addition to the new styles.
> idk this is kinda silly, just implement two classes