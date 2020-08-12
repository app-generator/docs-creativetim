title: How to deploy Flask on Heroku

# [Django](https://www.djangoproject.com/) Deploy on [Heroku](https://www.heroku.com/)

This page explains how to deploy a [Flask](https://www.palletsprojects.com/p/flask/) application on Heroku, the popular deployment platform.

<br />

## Prerequisites

- Basic programming knowledge in Python
- Basic Django knowledge and [WSGI](https://wsgi.readthedocs.io/en/latest/) concept
- Comfortable using a terminal
- Already familiar with [GIT](https://git-scm.com/)

<br />

## What is [Django](https://www.djangoproject.com/)
---

[Django](https://www.djangoproject.com/) is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.
Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It's free and open source.

> **django Links**

- [Django](https://www.djangoproject.com/) - the official website
- [Django Documentation](https://docs.djangoproject.com/en/3.0/)

<br />

## What is [Heroku](https://www.heroku.com/)
---

Heroku's a fully-managed platform that helps developers to deploy apps with ease.
Heroku is a cloud-based, fully-managed platform as a service (Paas) for building, running, and managing apps.

> A short-list with features:

- Runtime - Heroku empowers developers to deliver products using a CLI, called *Heroku Toolbelt*
- PostgreSQL DBMS - a powerful database already configured to be production-ready
- Automatic scaling - Heroku scales in an instant, both vertically and horizontally.
- Github integration - trigger production builds directly from Github commits

> **Heroku Links**

- [Heroku](https://www.heroku.com/) - the official website
- [Heroku Documentation](https://devcenter.heroku.com/)

<br />


To explain the process, we will use a simple Django Boilerplate already enhanced for a Heroku deployment.

## Sample project - [Django Boilerplate](https://github.com/app-generator/boilerplate-code-django)
---

*Django Boilerplate* is a template codebase used by the **AppSeed** platform to generate Django Web Apps enhanced with a basic set of features:

- UI-Ready, simple codebase
- SQLite database, Flask-SQLAlchemy ORM
- Session-Based auth flow (login, register) via Flask-Login
- Deployment scripts: Docker, Gunicorn / Nginx, Heroku

As mentioned, the project comes pre-configured for Heroku. The relevant files are listed below:

- [runtime.txt](https://github.com/app-generator/boilerplate-code-django/blob/master/runtime.txt) - specify the Python version used by Heroku during the build and deploy
- [Procfile](https://github.com/app-generator/boilerplate-code-django/blob/master/Procfile) - configuration file that informs Heroku where to look for the [WSGI](/what-is/wsgi/) interface
- [requirements.txt](https://github.com/app-generator/boilerplate-code-django/blob/master/requirements.txt)
- `settings.py` file - to add the required modules provided by Heroku platform

<br />

### Requirements.txt update
---

To have a successful deployment on Heroku, the usual requirements.txt file should be updated to contain some new modules:

- `gunicorn` - the Gunicorn server to start our app
- `django-heroku` - a helper bundle provided by the Heroku development team to make the deployment much easier.

<br />

### File - [runtime.txt](https://github.com/app-generator/boilerplate-code-django/blob/master/runtime.txt)
---

To build the deploy any python-based app, Heroku uses a default Python version `python-3.6.10` or the one specified in the runtime.txt file. Supported environment, as per Heroku official documentation - [Specifying a Python version](https://devcenter.heroku.com/articles/python-support#specifying-a-python-version):

- python-3.8.3
- python-3.7.7
- python-3.6.10 <-- **The Default Version**
- python-2.7.18

<br />

### Procfile
---

Heroku apps include a Procfile that specifies the commands that are executed by the app on startup.
As specified in the [official docs](https://devcenter.heroku.com/articles/procfile), the *Procfile* is always a simple text file that is named Procfile without a file extension.

```txt
web: gunicorn core.wsgi --log-file=-
```

For our sample, `gunicorn` is called with `core.wsgi` argument.

<br />

### Update `settings.py`

The main app settings file should be updated to include `django-heroku` as below:

```python
# File: core/settings.py

# Usual import here ..
...

import django_heroku     # <-- Include this

...
# Common Django settings
...

# Add this code at the end of the file
# Activate Django-Heroku.
django_heroku.settings(locals())
```

<br />

## How to deploy on Heroku

- [Create a FREE account](https://signup.heroku.com/) on Heroku platform
- [Install the Heroku CLI](https://devcenter.heroku.com/articles/getting-started-with-python#set-up) that match your OS: Mac, Unix or Windows
- Open a terminal window and authenticate via `heroku login` command
- Clone the sources and push the project for LIVE deployment

The full command list, executed on our sample project.

```bash
$ # Get the code
$ git clone https://github.com/app-generator/boilerplate-code-django.git
$ cd boilerplate-code-django
$
$ # Heroku Login
$ heroku login
$
$ # Create the app in Heroku platform
$ heroku create # a random name will be generated by Heroku
$
$ # Disable collect static
$ heroku config:set DISABLE_COLLECTSTATIC=1
$
$ # Push the source code and trigger the deploy
$ git push heroku master
$
$ # Execute DBSchema Migration
$ heroku run python manage.py makemigrations
$ heroku run python manage.py migrate
$
$ # Visit the deployed app in browser.
$ heroku open
$
$ # Create a superuser
$ heroku run python manage.py createsuperuser
```

At this point, you should be able to visit the app in the browser.

<br />

## Help & Resources

- Read more about Heroku - [official docs](https://devcenter.heroku.com/)
- [Django Templates](https://www.creative-tim.com/templates/django) - index provided by Creative-Tim

<br />
