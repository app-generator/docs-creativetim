---
title: Black Dashboard Flask
---

# [Black Dashboard Flask](https://www.creative-tim.com/product/black-dashboard-flask)

Black Dashboard Black is a free Bootstrap 4 Admin Template for Django - Features:

- Design - Black Dashboard (Free version)
- UI-Ready, Django Native templating
- [SQLite](https://www.sqlite.org/) database, Native Django ORM
- Session-Based auth flow (login, register)
- Deployment scripts: [Docker](https://www.docker.com/), [Gunicorn](https://gunicorn.org/)/[Nginx](https://www.nginx.com/) stack

> **Links**

- [Black Dashboard Flask](https://www.creative-tim.com/product/black-dashboard-flask) - product page
- [Black Dashboard Flask Demo](https://www.creative-tim.com/live/black-dashboard-flask) - LIVE App, default login credentials ** *test / pass* **
- [Black Dashboard Flask Sources](https://github.com/creativetimofficial/black-dashboard-flask/) - MIT License, released on Github
- Tutorials
    - [Set up `CentOS` for development](./setup-centos-for-development.md)
    - [Set up `Ubuntu` for development](./setup-ubuntu-for-development.md)
    - [Set up `Windows` for development](./setup-windows-for-development.md)
    - [Flask - Deploy on HEROKU](./flask-deploy-on-heroku.md)

<br />

![Black Dashboard Flask - Free Django template](https://raw.githubusercontent.com/app-generator/black-dashboard-flask-demo/master/media/black-dashboard-flask-screen.png)

<br />

## What is [Flask](https://palletsprojects.com/p/flask/)
---

Flask is a lightweight [WSGI](/what-is/wsgi/) web application framework. It is designed to make getting started quick and easy, with the ability to scale up to complex applications.
Classified as a microframework, Flask is written in Python and it does not require particular tools or libraries. It has no database abstraction layer, form validation, or any other components where pre-existing third-party libraries provide common functions.

> **Flask Links**

- [Flask](https://palletsprojects.com/p/flask/) - the official website
- [Flask Documentation](https://flask.palletsprojects.com/)

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

- [Setup CentOS for development](./setup-centos-for-development.md)
- [Setup Ubuntu for development](./setup-ubuntu-for-development.md)
- [Setup Windows for development](./setup-windows-for-development.md)

<br />

## Build the app
---

To built and start the app locally, follow the steps:

> **Get the source code**

- Download the ZIP from Github Repository
- Using GIT tool in the terminal to clone the source code

> **Change the current directory** to `source code` directory

```bash
$ # Make sure you are running the commands INSIDE source code directory
$
$ # Create and activate a Virtualenv (Unix based systems)
$ virtualenv env
$ source env/bin/activate
$
$ # Create and activate a Virtualenv (Windows based systems)
$ # virtualenv env
$ # .\env\Scripts\activate
$
$ # Install requirements
$ pip3 install -r requirements.txt
$
$ # Set the FLASK_APP environment variable
$ (Unix/Mac) export FLASK_APP=run.py
$ (Windows) set FLASK_APP=run.py
$ (Powershell) $env:FLASK_APP = ".\run.py"
$
$ # Set up the DEBUG environment
$ # (Unix/Mac) export FLASK_ENV=development
$ # (Windows) set FLASK_ENV=development
$ # (Powershell) $env:FLASK_ENV = "development"
$
$ # Run the application
$ # --host=0.0.0.0 - expose the app on all network interfaces (default 127.0.0.1)
$ # --port=5000    - specify the app port (default 5000)  
$ flask run --host=0.0.0.0 --port=5000
$
$ # Access the app in browser: http://127.0.0.1:5000/
```

At this point, we can visit the app in the browser **`http://127.0.0.1:5000/`**.
By default, the app will redirect guest users to the login page. To access the private pages:

- Create a new user using the **registration page**
- Authenticate using the **login page**

<br />

## App Codebase (simplified)
---

Starter uses a simple codebase (no Blueprints) with a structure presented bellow:

```bash
< PROJECT ROOT >
   |
   |-- app/                      # Implements app logic
   |    |-- base/                # Base Blueprint - handles the authentication
   |    |-- home/                # Home Blueprint - serve UI Kit pages
   |    |
   |   __init__.py               # Initialize the app
   |
   |-- requirements.txt          # Development modules - SQLite storage
   |-- requirements-mysql.txt    # Production modules  - Mysql DMBS
   |-- requirements-pqsql.txt    # Production modules  - PostgreSql DMBS
   |
   |-- .env                      # Inject Configuration via Environment
   |-- config.py                 # Set up the app
   |-- run.py                    # Start the app - WSGI gateway
   |
   |-- ************************************************************************
```

<br />

## The bootstrap flow
---

- `run.py` loads the `.env` file
- Initialize the app using the specified profile: *Debug* or *Production*
    - If env.DEBUG is set to *True* the SQLite storage is used
    - If env.DEBUG is set to *False* the specified DB driver is used (MySql, PostgreSQL)
- Call the app factory method `create_app` defined in app/__init__.py
- Redirect the guest users to Login page
- Unlock the pages served by *home* blueprint for authenticated users

<br />

> **`.env`** (saved in the root of the project)

```bashrc
# File: `.env`

DEBUG=True              # Enable/Disable the development environment

SECRET_KEY=S3cr3t_Key   # The Key used by Flask to encrypt session information

# Database production settings (If DEBUG=False)

DB_ENGINE=postgresql    # DBMS
DB_NAME=appseed-flask   # Database Name
DB_HOST=localhost       # Database Host
DB_PORT=5432            # Database Port
DB_USERNAME=appseed     # DB Username
DB_PASS=pass            # DB Password

```

<br />

> **`run.py`** (simplified version)

```python
# File: run.py

DEBUG = config('DEBUG', default=True)

# Create the WSGI app, using the app factory pattern
app = create_app( app_config )

# Migrate automaticaly the app using Flask Migrate library
Migrate(app, db)
```

<br />

> **`app/__init__.py`** (simplified version)

```python
# File: app/__init__.py

db            = SQLAlchemy()        # Invoke SQLAlchemy
login_manager = LoginManager()      # Invoke Login Manager

def register_extensions(app):
    db.init_app(app)                # Inject SQLAlchemy magic
    login_manager.init_app(app)     # Add Login Manager to the app

# Register app blueprints: `base`, `home`
def register_blueprints(app):
    for module_name in ('base', 'home'):
        module = import_module('app.{}.routes'.format(module_name))
        app.register_blueprint(module.blueprint)

# Create the tables (automaticaly)
def configure_database(app):

    @app.before_first_request
    def initialize_database():
        db.create_all()

# Create the WSGI app using the factory pattern
def create_app(config):
    app = Flask(__name__, static_folder='base/static')
    app.config.from_object(config)
    register_extensions(app)
    register_blueprints(app)
    configure_database(app)
    return app
```

<br />

The **`app/__init__.py`** constructs the app by putting together a short-list of things:

- Invoke SQLAlchemy
- Invoke and inject the `Login Manager` into the app
- Load the configuration from `config.py` file
- Register the app blueprints
- Check if the database tables are created
- return the WSGI app

<br />

## App Codebase
---

The starter defines two blueprints:

- *Base* blueprint - handles the authentication (routes and forms) and assets management
- *Home* blueprint - serve HTML pages for authenticated users

<br />

> **App / Base Blueprint** structure

```bash
< PROJECT ROOT >
   |
   |-- app/
   |    |-- home/                                # Home Blueprint - serve app pages (private area)
   |    |-- base/                                # Base Blueprint - handles the authentication
   |         |-- static/
   |         |    |-- <css, JS, images>          # CSS files, Javascripts files
   |         |
   |         |-- templates/                      # Templates used to render pages
   |              |
   |              |-- includes/                  #
   |              |    |-- navigation.html       # Top menu component
   |              |    |-- sidebar.html          # Sidebar component
   |              |    |-- footer.html           # App Footer
   |              |    |-- scripts.html          # Scripts common to all pages
   |              |
   |              |-- layouts/                   # Master pages
   |              |    |-- base-fullscreen.html  # Used by Authentication pages
   |              |    |-- base.html             # Used by common pages
   |              |
   |              |-- accounts/                  # Authentication pages
   |                   |-- login.html            # Login page
   |                   |-- register.html         # Registration page
   |
   |-- requirements.txt                          # Development modules - SQLite storage
   |-- requirements-mysql.txt                    # Production modules  - Mysql DMBS
   |-- requirements-pqsql.txt                    # Production modules  - PostgreSql DMBS
   |
   |-- .env                                      # Inject Configuration via Environment
   |-- config.py                                 # Set up the app
   |-- run.py                                    # Start the app - WSGI gateway
   |
   |-- ************************************************************************
```

<br />

> **App / Home Blueprint** structure

```bash
< PROJECT ROOT >
   |
   |-- app/
   |    |-- base/                     # Base Blueprint - handles the authentication
   |    |-- home/                     # Home Blueprint - serve app pages (private area)
   |         |
   |         |-- templates/           # UI Kit Pages
   |              |
   |              |-- index.html      # Default page
   |              |-- page-404.html   # Error 404 - mandatory page
   |              |-- page-500.html   # Error 500 - mandatory page
   |              |-- page-403.html   # Error 403 - mandatory page
   |              |-- *.html          # All other HTML pages
   |
   |-- requirements.txt               # Development modules - SQLite storage
   |-- requirements-mysql.txt         # Production modules  - Mysql DMBS
   |-- requirements-pqsql.txt         # Production modules  - PostgreSql DMBS
   |
   |-- .env                           # Inject Configuration via Environment
   |-- config.py                      # Set up the app
   |-- run.py                         # Start the app - WSGI gateway
   |
   |-- ************************************************************************
```

<br />

## App Configuration
---

The configuration file **`config.py`** (in the root of the project) define a dual configuration controlled via the `.env` file ( `DEBUG` variable)

> **DebugConfig** - default configuration used for development

This configuration becomes active if `.env` file has the `DEBUG` file set to *True*

```python
# Development/Debug configuration

# Set up the App SECRET_KEY
SECRET_KEY = config('SECRET_KEY', default='S#perS3crEt_007')

# This will create a file in <app> FOLDER
SQLALCHEMY_DATABASE_URI = 'sqlite:///' + os.path.join(basedir, 'db.sqlite3')
SQLALCHEMY_TRACK_MODIFICATIONS = False

```

During the first request, the SQLite database and tables are automatically created in the root in the project.

> *Hint*: to visualize the SQLite database content an external tool should be installed: [DB Browser for SQLite](https://sqlitebrowser.org/) it might be a good choice.

<br />

> **ProductionConfig** - production configuration

This configuration becomes active if `.env` file has the `DEBUG` file set to *False*

```python
# Production configuration

SESSION_COOKIE_HTTPONLY  = True
REMEMBER_COOKIE_HTTPONLY = True
REMEMBER_COOKIE_DURATION = 3600

# PostgreSQL database
SQLALCHEMY_DATABASE_URI = '{}://{}:{}@{}:{}/{}'.format(
    config( 'DB_ENGINE'   , default='postgresql'    ),
    config( 'DB_USERNAME' , default='appseed'       ),
    config( 'DB_PASS'     , default='pass'          ),
    config( 'DB_HOST'     , default='localhost'     ),
    config( 'DB_PORT'     , default=5432            ),
    config( 'DB_NAME'     , default='appseed-flask' )
)

```

In this configuration profile, the database defaults to a PostgreSQL DBMS. Make sure the `.env` has the right credentials to access the database.

<br />

## App Tables
---

The file **`app/base/models.py`** (Base Blueprint) defines the table(s) used by the application. Being a simple starter, by default the following tabes are defined:

- Table #1 - **User** with fields:
    - Id - Primary key, unique
    - user - Store the username
    - email - The email address
    - password - Hashed password

<br />

## App Forms
---

The file **`app/base/forms.py`** (Base Blueprint) defines the table(s) used by the application. Being a simple starter, by default the following forms are defined:

- Form #1 - **LoginForm** with fields:
    - username
    - password

<br />

- Form #2 - **RegisterForm** with fields:
    - username - used to authenticate
    - email    - email address
    - password - used to authenticate

<br />

## App Routing
---

The routing rules are defined by *Base* and *Home* blueprints as specified below. This is the public zone of the app.

> **Base Blueprint** - routing file `app/base/routes.py`

- `/login` route is resolved by `login()` method
- `/register` route is resolved by `register()` method
- `/logout` route calls the `logout_user()` defined in [flask_login](https://flask-login.readthedocs.io/en/latest/)

*Registered ERROR handlers*

- 404 Error - Page not found
- 403 Error - Access Forbidden
- 500 Error - Internal Error

<br />

> **Home Blueprint** - routing file `app/home/routes.py`

This blueprint will serve requested pages from `app/home/templates` directory to authenticated users. 
The authentication status is checked by `@login_required` decorator.

- `/<template>` route resolved by `route_template()`.
    - If a requested page is not found a default 404 page is returned to the user

<br />

## Pages & Assets
---

Pages and all assets defined in the UI Kits are served by the app using both blueprints:

- *Home Blueprint* manage the static assets - `app/base/static/assets`
- *Home Blueprint* store the layout `master pages`, HTML chunks (footer. header, scripts) and `login, registration` pages

- *Base Blueprint* serve the HTML pages (index, page-404, etc) and the rest of the pages defined in the UI kit.


```bash
< PROJECT ROOT >
   |
   |-- app/
   |    |-- base/                               # Base Blueprint
   |    |    |-- static/assets/
   |    |    |           |-- css/               # UI Kit css
   |    |    |           |-- JS/                # Javascript files
   |    |    |           |-- images/            # images used by the app
   |    |    |           |-- scss/              # SCSS files (if any)
   |    |    |
   |    |    |-- templates/                      # Templates used to render pages
   |    |         |
   |    |         |-- includes/                  #
   |    |         |    |-- navigation.html       # Top menu component
   |    |         |    |-- sidebar.html          # Sidebar component
   |    |         |    |-- footer.html           # App Footer
   |    |         |    |-- scripts.html          # Scripts common to all pages
   |    |         |
   |    |         |-- layouts/                   # Master pages
   |    |         |    |-- base-fullscreen.html  # Used by Authentication pages
   |    |         |    |-- base.html             # Used by common pages
   |    |         |
   |    |         |-- accounts/                  # Authentication pages
   |    |              |-- login.html            # Login page
   |    |              |-- register.html         # Registration page
   |    |
   |    |-- home/                                # Home Blueprint - serve app pages (private area)
   |         |-- templates/                      # UI Kit Pages
   |              |
   |              |-- index.html                 # Default page
   |              |-- page-404.html              # Error 404 - mandatory page
   |              |-- page-500.html              # Error 500 - mandatory page
   |              |-- page-403.html              # Error 403 - mandatory page
   |              |-- *.html                     # All other HTML pages
   |
   |-- ************************************************************************
```

<br />

## Data Structures
---

The Flask starter exposes a short-list with data structures used globally across the app:

<br />

### `current_user` object

Constructed by [Flask-Login](https://flask-login.readthedocs.io/en/latest/) can be used to detect if the current request is executed by an authenticated user or not. The object has global visibility and can be used in all app controllers and handlers but also in views.

<br />

> **How it works**

`app/base/models.py` define the callback functions required by **Flask-Login** library:

```python
# File: app/base/models.py

@login_manager.user_loader
def user_loader(id):
    return User.query.filter_by(id=id).first()

@login_manager.request_loader
def request_loader(request):
    username = request.form.get('username')
    user = User.query.filter_by(username=username).first()
    return user if user else None

```

<br />

> **Usage in contoler** (Sample file)

```python

def sample_method(path):

    # Redirect guests users to login page
    if not current_user.is_authenticated:
        return redirect(url_for('login'))
```

<br />

> **Usage in view**

```html
    <div class="collapse navbar-collapse" id="navigation">
        <ul class="navbar-nav ml-auto">

        <!-- The Usage of <current_user> object -->
        {% if current_user.is_authenticated %}

            <!-- Html chunk rendered for authenticated users-->

            <li class="nav-item">
                <a href="/" class="nav-link text-primary">
                    <i class="tim-icons icon-minimal-left"></i> Back to Dashboard
                </a>
            </li>

        {% else %}

            <!-- Html chunk rendered for guests users-->

            <li class="nav-item ">
                <a href="{{ url_for('register') }}" class="nav-link">
                    <i class="tim-icons icon-laptop"></i> Register
                </a>
            </li>
            <li class="nav-item ">
                <a href="{{ url_for('login') }}" class="nav-link">
                    <i class="tim-icons icon-single-02"></i> Login
                </a>
            </li>

        {% endif %}

        </ul>
    </div>
```

<br />

## [Flask](https://palletsprojects.com/p/flask/) resources
---

- [Flask](https://palletsprojects.com/p/flask/) - the official website
- [Flask Templates](https://www.creative-tim.com/templates/flask) - index provided by Creative-Tim

<br />
