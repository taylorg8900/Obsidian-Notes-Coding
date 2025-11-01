How to install Django:
- `pip3 install Django`

Commands
- Start a Django project: `django-admin startproject [project name]`
- Run a server on your machine: `python manage.py runserver`

Creating a Django App
1. `python manage.py startapp [new application name]`
2. In `[main directory]/settings.py`, add `[new application name]` to the list variable `INSTALLED_APPS` 
3. In `[main directory]/urls.py`, add `path('[new app name]/', include("[new app name].urls"))` to the list variable`urlpatterns`
4. Create `urls.py` in our new app's directory, with the following structure:
```python
# [new app name]/urls.py
from django.urls import path
from . import views

urlpatterns = [
	path("", views.index, name="index")
]
```
5. In `[new app name]/views.py`, create the `index` function
```python
# [new app name]/views.py
from django.shortcuts import render

value = 0

def index(request):
	return render(request, "[new app name]/index.html", {
		"[variable name in our HTML file]": value
		}
	)
```


Django HTML Syntax
- Variables `{{ [variable name] }}`
- Conditionals `{% [if, elif, else, endif] %}`
- Loops `{% for item in [list object] %}` `{% endfor %}` 

Creating our HTML file
- Put it inside of `[app name]/templates/[app name]/index.html`

Creating and linking CSS files with Django
- Convention is to put CSS files for each app within `[app name]/static/[app name]/styles.css` because they are static files
- Include `{% load static %}` at the top of our HTML file
- Add `<link href="{% static '[app name]/styles.css' %}" rel=stylesheet">` in `<head>`


