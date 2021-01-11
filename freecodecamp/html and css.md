# html notes:

basic outline:

```html
<!DOCTYPE html>
<head lang="en">
	<meta charset="utf-8">
	<title>title the browser sees</title>
	<link href="style.css" rel = "stylesheet">
	<script src="script.js"></script>
</head>
<body>
	<header>header is different from head</header>
	<!-- comment -->
	<div>
	<p>divs divide things</p>
	<p><em>emphasis</em></p>
	</div>
</body>
```


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