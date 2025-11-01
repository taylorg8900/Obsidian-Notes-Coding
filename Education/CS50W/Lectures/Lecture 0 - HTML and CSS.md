Links
- [Lecture notes](https://cs50.harvard.edu/web/notes/0)
- [W3Schools website](https://www.w3schools.com/html)

Topics
- HTML and CSS
	- HTML describes the structure of a webpage
	- CSS describes the style of a webpage
- Git
	- Version control system
- Python
- Django
	- A web programming framework written in Python, will make it easy to design web applications
	- Particularly makes it easy to design web applications that work with data
- SQL, Models, and Migrations
	- SQL lets us interact with databases
	- Django interacts with Models and Migrations to let us work with data, and let users interact with data
- JavaScript
	- User Interfaces
- Testing and CI/CD
	- Continuous Integration and Continuous Delivery
	- Testing to make sure that features are unchanged between commits or updates to our applications
- Scalability and Security
	- How do we load balance and handle many users access server at once? How do we proactively design applications to make them secure?

# HTML 
---
Hypertext Markup Language

Very simple example 

```html
<!DOCTYPE html>
<html lang="en">
	<!-- This is a comment in HTML. -->
	<head>
		<title>Hello!</title>
		<style>
		/* This is a comment in CSS. */
		</style>
	</head>
	<body>
		Hello, world!
	</body>
</html>
```

Breakdown of code snippet
- `<!DOCTYPE html>` 
	- A **DOCTYPE Declaration**, how we tell the browser which version of html we are using (which in this case, is the most recent one - html 5)
- **HTML Elements**
	- Indicated by an **HTML Tag**, enclosed in angle brackets
	- `<head>`
		- Describes things not in the main body of the page, but information about the page that is helpful for the browser itself to know about
	- `<title>`
		- The title of the webpage, what shows up at the top of your browser
	- `<body>`
		- The body of the page, that is visible to the user
- **HTML Attributes**
	- Additional information that we are giving about a tag
	- Example: `<html lang="en">`

**Document Object Model**
- A way to describe HTML code by creating a tree like model to show how elements are related to each other
- Parent elements and child elements

## Common HTML elements

Elements 
- **Headings**
	- `<h1>`
		- Creates a large heading
	- `<h2>` - `<h6>`
		- Is smaller than `<h1>`
		- Continues this pattern down to `<h6>`
- Text formatting
	- `<strong>bold</strong>` creates bold text
	- `<i>italicized</i>` creates italicized words
- **Lists**
	- **Ordered Lists**
		- Numbers to denote an order, browser automatically creates the numbers for items within the body of `<ol>`
		- `<ol>`
	- **Unordered Lists**
		- Such as bullet points
		- `<ul>`
	- **List Item**
		- Put these within the List elements
		- `<li>First Item</li>
- **Images**
	- **Image Tag**
		- `<img src="cat.jpg" alt="Cat">`
		- Required attributes
			- Need to specify which image to display with `src=""`, and a path or file name within the quotes
			- Need to provide alternative text with `alt=""` in case the browser is not able to display the image, or if blind people are using our side
		- Additional attributes
			- `width="300"` 
				- `"300"` denotes pixel width, automatically adjusts height
		- Does not require a closing HTML tag
- **External Links**
	- **Anchor Tag**
		- `<a href="https://google.com">This link takes you to google.</a>`
	- **href Attribute**
		- `href=""`
		- Can take you to external sites and pages, or other pages internally
- **Tables**
	- **Table Tag**
		- `<table>`
		- First HTML tag used to create a table, everything else gets nested inside of this
	- **Table Header**
		- `<thead>` 
		- First row of the table
		- Use `<th>` tags inside here, to put in text that goes into each cell of the header
	- **Table Headings**
		- `<th>`
		- Text that appears in the cells of the table header
	- **Table Body**
		- `<tbody>`
		- The main part of our table
		- Put `<tr>` tags inside here, to create each row
	- **Table Row**
		- `<tr>`
	- **Table Data**
		- `<td>`
		- Any text that belongs in each cell of the table (just not the header cells)
- **Forms**
	- **Form Tag**
		- `<form>`
	- **Input Field**
		- `<input type="text" placeholder="Full Name" name="full_name">`
		- Attributes
			- `name=""` gives us some way of knowing which input field gave us information
			- `type=""` tells the browser what kind of information the user will be able to input
				- `type="submit"`
					- Another option which can be used for interactivity, which we will learn about later
				- `type="password"` 
					- Makesinput text turn into dots
				- `type="radio"`
					- User can select between a number of options
					- Like for multiple choice questions on tests
			- `list="countries"`
				- This is a newer attribute for Input Fields in HTML, where we can associate a `<datalist id="countries">` and provide a dropdown for users to click on and select a specific option
				- The user can also start typing to find certain options faster with this
				- For `<datalist>` to do anything we need an option element like `<option value="Argentina">` 
- **Divisions**
	- `<div>` 
	- How we create sections which contain certain things
- **Buttons**
	- `<button>`
	- `<button>Click Me</button>`
- Line break
	- `<br>` creates a line break, which just moves the next element or text to a new line
	- 'Empty element', meaning that it doesn't need a closing tag - '`<br>`' is just used on its own

# CSS
---
Cascading Style Sheets

Inline Styling
- We can give individual elements a CSS property, such as the color or alignment of the element, with `style="color: blue;"` for example
- If we apply a CSS property to an HTML element with children elements, it will apply to every child element

Common CSS properties
- `"color: blue;"`
- `"text-align: center;"`
- `background-color: blue;`
	- Used with `<div>`

Moving style related code into `<head>`
```html
<head>
	<title>Hello!</title>
	<style>
		h1 {
			color: blue;
			text-align: center;
		}
	</style>
</head>
```


### Linking to an external CSS file
`<link rel="stylesheet" href="styles.css">`
- Include this within `<head>`, on its own without a style tag anywhere 

# Common CSS styles

List of stuff
- **Size**
	- `div { width: 100px; height: 400px; }`
- **Padding**
	- `div { padding: 20px; }`
	- Makes other elements not so close to the edge, applies to the 'inside' of a thing
- **Margin**
	- `div { margin: 20px; }`
	- Applies to the 'outside' of an element
- **Font**
	- `div { font-family: Arial, sans-serif; }`
	- `div {font-size: 28px; font-weight: bold; }`
	- You can specifiy a 'back-up' option with by including multiple fonts like above
- **Border**
	- `div {border: 3px solid black; }`
	- `table {border-collapse: collapse; }`
		- This will remove the white space in between table elements where there is a border
- **Flex**
	- `display: flex;`
	- `flex-wrap: wrap;`

# CSS Selectors

**Multiple Element Selector**
- You can have a style apply to multiple HTML elements by having them together
	- `td, th { border: 1px solid black; }`

**Element IDs**
- Lets us reference it to apply a style
	1. `<h1 id="foo">Heading 1</h1>` 
	2. `<style> #foo { color: blue; } </style>`

**Classes**
- Lets us assign this class to any specific HTML elements we want, avoids duplicated code and inline code
	1. `<h1 class="baz">Heading1</h1>` 
	2. `<style> .baz { color: blue; } </style>`

# Styling Priority
A problem we face is that we can assign a style to an HTML element in many different ways. What if we have a specific style apply to all `h1` elements, but then we grab a specific one and assign a class to it? How does the language know which style to give to it?

Specificity (Priority)
- Inline styling > ID > Classes > Type
- Inline is most specific, and Type is least specific

# CSS Selectors
Here are some of the ways you can be really specific about CSS styling
- Multiple Element Selector
	- `a, b`
- Descendant Selector
	- `a b`
	- Used to select *all* `b` elements which are 'descendants' of `a`, whether or not they are immediate
- Child Selector
	- `a > b`
- Adjacent Sibling Selector
	- `a + b`
- Attribute Selector
	- `[a=b]`
		- `a[href="https://facebook.com"] { color: red; }`
			- Anchor elements with this attribute should be colored red
- Pseudoclass Selector
	- `a:b`
		- `button:hover { background-color: orange; }`
			- When you hover over a button, it turns orange
- Pseudoelement Selector
	- `a::b`

# Responsive Design

Add this line to the `head` section of our page to make the viewport just the width of the device, makes it look better on mobile
- `<meta name="viewport" content="width=device-width, intial-scale=1.0">`

## Media Queries
- Ways of changing the style of a page based on how the page is being viewed
- You signal a media query by typing `@media`, followed by the type of query in parentheses

```html
<!-- This turns the background color to red if the width of page is more than 600 pixels, and blue if it is less than 599 pixels -->
<head>
	<style>
		@media (min-width: 600px) {
			body {
				background-color: red;	
			}
		}
		@media (max-width: 599px) {
			body {
				background-color: blue;
			}
		}
	</style>
</head>
```

## Flexbox
This lets elements wrap around the screen dynamically, ensuring that any elements look good on different sized screens
```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Hello!</title>
		<style>
			#container {
				display: flex;
				flex-wrap: wrap;
			}
			
			#container > div {
				background-color: springgreen;
				font-size: 20px;
				margin: 20px;
				padding: 20px;
				width: 200px;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<div>1. This is sample text.</div>
			<div>2. This is sample text.</div>
			<div>3. This is sample text.</div>
			<div>4. This is sample text.</div>
			<div>5. This is sample text.</div>
		</div>
	</body>
</html>
```

## Grid
```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Hello!</title>
		<style>
			#grid {
				background-color: green;
				display: grid;
				padding: 20px;
				/* How much space goes between the columns and rows in our grid. */
				grid-column-gap: 20px;
				grid-row-gap: 10px;
				/* Specifies how many columns there will be, and how wide they are. 'auto' lets it decide automatically. */
				grid-template-columns: 200px 200px auto;
			}
			
			.grid-item {
				background-color: white;
				font-size: 20px;
				padding: 20px;
				text-align: center;
			}
		</style>
	</head>
	<body>
		<div id="grid">
			<div class-"grid-item">1</div>
			<div class-"grid-item">2</div>
			<div class-"grid-item">3</div>
			<div class-"grid-item">4</div>
			<div class-"grid-item">5</div>
	</body>
</html>
```

# Bootstrap
---
A popular library full of CSS styling, so that we don't need to create our own.
- [getboostrap.com](https://getbootstrap.com)
- [Bootstrap's Docs](https://getbootstrap.com/docs/5.3/getting-started/introduction)

Bootstrap's Column Model
- A way to ensure that pages built with it are mobile responsive. Each page is divided into 12 columns, and we can decide how to use that space depending on what kind of screen the content is displayed on
- [Column Docs](https://getbootstrap.com/docs/5.3/layout/columns/#how-they-work)
- `<div class="col-3"> A section that is 3 units long, out of a maximum of 12 units. </div>`
	- Contained within a `<div class="row"></div>`
- `<div class="col-lg-3 col-sm-6">A section that is 3 units on large screens, and 6 units on small screens.</div>`

# SASS
---
Basically an extension to CSS
- Filename extension for this would be something like `variables.scss`, instead of the usual `variables.css`

Features of SASS
- Variables
- Nesting CSS elements instead of using native CSS selectors
- Inheritance

CSS doesn't support variables, but SASS does
```scss
// This is a comment in scss

// All variables begin with a '$'
// This creates a variable named color, that is equal to 'red'
$color: red;

ul {
	font-size:14px;
	color: $color;
}

ol {
	font-size: 18px;
	color: $color;
}
```

We need to convert scss into css so that web browsers can understand it. Attempting to link the above code snippet would not actually work the same as linking a css file.

How to compile scss into css
- Install a program named SASS onto your computer
- **Manually**
	- In the terminal, run `sass variables.scss:variables.css`
		- `sass [File to be compiled]:[File to be generated]`
- **Automatically**
	- In the terminal, run `sass --watch variables.scss:variables.css`

SASS also allows nesting of CSS elements, rather than using very specific selectors