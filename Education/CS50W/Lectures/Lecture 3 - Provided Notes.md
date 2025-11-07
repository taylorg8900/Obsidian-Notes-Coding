[Provided notes](https://cs50.harvard.edu/web/notes/3)

Steps to install Django
1. Install [pip](https://pip.pypa.io/en/stable/installation)
2. Run `pip3 install Django` in the terminal

Creating apps with Django
1. `django-admin startproject [project name]` to create the starter files for our project
	- `manage.py` is the program we use to execute commands, for things such as running the server
	- `settings.py` contain configuration for our project
	- `urls.py` contain information on where users are routed after trying to reach a particular URL
2. `python manage.py runserver` will open a local server
3. `python manage.py startapp [app name]` to create a new app, along with some additional directories and files
4. Add our new app by navigating to `settings.py` and adding it to the list variable `INSTALLED_APPS`
5. Go to `[app name]/views.py`, where we create a page that the user will see and interact with, to create the page
6. Create `[app name]/urls.py`