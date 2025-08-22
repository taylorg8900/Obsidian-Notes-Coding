```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Hello!</title>
	</head>
	<body>
		Hello, world!
	</body>
</html>
```


Example of Child CSS Selector
```html
<!-- The li elements which are immediate children of ul are colored blue -->
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Hello!</title>
		<style>
			ul > li {
				color: blue;
			}
		</style>
	</head>
	<body>
		<ol>
			<li>list item one</li>
			<li>list item two</li>
			<ul>
				<li>sublist item one</li>
				<li>sublist item two</li>
			</ul>
			<li>another list item</li>
		</ol>
	</body>
</html>
```
