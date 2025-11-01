Just like with the previous lecture, I will only include notes that I don't already know from CS1400.

***Sets*** are collections of data that are unordered, where each value is only contained once. You create them with `set()` 

***Decorators*** take an existing function and add capabilities to it. I'm not really sure how useful these are compared to just calling a function from within another, but here is the example given:
```python
def announce(f):
	def wrapper():
		print("About to run the function...")
		f()
		print("Done with the function.")
	return wrapper

@announce #This is how you attach the decorator to a function
def hello():
	print("Hello, world!")

hello()

# This will run the `hello()` function as `f()` in `announce()`
```

Apparently these are useful for things like adding functionality only when a user is logged in to a website

***Lambdas*** are ways to express short functions on one line, so you don't need to write an entire function for something simple
```python
people = [
	{"name": "Harry", "house": "Gryffindor"},
	{"name": "Cho", "house": "Ravenclaw"},
	{"name": "Draco", "house": "Slytherin"}
]

people.sort(key=lambda person: person["name"])
```