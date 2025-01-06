How does the internet work?
	like plumbing but with wires and the toilets are computers
	started with ARPANET, between universities
	#term routers
		computers, servers which route information from one point to another
		the software they use lets them route information between other computers
		what language do they speak in?
		#term TCP/IP
			technically a 'protocol'
		IP
			Internet Protocol
				a set of conventions
				every computer in the world has an IP address, which looks like #.#.#.# and each hash can be between 0 and 255, which means that it can be stored in 4 bytes, which is 4 billion possible addresses (ipv4)
			Steps to using IP
				first write an address and have another one which is the sender/source address
				apparently thats all you need baby, and passing the 'evelope' between many routers which are closer and closer to the target address (this must be extremely dumbed down lol)
				apparently it only takes about 30 hops between routers to get to where it needs to go
			Fragmentation
				for large files, they get split up and sent separately
				you now need info on the order in which the data got separated, along with source and destination addresses
				use TCP for this, as it is a different protocol
		TCP
			Transmission Control Protocol
			keeps track of sequence numbers between fragments of data
			uses	#term ports
				A unique numeric identifier for a specific internet service
				decided by convention
				http is an integer 80, so now accessing a web server looks like calling the address #.#.#.#:80
				Allows servers to distinguish which type of service should be handling the request
		tldr of TCP/IP
			Allows us to uniquely address computers on the internet by using IP addresses, and to guarantee delivery of information between 2 points by using sequence numbers (for fragments) and port numbers (for type of service)
	DNS
		Domain Name System servers
		translates domain names to IP addresses so users can type friendly names and they get turned into IP addresses
		domain name -> IP Address
			having a sort of dictionary containing every possible domain name is kind of crazy but it's alright because it is stored inside of a server somewhere that internet service providers own
		#term root server
			small number of servers around the world that keep information about all of the .orgs and .coms etc
		#term caching
			storing the IP address of the domain on your device so you aren't just querying the DNS servers all the time
		Expiration dates
			not really elaborated on, but implying something about keeping the IP address for your domain for a long time is bad somehow
			I asked cs50.ai about it and here's what i got:
				you would want to change what is stored in the DNS server frequently because you might choose to migrate your server, load balance traffic across multiple servers, add subdomains, update security, etc and if the expiration date is very long then you wouldn't be able to change anything for a long time
	DHCP
		Dynamic Host Configuration Protocol
		gives your computer an IP address when it starts, a lot more scalable than manually deciding what your address is when you first plug in a family computer like back in the ancient times like probably the 90's
		Also tells your computer which DNS servers to use
		Also tells your computer which local gateway you use (your router in your house, neat)
	HTTP
		Hypertext transfer protocol
		how web browsers and web servers communicate
	HTTPS
		same thing but encrypts information
		GET
			used by a browser when it wants information
		POST
			used by a browser when it wants to send information
HTML
	new command to use in cs50.dev to start our very own web server on port 8080, on the server that is handling our codespaces via github
			http-server
	tags
		\<head>
		\<body>
		\<p> means paragraph
		\<h1> \<h2> \<h3> different headings with stylized size and boldness
		\<ul> means unordered list, a bulleted list (no numbers)
		\<ol> means ordered list, has numbers
		\<li> 'list item'
		\<table> table
		\<tr> table row
		\<td> table data, like a cell
		\<img> image
			doesnt have a close tag, which i guess doesn't need because it has null value  at the end anyway
		\<video>
		\<source>
			inside video tag
			\<source src="video.mp4" type="video/mp4"> 
		\<a> anchor
			this is how we use hyperlinks
			\<a href="image.html">Harvard\</a>
		---dynamic stuff---
		\<form>
		\<input>
		\<button>
		---css stuff---
		\<style>
		\<link>
	attributes
		lang=
			\<html lang="en">
		src=
			\<img src="image.png">
		alt=
			\<img alt="Harvard University" src="bridge.png">
				provide alternate info in case src can't be displayed, or for accessibility for things like blind people
		controls
			i guess a play button pause button etc
			does not need values/ an equal sign
		muted
			mute audio by default
		type=
			type="video/mp4"
			type="search"
			type="submit"
			type="email"
		value=
			value="Google Search"
		href=
			hyperreference, destination for a link
		name=
		method=
		action=
		autocomplete=
		autofocus
		placeholder=
			can hold temporary text
		pattern=
			where regular expressions are
	comments
		\<!-- 'type comment in here' -->
	dynamic websites
		at the end of the url, you can have other things and not just folders or files
			?key=value
	regular expressions
		a pattern #term (regex) that allows you to validate input from users and make sure it matches some pattern
		as of now, creating our own is never going to be good enough to stop users from fucking things up because they can still do 'select element' and change their client side version of the web page to submit information, so we need a server side mechanism to protect from that sort of thing too
	[validator.w3.org](https://validator.w3.org/)
		web based tool that provides feedback for if you've made syntactic errors with html code
	HTML entities
		how to type special characters that aren't on your keyboard, like copyright symbol
		example - &#169
CSS
	Cascading Style Sheets
	lets you specify how certain tags show up on the screen
	#term properties
		sets of key-value pairs, like saying color of this thing equals blue
	How do we select which elements we want to do things with?
		type selector
		class selector
		ID selector
		attribute selector
		...
		\<style>
			\<p style="font-size: large; text=align: center;">
		\<link>
			allows you to link in the contents of a .css file which contains properties separately
			\<link href="styles.css" rel="stylesheet">
		\<div>
			means 'division', or region of the page	
			this is why clicking and dragging seemingly empty areas of some webpages selects entire regions
		\<header>
		\<main>
		\<footer>
	Selection by type
		selecting by type example
			body {
				text-align: center;
			}
		second example
			a {
				color: red;
				text-decoration: none;
			}
		third example
			a:hover {
				text-decoration: underline;
			}
		#important you can see different css properties if you go to inspect in the page and go to the right (after beingin the elements tab) and click styles and mess with the css code inside the browsers memory, for instance deleting 'center' in the example above will give you a drop down with a ton of different also valid options for which to text-align
	Selection by class
		keywords we can create and associate our own properties with
		example of creating a class
			.centered {
				text-align: center;
			}
			\<header class="centered">
	Selection by ID
		creating a unique identifier that lets you target it with CSS
		example
			\#harvard {
				color: \#FF0000;
			}
			\#yale {
				color: \#0000FF;
			}
			Visit \<a href="https://www.harvard.edu/" id="harvard">Harvard\</a>
Frameworks
	a library written by someone else to make it easier to structure your project so you don't have to implement basics that other people would have already dealt with before
	#term Bootstrap
		Very popular and widely used framework
		[getbootstrap.com](https://getbootstrap.com/) documentation
Javascript
	
		