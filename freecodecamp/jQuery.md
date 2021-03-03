```javascript
$(document).ready(funciton() {
  // code runs as soon as browser loads the page
});
```
without `document ready function`, code may run before HTML is rendered, which would cause bugs.

all jQuery functions start with `$` a bling or dollarsign

you can find html elements using css style declarations
```javascript
$(document).ready(function() {
  $("button").addClass("animated bounce"); // finds 'button' elements
  $(".well").addClass("animated shake"); // finds 'well' class
  $("#target3").addClass("animated fadeOut"); // finds 'target3' id
});
```

`.removeClass()` can remove a class

`.css(ar1,ar2)` can change an element's css
```javascript
$("#target1").css("color", "blue");
```
`.prop()` can adjust the properties of elements.
```javascript
$("button").prop("disabled", true); // disables all buttons
```
`.html()` lets you add HTML tags and text within an element.
```javascript
$("h3").html("<em>jQuery Playground</em>");
```
`.remove()` removes an HTML element entirely

`.appendTo()` that allows you to select HTML elements and append them to another element.

`.clone()` makes a copy of an element.
```javascript
$("#target5").clone().appendTo("#left-well");
```
`.parent()` accesses an element's parent
```javascript
$("#left-well").parent().css("background-color", "blue")
```
`.children()` accesses all of the children of an element

`target:nth-child(n)` CSS selector allows you to select all the nth elements with the target class or element type.
```javascript
$(".target:nth-child(2)").addClass("animated bounce");
// adds classes to .target class that is also the 2nd child of an element
```
jQuerey is zero indexed? what? yeah idk how that last script worked correctlty then

`:even` and `:odd` selectors let you select even and odd elements
```javascript
$(".target:even").addClass("animated shake");
// again, zero based, so 0, 2, 4
```
`body` targets the body element
```javascript
$("body").addClass("animated fadeOut");
```