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
