# html notes:

basic outline:

```html
<!DOCTYPE html>
<head lang="en">
	<!-- metadata elements -->
	<meta charset="utf-8">
	<title>title the browser sees</title>
	<link href="style.css" rel = "stylesheet"> <!-- stylesheet link -->
	<script src="script.js"></script>
</head>
<body>
	<!-- page contents -->
	<header>header is different from head</header>
	<!-- comment -->
	<div>
		<p>divs divide things</p>
		<p><em>emphasis</em></p>
	</div>

	<ul> <!-- unordered list -->
  		<li>milk</li>
		<li>cheese</li>
	</ul>

	<ol> <!-- ordered list -->
		<li>Garfield</li>
		<li>Sylvester</li>
	</ol>

	<form action="https://freecatphotoapp.com/submit-cat-photo">
		<!-- label "for" attribute matches input "id" attribute -->
		<!-- "checked" sets item to be checked by default -->
		<label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor" value="indoor" checked> Indoor</label>
		<label for="outdoor"><input id="outdoor" type="radio" name="indoor-outdoor" value="outdoor"> Outdoor</label>
		<br>
		<label for="loving"><input id="loving" type="checkbox" name="personality" value="loving" checked> Loving</label>
		<label for="lazy"><input id="lazy" type="checkbox" name="personality" value="lazy"> Lazy</label>
		<label for="energetic"><input id="energetic" type="checkbox" name="personality" value="energetic"> Energetic</label>
		<br>
		<!-- "required" must be filled out in order to submit form-->
		<input type="text" placeholder="this is placeholder text" required>
		<button type="submit">Submit</button>
  	</form>

	<img src="http://www.linkhere.com/" alt ="screen reader text">
	<!-- "_blank" used to open link in new tab -->
	<!-- "#" used to create a dead link -->
	<a target="_blank" href="#"> link to freecodecamp.org</a>

</body>
```
# Accessibility

main, header, footer, nav, video, article, section

alt atribute is used to provide screen reader text/description of image/seo

```<img src="visualDecoration.jpeg" alt="">```

leave alt blank ```""``` for decorative images or images explined elsewhere in text



# css notes:

padding on indside of border
margin on outside of border

margin/padding can be written xx xx xx xx in clockwise pattern

css override order:
1. !important - avoid
2. inline styles
3. id attribtue
4. classes
5. elements


hex color can be shortend from 6 to 3

css variables are a thing
```css
--variable-name: color;
body{ background: var(--variable-name, fallbackcolor);}
```

```:root``` specifise root element in css/html