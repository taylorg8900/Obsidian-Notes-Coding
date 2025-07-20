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

# CSS
---
Cascading Style Sheets