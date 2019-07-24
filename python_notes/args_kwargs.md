# *args and **kwargs

*args and **kwargs helps you pass a variable number of arguments to a function.

# *arg Example

*args sends a non-keyworded variable length argument tuple to the function

```python
def test_args(f_arg, *args):
    print("first argument:" + str(f_arg))
    for arg in args:
        print("Another argument in args: " + str(arg))

test_args('a','b','c','d')

args = ("one", 2, 3)
test_args(*args)
```

# **kwargs Example

**kwargs sends keyworded variable length of argument dictionary to a function

```python
def test_kwargs(**kwargs):
    if kwargs is not None:
        for key, value in kwargs.iteritems():
            print("%s = %s" % (key, value))
 
test_kwargs(name="a")

kwargs = {"one": 1, "2": "two", "three": "3"}
test_kwargs(**kwargs)
```
