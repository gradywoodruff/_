# Django
A web framework for Python

### Starting Django
First create a new virtual env, and change directories

	virtualenv -p python3 projectname
	cd projectname

Add the new folder as the source make sure Pip is running in that folder

	source bin/activate
	which pip

Install django

	pip install django

Then start a project

	django-admin startproject projectname

Start the server

	python manage.py runserver

### Start a new app
To create a new app first enter the command

	django-admin startapp appname

Then add that app to the `INSTALLED_APPS` in the main `settings.py` file

	INSTALLED_APPS = [
    	'appname'
	    'django.contrib.admin',
	    'django.contrib.auth',
	    'django.contrib.contenttypes',
	    'django.contrib.sessions',
	    'django.contrib.messages',
	    'django.contrib.staticfiles',
	]




# ERRORS
If the settings needs to be reset:

	export DJANGO_SETTINGS_MODULE=django.conf.global_settings