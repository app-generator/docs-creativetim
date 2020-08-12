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

