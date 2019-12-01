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

If this is your first time using Django, you’ll have to take care of some initial setup. Namely, you’ll need to auto-generate some code that establishes a Django project --- a collection of settings for an instance of Django, including database configuration, Django-specific options and application-specific settings.

