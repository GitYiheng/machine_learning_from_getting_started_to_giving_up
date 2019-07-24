# Decorator

Decorator takes in a function, adds some functionality and returns it. It acts as a wrapper.

# How It Works

Decorate a function and reassign it.

```python
def wrapper(in_func):
    def out_func():
        in_func()
        print("But decorated")
    return out_func

def func():
    print("I'm old")

# before decoration
func()

# after decoration
decorated_func = wrapper(func)
func = decorated_func
func()
```

# Use @

```python
def wrapper(in_func):
    def out_func():
        in_func()
        print("But decorated")
    return out_func

@wrapper
def func():
    print("I'm old")

func()
```

# Decorator with Parameters

```python
def wrapper(in_func):
    def out_func(*args, **kwargs):
        print("Decorated")
        return in_func(*args, **kwargs)
    return out_func

@wrapper
def add(*args, **kwargs):
    sum = 0
    for arg in args:
        sum += arg
    if kwargs is not None:
        for key, value in kwargs.iteritems():
            sum += value
    return sum

print(add(1, 2, 3))
print(add(**{"a": 1, "b": 2, "c": 3}))
print(add(1, 2, 3, **{"a": 1, "b": 2, "c": 3}))
```
