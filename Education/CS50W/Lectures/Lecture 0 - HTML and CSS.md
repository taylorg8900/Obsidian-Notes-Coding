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
	<head>
		<title>Hello!</title>
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

# Common HTML elements

Elements 
- **Headings**
	- `<h1>`
		- Creates a large heading
	- `<h2>` - `<h6>`
		- Is smaller than `<h1>`
		- Continues this pattern down to `<h6>`
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
	- **Table Header**
		- `<thead>` 
		- First row of the table
		- Put `<th>` tags inside here, and make sure to use `<tr>` tags to accomplish this
	- **Table Headings**
		- `<th>`
		- Each column of the table is described by this
	- **Table Body**
		- `<tbody>`
		- The main part of our table
		- Put `<tr>` tags inside here
	- **Table Row**
		- `<tr>`
	- **Table Data**
		- `<td>`
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

How do we make it so that a specific style is available to multiple pages at once?
- By moving it to another file, specifically a `.css` file
- Link the `.css` file to a `.html` page inside the `<head>` element with a `<link rel="stylesheet" href"styles.css">`, where the `href""` contains the name of a file with our styling

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

**Multiple Element Selector**
- You can have a style apply to multiple HTML elements by having them together
	- `td, th { border: 1px solid black; }`

**Element IDs**
- Lets us reference it to apply a style
- `<h1 id="foo">Heading 1</h1>` and then `<style> #foo { color: blue; } </style>`

**Classes**
- `<h1 class="baz">Heading1</h1>` and then `<style> .baz { color: blue; } </style>`
- Lets us assign this class to any specific HTML elements we want, avoids duplicated code and inline code

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
- Child Selector
	- `a > b`
- Adjacent Sibling Selector
	- `a + b`