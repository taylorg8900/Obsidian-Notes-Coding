comments
- `<!--This is comment, with weird syntax-->`

tags
- \<body> 
	- contains all of the contents of the HTML document
	- can only be one per document
- \<p>
- \<head>
	- container for metadata, between \<html> and \<body> tag
	- these elements go inside of it: 
		- \<title>
		- \<meta>
		- \<link>
			- `<link rel="stylesheet" href="style.css">`
		- \<style>
			- Internal CSS
- \<title>
	- defines title of document, required, important for search engine optimization
	- provides title when it is added as bookmark
- \<meta> 
	- defines metadata about the HTML document
	- stuff that is searched with search engines and web services etc
- \<link>
	- links to a external style sheet

- \<a> 
	- defines a hyperlink
	- 'href' attribute
- \<img>
	- embeds an image in the page
	- required attributes: scr, alt
- \<ul>
	- unordered list
	- each list item starts with the \<li> tag
- \<ol>
	- ordered list
	- each list item starts with the \<li> tag

# CSS
- comments
	- example: `/* This is a single line comment*/`
### classes
how to make them
- preface with a dot: `.city { .... }`
how to access in HTML
- `<div class="city">`

properties
- float
	- `float: left;`
	- makes elements 'float' to the left in it's container, so it can dynamically move around in relation to other things in the container
- div
	- easily styled by using class or id attributes
	- container for HTML elemnts which are then styled by CSS or javascript
- background-color
	- background color of an element
- color
	- text color
- font-family
	- text fonts
- font-size
	- text sizes
- border
	- borders
	- `p {border: 1px solid yellow;}`
- padding
	- space inside border
- margin
	- space outside border
	- `margin-top: 100px;`
	- can have top, bottom, right, left
- 