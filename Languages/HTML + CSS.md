questions i have: 
- what is php? `<form action="/action_page.php" method="get">`
	- [focus pseudo class](https://www.w3schools.com/css/tryit.asp?filename=trycss_link_focus)
	- 
# CSS
---
Syntax
- A `rule` consists of a selector and a declaration block
	- `h1 {color: blue; font-size: 12px;}`
	- Selector {Property: Value; Property: Value;}

A `Selector` selects the HTML element you want to style
- 5 categories of CSS selectors
	- Simple Selectors                  (select elements based on name, id, class)
	- Combinator selectors          (select elements based on a specific relationship between them)
	- Psuedo-class selectors        (select elements based on a certain state)
	- Pseudo-elements selectors (select and style a part of an element)
	- Attribute selectors               (select elements based on an attribute or attribute value)
- [Simple Selectors](https://www.w3schools.com/css/css_selectors.asp)
	- element selector 
		- example: `p {text-align: center; color: red;}`
	- id selector 
		- example: `#para1 {text-align: center; color: red;}`
		- can only use ID on one html element, it is intended to select a specific element
	- CSS class selector 
		- example: `.center {text-align: center; color: red;}`
			- all HTML elements with `class="center"` will be red and center aligned
		- example: `p.center {text-align: center; color: red;}`
			- only `<p>` elements with `class="center"` will be red and center aligned
			- lets you specify that only specific HTML elements are affected by a class
		- example: `<p class="center large">This paragraph refers to two classes.</p>`
			- the `<p>` element is styled according to two classes, "center" and "large"
	- Universal selector 
		- example: `* {text-align: center; color: blue;}`
		- affects every HTML element on the page
	- Grouping selector:
		- example: `h1, h2, p {text-align: center; color: red;}`
		- groups them together, not much else to say
- Combinator Selectors
	- The only one that really makes sense to me and seems immediately useful are Child Combinators
	- Will not take notes on this because it feels a little too abstract right now
- Pseudo-class Selectors
	- What are pseudo-clases?
		- used to define a special state of an element, like when a mouse hovers over it, or if a link has been visited/unvisited
	- examples:
		- `selector:pseudo-class {property: value;}`
		- `a:link {color: #FF0000;}`
		- `a:visited {color: #00FF00;}`
		- `a:hover {color: #FF00FF;}`
		- `p {display: none; background-color: yellow; padding: 20px;}`
		- `div:hover p {display: block;}`
		- `.master:hover {background-color: red;}`
- [pseudo elements](https://www.w3schools.com/css/css_pseudo_elements.asp)
	- used to style specific parts of an element
	- "can be used to : style the first letter or line of an element, insert content before or after an element, style the markers of list items, style the viewbox behind a dialog box"
	- syntax: `selector::pseudo-element {property:value;}`
	- ::first-line
		- formats the first line of text
		- example: `p::first-line {color: #ff0000; font-variant: small-caps;}`
	- ::first-letter
		- formats the first letter of text
	- ::before
		- inserts some content before the content of an element
	- ::after
		- inserts some content after the content of an element
	- ::marker
		- styles the markers of list items
	- ::selection
		- matches the portion of an element that is selected by a user (like with their mouse or shift + arrow keys)
- [Attribute selectors](https://www.w3schools.com/css/css_attribute_selectors.asp)
	- selects elements with a specified attribute
	- example: `a[target] {background-color: yellow;}`
		- *only* `<a>` elements with the attribute target will have their color changed, like `<a href="..." target="...">website link</a>`
	- example: `a[target="_blank"] {background-color: yellow;}`
		- only `<a>` elements that have the attribute target, **and** the "\_blank" value are selected

How to add CSS
1) External CSS
2) Internal CSS
3) Inline CSS

