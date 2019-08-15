# Abstract Base Classes

An abstract class is a class that contains one or more abstract methods.

An abstract method is a method that is declared, but contains no implementation.

# Fail to override

A class that is derived from an abstract class cannot be instantiated unless all of its abstract methods are overridden.

```python
from abc import ABC, abstractmethod
 
class AbstractClassExample(ABC):
 
    def __init__(self, value):
        self.value = value
        super().__init__()
    
    @abstractmethod
    def do_something(self):
        pass

class DoAdd42(AbstractClassExample):
    pass

x = DoAdd42(4)
```

# Succeed in overriding

```python
from abc import ABC, abstractmethod
 
class AbstractClassExample(ABC):
 
    def __init__(self, value):
        self.value = value
        super().__init__()
    
    @abstractmethod
    def do_something(self):
        pass

class DoAdd42(AbstractClassExample):
    def do_something(self):
        return self.value + 42
    
class DoMul42(AbstractClassExample):
   
    def do_something(self):
        return self.value * 42
    
x = DoAdd42(10)
y = DoMul42(10)
print(x.do_something())
print(y.do_something())
```

# Implement an abstract method in an abstract base class

The abstract method can be invoked with super() call mechanism.

```python
from abc import ABC, abstractmethod
 
class AbstractClassExample(ABC):
    
    @abstractmethod
    def do_something(self):
        print("Some implementation!")
        
class AnotherSubclass(AbstractClassExample):
    def do_something(self):
        super().do_something()
        print("The enrichment from AnotherSubclass")
        
x = AnotherSubclass()
x.do_something()
```
