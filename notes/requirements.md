# Requirements

Requirements files give you a way to create an environment: a set of packages that work together.

Requirements files are lists of packages to install. Instead of running something like `pip install MyApp` and getting whatever libraries come along, you can create a requirements file something like:

```
MyApp
Framework==0.9.4
Library>=0.2
```

If you save this in requirements.txt, then you can `pip install -r requirements.txt`.
