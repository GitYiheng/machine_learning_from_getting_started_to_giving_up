# Generators

Generator functions allow you to declare a function that behaves like an iterator, i.e. it can be used in a for loop.

First, let us consider the simple example of building a list and returning it.

```python
# Build and return a list
def firstn(n):
    num, nums = 0, []
    while num < n:
        nums.append(num)
        num += 1
    return nums

sum_of_first_n = sum(firstn(1000000))
```

The code is quite simple and straightforward, but it builds the full list in memory.

So, we resort to the generator pattern. The following implements generator as an iterable object.

```python
# Using the generator pattern (an iterable)
class firstn(object):
    def __init__(self, n):
        self.n = n
        self.num, self.nums = 0, []

    def __iter__(self):
        return self

    # Python 3 compatibility
    def __next__(self):
        return self.next()

    def next(self):
        if self.num < self.n:
            cur, self.num = self.num, self.num+1
            return cur
        else:
            raise StopIteration()

sum_of_first_n = sum(firstn(1000000))
```

This will perform as we expect, but we have the following issues:

- There is a lot of boilerplate
- The logic has to be expressed in a somewhat convoluted way

Furthermore, this is a pattern that we will use over and over for many similar constructs. Imagine writing all that just to get an iterator.

Python provides generator functions as a convenient shortcut to building iterators. Lets us rewrite the above iterator as a generator function:

```python
# a generator that yields items instead of returning a list
def firstn(n):
    num = 0
    while num < n:
        yield num
        num += 1

sum_of_first_n = sum(firstn(1000000))
```

Note that the expression of the number generation logic is clear and natural. It is very similar to the implementation that built a list in memory, but has the memory usage characteristic of the iterator implementation.

Generator expressions provide an additional shortcut to build generators out of expressions similar to that of list comprehensions.

In fact, we can turn a list comprehension into a generator expression by replacing the square brackets ("[ ]") with parentheses. Alternately, we can think of list comprehensions as generator expressions wrapped in a list constructor.

Consider the following example:

```python
# list comprehension
doubles = [2 * n for n in range(50)]

# same as the list comprehension above
doubles = list(2 * n for n in range(50))
```

Notice how a list comprehension looks essentially like a generator expression passed to a list constructor.

By allowing generator expressions, we don't have to write a generator function if we do not need the list. If only list comprehensions were available, and we needed to lazily build a set of items to be processed, we will have to write a generator function.

This also means that we can use the same syntax we have been using for list comprehensions to build generators.

Keep in mind that generators are a special type of iterator, and that containers like list and set are also iterables. The uniform way in which all of these are handled adds greatly to the simplification of code.
