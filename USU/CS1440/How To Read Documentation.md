How good documentation is organized
1. Introduction
2. Definitions
3. Examples
4. In-Depth Explanation
5. See also

built-in python documentation
- `help()` in the repl
- using `"""` triple quotes to make a paragraph comment right after the `def function():` part of a function will create documentation for it
- using a `#` comment right before defining a class or definition is also seen by the python documentation grabber thing

Software Development Plan sections in this class
1. Requirements Analylsis
	1. explain what the program is supposed to do/solve
	2. explain things like: what you know how to do, challenges that will come up, data that will be used by the program, what output will look like
2. Design
	1. explain what happens when the program works correctly, or hits errors and what the errors should be
	2. write out pseudocode
3. Implementation
	1. deliver the code
	2. note any 'interesting and relevant events'
4. Testing and Debugging
	1. create a set of test cases
	2. if bugs are discovered, describe their cause and solution
5. Deployment
	1. make sure it is pushed to a repository correctly
6. Maintenance
	1. note likely sources of headaches in the future, or areas in the documentation that are sloppy
	2. pretty much try to patch up any remaining holes so if you have to come back and are lost you can defer here for common issues that might come up

sample md formatting for sdp
```
# 1 - Requirements Analysis

# 2 - Design

# 3 - Implementation

# 4 - Testing and Debugging

# 5 - Deployment

# 6 - Maintenance
```

sample documentation for a function in python
```python
def add(x, y)
	"""
	Adds two numbers and returns the result.
	
	Parameters:
	x (int or float): The first integer
	y (int or float): The second integer
	
	Return Value:
	int or float: Two integers added together.
	"""
	return a + b
```

sample documentation for a function in java, using javadoc 'docstrings'
- always goes right before a class or function

```java
/**
 * Adds two numbers and returns the sum.
 * 
 * @param a The first number.
 * @param b The second number.
 * @return The sum of a and b.
 * 
 */ 
public int add(int a, int b) { return a + b; }
```

javadoc tags:
- `@param` describes a method parameter
- `@return` describes the return value of a method
- `@throws` describes exceptions thrown by the method
- `@author` describes the author of the class or method
- `@version` specifies the version of the class