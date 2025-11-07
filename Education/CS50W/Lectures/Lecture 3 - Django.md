***Django*** is a Python web framework that lets us dynamically generate HTML and CSS to create web applications. A Django project consists of multiple Django applications, each one providing a specific service. It is powerful because of its ability to be used to store and retrieve information from databases in particular.

***HTTP*** stands for Hypertext Transfer Protocol, which is how information is sent between clients and servers
- Consists of requests, and responses in the form of status codes. An example is 200 meaning OK, 301 means moved permanently, 404 means not found, 500 means internal server error

How to install Django:
- `pip3 install Django`

Command to start a Django project:
- `django-admin startproject [project name]`
- This will automatically generate some starter files for us to get started on building a web application
	- We will use `manage.py` to execute commands on our project
		- An example of this is `python manage.py runserver`
	- `settings.py` contains important configuration settings
	- `urls.py` is sort of a table of contents for the URLs inside of our website/project

## Creating Django Applications

Creating a Django App
- `python manage.py startapp [new application name]`

Adding a Django App to our project
- Inside of `settings.py`, there is a list named `INSTALLED_APPS` where we need to add whatever our new applications name is to.o

`views.py` example:
```python
# views.py inside of our new Django App named "hello"

from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def index(request):
	# HttpResponse is a special class created by Django that we need to import
	return HttpResponse("Hello, world!")

def brian(request):
	return HttpResponse("Hello, Brian!")
```

`urls.py` example:
```python
# urls.py inside of our new Django App named "hello"

from django.urls import path
# `.` means current directory
from . import views

# urlpatterns is a list of all allowable urls for this application 
urlpatterns = [
	# When someone visits the default route (which is the "", and the url on our machine might look like 127.0.0.1:8000/hello/), run the index function from views.py
	# When someone visits 127.0.0.1:8000/hello/brian, call views.brian instead
	path("", views.index, name="index")
	path("brian", views.brian, name="brian")
] 
```

To get our new application running, we need to change `urls.py` inside of our original folder; this is where all of our applications are being kept track of, and not putting it in here means that we can't access any new apps we make
```python
# Add 'include' to this statement so we can use it
from django.urls import include, path

# Adding to the existing `urlpatterns` list in this file
urlpatterns = [
	# admin is the default Django application, which we will see more of in the next lecture
	# We are basically adding all of the urls inside of 'hello' here on one line
	path('admin/', admin.site.urls),
	path('hello/', include("hello.urls"))
]
```

#### Using a placeholder to reduce duplicated code

We are going to implement a function in `hello/views.py` and a placeholder inside of `hello/urls.py` like this:
```python
# -----
# Inside views.py
def greet(request, name):
	return HttpResponse(f"Hello, {name.capitalize()}!")
# -----

# -----
# Inside hello/urls.py
urlpatterns = [
	path("", views.index, name="index"),
	path("<str:name>", views.greet, name="greet")
]
# -----
```


Even though using a placeholder cuts down on duplicated code, the way we are using Django so far to have an `HttpResponse` only show us a page with text will very quickly become difficult to use if we want to have a lot of text or other things such as images. There is a way to have Django utilize entire HTML pages as templates instead using the built in `render()` function
```python
# Inside of hello/views.py
def greet(request, name):
	# Third argument is optional, called the 'context', which is all of the information/variables that we want to provide to the template
	return render(request, "hello/greet.html", {
		"name": name.capitalize()
	})
```

We also need the HTML file that is going to be used, called `hello/greet.html`. The way that Django can identify which things to modify in the HTML file is by encasing variable names with two curly braces, like `{{ name }}`. Also, the lecturer puts this HTML file inside of `hello/templates/hello/greet.html`
```html
<!-- hello/greet.html -->
<!DOCTYPE html>
<html lang="en">
	<!-- This is a comment in HTML. -->
	<head>
		<title>Hello!</title>
	</head>
	<body>
		<h1>Hello, {{ name }}!</h1>
	</body>
</html>
```

We can use standard python code to create conditionals to dynamically change the content of our site. The following example checks to see if it is New Years Day
```python
# Inside a new app, with the path being called newyear/views.py
import datetime
from django.shortcuts import render

def index(request):
	now = datetime.datetime.now()
	return render(request, "newyear/index.html", {
		"newyear": now.month == 1 and now.day == 1
	})
```

And now we can see what the syntax for conditionals are in Django. Our HTML file will use `{% %}`, with logic inbetween the percent signs. You need to include `{% endif %}` at the end, so that it knows that the logic block has ended. The interesting thing is that if you check out the page in the browser, all of the conditional logic doesn't even show up, it only shows `<h1>NO</h1>`.
```html
<!-- more on this underneath this example -->
{% load static %}

<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Is it New Year's?</title>
		<link href="{% static 'newyear/styles.css' %}" rel="stylesheet">
	</head>

	<body>
		{% if newyear %}
			<h1>YES</h1>
		{% else %}
			<h1>NO</h1>
		{% endif %}
	</body>
```

#### Creating CSS files with Django
Django considers CSS files to be static, because they don't dynamically change like some of our pages can. The convention is to have a folder/file such as `[app name]/static/[app name]/styles.css`

### Template Inheritance

First, create a layout file that can be inherited by other HTML files later, such as;
```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Hello!</title>
	</head>
	<body>
		{% block body %}
		{% endblock %}
	</body>
</html>
```

What is contained inside of the files that inherit from our layout file is whatever goes inside of the block above.
```html
{% extends "tasks/layout.html" %}

{% block body %}
	<h1>Tasks</h1>
	<ul>
		{% for task in tasks %}	
			<li>{{ task }}</li>
		{% endfor %}
	</ul>
{% endblock %}
```

### Adding links between pages

Bad design: `<a href="/tasks/add">Link</a>`
- Bad design because we are hardcoding a file path to get to another page. If we wanted to change this in the future, we would have to edit it in two places

Good design: `<a href="{% url 'add' %}">Link</a>`
- This takes advantage of the `name="add"` that we included inside of our `urls.py` file. Even if we changed the name of the file itself, since this relationship exists, we can avoid having to change the name in multiple places.

We want to avoid the situation where multiple apps all have the same 'add' url, so that we only link to the exact page that we really want. To do this, we can do this:
1. Inside of our app's `urls.py` file, add the line `app_name = "[app name]"`
	- I'd have to read the documentation to know how this actually does anything, but just trust that it works I guess
2. Make the line in our html file look like `<a href="{% url '[app name]:add' %}">Link</a>` instead

### Using Forms to submit data
`<form action="{% url 'tasks:add' %}" method="post">`
- We are used to seeing `method="get"`, which means "I would like to get a particular page"
- `method="post"` is used anytime we are submitting data that can change some kind of state in a page, lets us send data

![[2025.11.5 csrf error.PNG]]

CSRF stands for Cross Site Request Forgery, and it's a security vulnerability if it's not designed properly. We can implement some kind of CSRF token into our forms and check to make sure it's coming from the user who is actually on our page.
- Django Middleware is the add-on that solves this, and you can see a bunch of it inside of the `settings.py` file

Here is how to fix this problem:
```html
{% block body %}
	<form action="{% url 'tasks:add' %}" method="post">
		{% csrf_token %} <!-- This is the important part, add this in here-->
		<input type="text" name="task">
		<input type="submit">
	</form>
{% endblock %}
```
This will generate a `input type="hidden"` tag with a huge token attached to it when anyone visits the page

## Creating forms with Django - Alternative method

```python
# Inside of tasks/views.py

# Django's library for creating forms inside of python and not html, much easier to work with
from django import forms
# Functions we use to redirect the user
from django.http import HttpResponseRedirect
from django.urls import reverse

# Library we already had in here
from django.shortcuts import render

tasks = ["foo", "bar", "baz"]

# We inherit from forms.Form so that we can use this class to generate forms in our html instead of making them manually
class NewTaskForm(forms.Form):
	task = forms.CharField(label="New Task")
	# You can add additional fields, for example an IntegerField
	priority = forms.IntegerField(label="Priority", min_value=1, max_value=5)

# We are going to move the tasks list in here, so that we can have sessions for each user
def index(request):
	if "tasks" not in request.session:
		request.session["tasks"] = []
	
	return render(request, "tasks/index.html", {
		"tasks": request.session["tasks"]
	})

# We can add context with the third argument here to be passed to our html, and pass in a NewTaskForm. Django will automatically generate a form, so we can have '{{ form }}' in our html code instead of doing it all manually
def add(request):
	if request.method == "POST":
		# request.POST contains all of the data the user submits
		form = NewTaskForm(request.POST)
		if form.is_valid():
			task = form.cleaned_data["task"]
			request.session["tasks"] += [task]
			# We are redirecting a user with this 
			# reverse is a function built in to Django that will figure out the url to send the user to
			return HttpResponseRedirect(reverse("tasks:index"))
		else:
			# Send back the existing form data, instead of generating a new form. This is so the user can see where what they typed in went wrong
			return render(request, "tasks/add.html", {
				"form": form
			})
	return render(request, "tasks/add.html", {
		"form": NewTaskForm()
	})
```

## Tables

Django stores information inside of 'tables', including sessions

`python manage.py migrate` will allow us to create default tables that we need, but explanations for how this works comes later

