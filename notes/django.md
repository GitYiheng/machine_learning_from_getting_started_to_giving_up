# Django

Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel.

# Installation

```
pip install django
```

## Tutorial 1: Writing Your First Django App

Let’s learn by example.

Throughout this tutorial, we’ll walk you through the creation of a basic poll application.

It’ll consist of two parts:

- A public site that lets people view polls and vote in them.
- An admin site that lets you add, change, and delete polls.

We’ll assume you have Django installed already. You can tell Django is installed and which version by running the following command in a shell prompt:

```
python -m django --version
```

If Django is installed, you should see the version of your installation. If it isn’t, you’ll get an error telling `No module named django`.

This tutorial is written for Django 2.2, which supports Python 3.5 and later.

### Creating a Project

If this is your first time using Django, you’ll have to take care of some initial setup. Namely, you’ll need to auto-generate some code that establishes a Django project &mdash; a collection of settings for an instance of Django, including database configuration, Django-specific options and application-specific settings.

From the command line, `cd` into a directory where you’d like to store your code, then run the following command:

```
django-admin startproject mysite
```

This will create a `mysite` directory in your current directory.

Note: You’ll need to avoid naming projects after built-in Python or Django components. In particular, this means you should avoid using names like `django` (which will conflict with Django itself) or `test` (which conflicts with a built-in Python package).

Let’s look at what `startproject` created:

```
mysite/
├── manage.py
└── mysite
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

These files are:

- The outer `mysite/` root directory is just a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
- `manage.py`: A command-line utility that lets you interact with this Django project in various ways.
- The inner `mysite/` directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. `mysite.urls`).
- `mysite/__init__.py`: An empty file that tells Python that this directory should be considered a Python package.
- `mysite/settings.py`: Settings/configuration for this Django project.
- `mysite/urls.py`: The URL declarations for this Django project; a "table of contents" of your Django-powered site.
- `mysite/wsgi.py`: An entry-point for WSGI-compatible web servers to serve your project.

### The Development Server

Let’s verify your Django project works. Change into the outer `mysite` directory, if you haven’t already, and run the following commands:

```
python manage.py runserver
```

You’ll see the following output on the command line:

```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 17 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

December 01, 2019 - 05:51:26
Django version 2.2.7, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

Note: Ignore the warning about unapplied database migrations for now; we’ll deal with the database shortly.

You’ve started the Django development server, a lightweight Web server written purely in Python. We’ve included this with Django so you can develop things rapidly, without having to deal with configuring a production server – such as Apache – until you’re ready for production.

Now’s a good time to note: **don’t** use this server in anything resembling a production environment. It’s intended only for use while developing.

Now that the server’s running, visit `http://127.0.0.1:8000/` with your Web browser. You’ll see a "Congratulations!" page, with a rocket taking off. It worked!

#### Changing the Port

By default, the `runserver` command starts the development server on the internal IP at port 8000.

If you want to change the server’s port, pass it as a command-line argument. For instance, this command starts the server on port 8080:

```
python manage.py runserver 8080
```

If you want to change the server’s IP, pass it along with the port. For example, to listen on all available public IPs (which is useful if you are running Vagrant or want to show off your work on other computers on the network), use:

```
python manage.py runserver 0:8000
```

`0` is a shortcut for `0.0.0.0`.

#### Automatic reloading of runserver

The development server automatically reloads Python code for each request as needed. You don’t need to restart the server for code changes to take effect. However, some actions like adding files don’t trigger a restart, so you’ll have to restart the server in these cases.

### Creating the Polls App

Now that your environment – a "project" – is set up, you’re set to start doing work.

Each application you write in Django consists of a Python package that follows a certain convention. Django comes with a utility that automatically generates the basic directory structure of an app, so you can focus on writing code rather than creating directories.

#### Projects vs. Apps

What’s the difference between a project and an app? An app is a Web application that does something – e.g., a Weblog system, a database of public records or a simple poll app. A project is a collection of configuration and apps for a particular website. A project can contain multiple apps. An app can be in multiple projects.

Your apps can live anywhere on your Python path. In this tutorial, we’ll create our poll app right next to your `manage.py` file so that it can be imported as its own top-level module, rather than a submodule of `mysite`.

To create your app, make sure you’re in the same directory as `manage.py` and type this command:

```
python manage.py startapp polls
```

That’ll create a directory `polls`, which is laid out like this:

```
polls/
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```
