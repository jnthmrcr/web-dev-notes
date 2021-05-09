add this to add bootstrap to a project
```javascript
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/>
```

bootstrap includes css classes you can apply to tags:

```container-fluid``` does stuff?

```img-responsive``` scales image with container

```text-center``` centered text
# buttons

`btn` ```btn-default``` makes a button

`btn-block` your button will stretch to fill your page's entire horizontal space and any elements following it will flow onto a "new line" below the block.

`btn-primary` class is the main color you'll use in your app. It is useful for highlighting actions you want your user to take. (replaces `btn-default`?)

`btn-info` class is used to call attention to optional actions that the user can take.

`btn-danger` class is the button color you'll use to notify users that the button performs a destructive action, such as deleting a cat photo.

# columns

Bootstrap uses a responsive 12-column grid system, which makes it easy to put elements into rows and specify each element's relative width. Most of Bootstrap's classes can be applied to a `div` element.

`col-md-*` class. Here, `md` means medium, and `*` is a number specifying how many columns wide the element should be. In this case, the column width of an element on a medium-sized screen, such as a laptop, is being specified.

`col-xs-*`, where `xs` means extra small (like an extra-small mobile phone screen), and `*` is the number of columns specifying how many columns wide the element should be

`row` makes things a row?

`text-primary` colors text the primary color

`text-danger` colors text the danger color

`span` elements let you style stuff on the same line
```html
<p>Things cats <span class="text-danger">love:</span></p>
```
# font awesome
Font Awesome is a convenient library of icons. You can include Font Awesome in any app by adding the following code to the top of your HTML:
```html
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css" integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous">
```

The `i` element was originally used to make other elements italic, but is now commonly used for icons. You can add the Font Awesome classes to the `i` element to turn it into an icon, for example:
```html
<i class="fa fa-info-circle"></i>
```
Note that the `span` element is also acceptable for use with icons.

first add `fa` class.

`fa-thumbs-up` for thumps up

`info-circle` for i circle thing

`trash` for trashcan

`fa-paper-plane` for a paper plane thing

can use `col-xs-*` on `forms`

`form-control` on text input to make it different idk

>All textual `<input>`, `<textarea>`, and `<select>` elements with the class .form-control have a width of 100%.

Bootstrap has a class called `well` that can create a visual sense of depth for your columns.