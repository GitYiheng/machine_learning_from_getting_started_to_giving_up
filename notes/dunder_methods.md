# Dunder or magic methods in Python

Dunder or magic methods in Python are the methods having two prefix and suffix underscores in the method name. Dunder here means "Double Under (Underscores)". These are commonly used for operator overloading. Few examples for magic methods are: `__init__`, `__add__`, `__len__`, `__repr__` etc.

The `__init__` method for initialization is invoked without any call, when an instance of a class is created, like constructors in certain other programming languages such as C++, Java, C#, PHP etc. These methods are the reason we can add two strings with `+` operator without any explicit typecasting.

Here’s a simple implementation:

```python
# Declare our own string class
class String:
  # Magic method to initiate object
  def __init__(self, string):
    self.string = string

# Driver Code
if __name__ == '__main__':
  # Object creation
  string1 = String('Hello')
  
  # Print object location
  print(string1)
```

Output:

```
<__main__.String object at 0x7f8fc832cb00>
```

The above snippet of code prints only the memory address of the string object. Let’s add a `__repr__` method to represent our object.

```python
# Declare our own string class
class String:
  # Magic method to initiate object
  def __init__(self, string):
    self.string = string
  # Print our string object
  def __repr__(self):
    return 'Object: {}'.format(self.string)

# Driver Code
if __name__ == '__main__':
  # object creation
  string1 = String('Hello')
  # print object location
  print(string1)
```
