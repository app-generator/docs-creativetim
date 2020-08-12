# [AppSeed/Creative-Tim Docs](https://docs-creative-tim.appseed.us/)

Related documentation repo for common products (latest items):

- [Black Dashboard PRO Django](https://www.creative-tim.com/product/black-dashboard-pro-django) - commercial product
- [Black Dashboard Django](https://www.creative-tim.com/product/black-dashboard-pro-django) - free, MIT License
- [Argon Dashboard Django](https://www.creative-tim.com/product/black-dashboard-pro-django) - free, MIT License

<br />

## How to build the docs

The project uses [Mkdocs](https://www.mkdocs.org/) to generate the HTML pages from Markdown files. To build locally the project, Nodejs must be installed.

```bash
$ # Clone Sources
$ git clone https://github.com/app-generator/docs-creativetim.git
$ cd docs-creativetim
$
$ # Virtualenv modules installation (Unix based systems)
$ virtualenv env
$ source env/bin/activate
$
$ # Virtualenv modules installation (Windows based systems)
$ # virtualenv env
$ # .\env\Scripts\activate
$
$ # Install requirements (mkdoks & related extensions)
$ pip3 install -r requirements.txt
$
$ # Install modules
$ yarn
$
$ # Start the app
$ yarn start
$
$ # Please visit http://localhost:8000 in browser
```

<br />

## How to contribute

Each page provides *Edit on github* shortcut button in the top bar (see below). By clicking on it, the user is redirected to Github and invited to fork, edit the page and make a pull request to notify the owner that the content is updated.

![AppSeed Docs - Edit on Github Option.](https://raw.githubusercontent.com/app-generator/docs-creativetim/master/static/docs-edit-page-option.jpg)

The *pull request* triggered by the change will be merged in the documentation after validation.

> For more information please contact the Support team on [Discord](https://discord.gg/fZC6hup) server.

<br />

## Latest Products

- ToDO

<br />

## Latest update - Mkdocs core

### [Support include of markdown files](https://github.com/mkdocs/mkdocs/issues/777)

> [Help Snippet](https://github.com/mkdocs/mkdocs/issues/777#issuecomment-308266201) - Extracted from Mkdocs Github repository

```yaml
# File: mkdocs.yml

markdown_extensions:
    - markdown_include.include:
        base_path: docs
```

**Usage**

```md
# File: Markdown File Sample

{!some/dir/in/docs/filename.md!}

```

<br />

---
[AppSeed/Creative-Tim Docs](https://docs-creativetim.appseed.us) - Related help for common products
