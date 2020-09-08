---
title: Paper Dashboard Django
---

# [Paper Dashboard Django](https://www.creative-tim.com/product/paper-dashboard-django)

Paper Dashboard Django is a free Bootstrap 4 Admin Template for Django - Features:

- Design - Paper Dashboard (Free version)
- [Django Dashboard](https://appseed.us/boilerplate-code/django-dashboard) codebase provided by [AppSeed](https://appseed.us/)
- UI-Ready, Django Native templating
- [SQLite](https://www.sqlite.org/) database, Native Django ORM
- Session-Based auth flow (login, register)
- Deployment scripts: [Docker](https://www.docker.com/), [Gunicorn](https://gunicorn.org/)/[Nginx](https://www.nginx.com/) stack

> **Links**

- [Paper Dashboard Django](https://www.creative-tim.com/product/paper-dashboard-django) - product page
- [Paper Dashboard Django Demo](https://www.creative-tim.com/live/paper-dashboard-django) - LIVE App, default login credentials ** *test / ApS12_ZZs8* **
- [Paper Dashboard Django Sources](https://github.com/creativetimofficial/paper-dashboard-django/) - MIT License, released on Github
- Tutorials
    - [Set up `CentOS` for development](./setup-centos-for-development.md)
    - [Set up `Ubuntu` for development](./setup-ubuntu-for-development.md)
    - [Set up `Windows` for development](./setup-windows-for-development.md)
    - [Django - Deploy on HEROKU](./django-deploy-on-heroku.md)

<br />

![Paper Dashboard Django - Free Django template](https://raw.githubusercontent.com/app-generator/paper-dashboard-django-demo/master/media/paper-dashboard-django-screen.png)

<br />

## What is [Django](https://www.djangoproject.com/)
---

[Django](https://www.djangoproject.com/) is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.
Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It's free and open source.

> **django Links**

- [Django](https://www.djangoproject.com/) - the official website
- [Django Documentation](https://docs.djangoproject.com/en/3.0/)
- [What is Django](/what-is/django) - a comprehensive resource about **Django**

<br />

## Environment
---

To use the stater, [Python3](https://www.python.org/) should be installed properly in the workstation. If you are not sure if Python is properly installed, please open a terminal and type `python --version`. The full-list with dependencies and tools required to build the app:

- [Python3](https://www.python.org/) - the programming language used to code the app
- [GIT](https://git-scm.com/) - used to clone the source code from the Github repository
- Basic development tools (g++ compiler, python development libraries ..etc) used by Python to compile the app dependencies in your environment.

<br />

> Check [Python](https://www.python.org/) version (using the terminal)

```bash
$ # Check Python version
$ python --version
Python 3.7.2 # <--- All good
```

<br />

> Check [GIT](https://git-scm.com/) command tool (using the terminal)

```bash
$ # Check git
$ git --version
$ git version 2.10.1.windows.1 # <--- All good
```

<br />

For more information on how to set up your environment please access the resources listed below. In case we've missed something, contact us on Discord.

- [How to set up Python](/how-to/install-python)
- [Setup CentOS for development](./setup-centos-for-development/)
- [Setup Ubuntu for development](./setup-ubuntu-for-development/)
- [Setup Windows for development](./setup-windows-for-development/)

<br />


## Build the app
---

To built and start the app locally, follow the steps:

> **Get the source code**

Access the product page and download the latest stable release or clone the sources using GIT command-line tool.

> **Change the current directory** to `source code` directory

```bash
$ # Make sure you are running the commands INSIDE source code directory
$
$ # Virtualenv modules installation (Unix based systems)
$ virtualenv env
$ source env/bin/activate
$
$ # Virtualenv modules installation (Windows based systems)
$ # virtualenv env
$ # .\env\Scripts\activate
$
$ # Install modules - SQLite Storage
$ pip3 install -r requirements.txt
$
$ # Create tables
$ python manage.py makemigrations
$ python manage.py migrate
$
$ # Start the application (development mode)
$ python manage.py runserver # default port 8000
$
$ # Start the app - custom port
$ # python manage.py runserver 0.0.0.0:<your_port>
$
$ # Access the web app in browser: http://127.0.0.1:8000/
```

At this point, we can visit the app in the browser **`http://127.0.0.1:8000/`**.
By default, the app will redirect guest users to the login page. To access the private pages:

- Create a new user using the **registration page**
- Authenticate using the **login page**

<br />

## App Codebase (simplified)
---

The codebase is built using a modular, intuitive structure, quite easy to maintain and extend by any developer with a basic Python/Django knowledge.

```bash
< PROJECT ROOT >
   |
   |-- core/                       # Implements app logic and serve the static assets
   |    |-- static/
   |    |    |-- <css, JS, images> # CSS files, Javascripts files
   |    |-- templates/             # Templates used to render pages
   |         |-- includes/         # HTML chunks and components
   |         |-- layouts/          # Master pages
   |         |-- accounts/         # Authentication pages
   |         |
   |      index.html               # The default page
   |       *.html                  # All other HTML pages
   |
   |-- authentication/             # Handles auth routes (login and register)
   |-- app/                        # A simple app that serve HTML files
   |
   |-- requirements.txt            # Development modules - SQLite storage
   |
   |-- .env                        # Inject Configuration via Environment
   |-- manage.py                   # Start the app - Django default start script
   |
   |-- ****************************
```

<br />

## The bootstrap flow
---

- Django bootstrapper `manage.py` uses `core/settings.py` as the main configuration file
- `core/settings.py` loads the app magic from `.env` file
- Redirect the guest users to Login page
- Unlock the pages served by *app* node for authenticated users

<br />

## App Codebase
---

The codebase structure is presented below:

```bash
< PROJECT ROOT >
   |
   |-- core/                               # Implements app logic and serve the static assets
   |    |-- settings.py                    # Django app bootstrapper
   |    |-- wsgi.py                        # Start the app in production
   |    |-- urls.py                        # Define URLs served by all apps/nodes
   |    |
   |    |-- static/
   |    |    |-- <css, JS, images>         # CSS files, Javascripts files
   |    |
   |    |-- templates/                     # Templates used to render pages
   |         |
   |         |-- includes/                 # HTML chunks and components
   |         |    |-- navigation.html      # Top menu component
   |         |    |-- sidebar.html         # Sidebar component
   |         |    |-- footer.html          # App Footer
   |         |    |-- scripts.html         # Scripts common to all pages
   |         |
   |         |-- layouts/                  # Master pages
   |         |    |-- base-fullscreen.html # Used by Authentication pages
   |         |    |-- base.html            # Used by common pages
   |         |
   |         |-- accounts/                 # Authentication pages
   |         |    |-- login.html           # Login page
   |         |    |-- register.html        # Register page
   |         |
   |      index.html                       # The default page
   |     page-404.html                     # Error 404 page
   |     page-500.html                     # Error 404 page
   |       *.html                          # All other HTML pages
   |
   |-- authentication/                     # Handles auth routes (login and register)
   |    |
   |    |-- urls.py                        # Define authentication routes  
   |    |-- views.py                       # Handles login and registration  
   |    |-- forms.py                       # Define auth forms  
   |
   |-- app/                                # A simple app that serve HTML files
   |    |
   |    |-- views.py                       # Serve HTML pages for authenticated users
   |    |-- urls.py                        # Define some super simple routes  
   |
   |-- requirements.txt                    # Development modules - SQLite storage
   |
   |-- .env                                # Inject Configuration via Environment
   |-- manage.py                           # Start the app - Django default start script
   |
   |-- ************************************************************************
```

<br />

## App Configuration
---

The environment configuration file **`.env`** specify a short-list with variables:

- [`SECRET_KEY`](https://docs.djangoproject.com/en/3.0/ref/settings/#secret-key) - Used by Django for [cryptographic signing](https://docs.djangoproject.com/en/3.0/topics/signing/)
- `SERVER` - The public domain/address used in production

```python
# File: core/settings.py

...

# SECRET_KEY value is read from `.env` file
SECRET_KEY = config('SECRET_KEY', default='S#perS3crEt_1122')

...

# Load the production server address from `.env` file
ALLOWED_HOSTS = ['localhost', '127.0.0.1', config('SERVER', default='127.0.0.1')]

...

# The SQLite database, located in the root of the project
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}

```

<br />

The default database is [SQLite](https://www.sqlite.org/) and the name and physical location can be changed by updating `core/settings.py`
The database and associated tables are created during the migration commands, listed in the README file:

```bash
$ # README file, shipped with every Django project

...

$ python manage.py makemigrations
$ python manage.py migrate

...
```

> **Hint**: to visualize the SQLite database content an external tool should be installed: [DB Browser for SQLite](https://sqlitebrowser.org/) it might be a good choice.

<br />

## App Tables
---

The tables created by the Django migration are generated by the default modules that handles the authentication, session management and permissions:

- [`django.contrib.auth`](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django-contrib-auth) - Django middleware app that implements authentication
- `django.contrib.sessions` - Django middleware app that implements session management

<br />

## App Forms
---

The file **`authentication/forms.py`** defines the table(s) used by the application. Being a simple starter, by default the following forms are defined:

- Form #1 - **LoginForm** with fields:
    - username
    - password

<br />

- Form #2 - **SignUpForm** with fields:
    - name - The friendly name
    - email - eMail address
    - username  - used to authenticate
    - password1 - used to authenticate
    - password2 - passwork check field

<br />

## App Routing
---

The settings file **`core/settings.py`** specify the routing file `core/urls.py` via *ROOT_URLCONF* variable:

```python
# File: core/settings.py
...

ROOT_URLCONF = 'core.urls'

...
```

<br />

> **`core/urls.py`** file

The core routing file agregates the routing from all apps defined in the project:

```python
# File: core/urls.py

urlpatterns = [
    # Django admin routes - inherited from Django default modules
    path('admin/', admin.site.urls),

    # Authentication routes - login / register
    # exposed by `authentication` app
    path("", include("authentication.urls")),

    # App routes - the modules that serve the UI Kit pages
    path("", include("app.urls"))
]

```

<br />

## Pages & Assets
---

Pages served by the starter are organized using a simple folder structure:

```bash
< PROJECT ROOT >
   |
   |-- core/                               # Implements app logic and serve the static assets
   |    |
   |    |-- static/assets/
   |    |    |-- css
   |    |    |-- JS
   |    |    |-- images
   |    |    |-- SCSS
   |    |
   |    |-- templates/                     # Templates used to render pages
   |         |
   |         |-- includes/                 # HTML chunks and components
   |         |    |-- navigation.html      # Top menu component
   |         |    |-- sidebar.html         # Sidebar component
   |         |    |-- footer.html          # App Footer
   |         |    |-- scripts.html         # Scripts common to all pages
   |         |
   |         |-- layouts/                  # Master pages
   |         |    |-- base-fullscreen.html # Used by Authentication pages
   |         |    |-- base.html            # Used by common pages
   |         |
   |         |-- accounts/                 # Authentication pages
   |         |    |-- login.html           # Login page
   |         |    |-- register.html        # Register page
   |         |
   |      index.html                       # The default page
   |     page-404.html                     # Error 404 page
   |     page-500.html                     # Error 404 page
   |       *.html                          # All other HTML pages
   |
   |-- app/                                # A simple app that serve HTML files
   |    |
   |    |-- views.py                       # Serve HTML pages for authenticated users
   |    |-- urls.py                        # Define some super simple routes  
   |
   |-- ************************************************************************
```

<br />

### Static Assets

The folder that contains all assets provided by the UI Kit is located in the `core` directory

- `static/assets` - the root directory for all files (JS, images)
- `static/assets/css` - CSS files that style the app
- `static/assets/img` - Images and Icons
- `static/assets/js` - javascript files provided by the UI Kit
- `static/assets/scss` - SCSS files, if provided by the UI Kit vendor

<br />

### `Templates` Folder

All pages served by the application are located inside this folder.

- `templates/layouts` - the directory with app masterpages
- `templates/includes` - the directory with HTML chunks and components
- `templates/accounts` - store the authentication pages (login, registration)
- `templates/` - all pages defined/served by the app are saved in the root of the `templates` folder

<br />

### Common pages

This section lists the common pages defined in all Flask applications prototyped on top of this generic starter.

- login.html, rendered with `layouts/base-fullscreen.html`
- register.html, rendered with `layouts/base-fullscreen.html`
- index.html, rendered with `layouts/base.html`
- page-404.html, rendered with `layouts/base.html`
- page-403.html, rendered with `layouts/base.html`

<br />

## Data Structures
---

The starter exposes a short-list with data structures used globally across the app:

<br />

### `request.user` object

Constructed by [AuthenticationMiddleware](https://docs.djangoproject.com/en/3.0/ref/middleware/#django.contrib.auth.middleware.AuthenticationMiddleware) can be used to detect if the current request is executed by an authenticated user or not. The object has global visibility and can be used in all app controllers and handlers but also in views.

<br />

> **Usage in controller**

```python
# Sample File

from django.http import HttpResponse

def testme(path):

    # Redirect guests users to login page
    if request.user.is_authenticated:
        return HttpResponse("User authenticated")
    else:
        return HttpResponse("Access forbidden - please authenticate")
```

<br />

> **Usage in view**

```html
    <div class="collapse navbar-collapse" id="navigation">
        <ul class="navbar-nav ml-auto">

        <!-- The Usage of <current_user> object -->
        {% if request.user.is_authenticated %}

            <!-- Html chunk rendered for authenticated users-->

            <li class="nav-item">
                <a href="/" class="nav-link text-primary">
                    <i class="tim-icons icon-minimal-left"></i> Your Dashboard
                </a>
            </li>

        {% else %}

            <!-- Html chunk rendered for guests users-->

            <li class="nav-item ">
                <a href="{% url 'register' %}" class="nav-link">
                    <i class="tim-icons icon-laptop"></i> Register
                </a>
            </li>
            <li class="nav-item ">
                <a href="{% url 'login' %}" class="nav-link">
                    <i class="tim-icons icon-single-02"></i> Login
                </a>
            </li>

        {% endif %}

        </ul>
    </div>
```

<br />

## [Django](https://www.djangoproject.com/) resources
---

- [Django](https://www.djangoproject.com/) - the official website
- [Django Documentation](https://docs.djangoproject.com/en/3.0/) - a `must-read` resource for any Django developer
- [Django Templates](https://www.creative-tim.com/templates/django) - index provided by Creative-Tim

<br />
