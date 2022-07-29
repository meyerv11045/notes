# Classes

```python
class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance
```

- The global scope associated with a method is the module containing its definition.
  - A class is never used as a global scope
- Use `isinstance()` to check an instance’s type: 
  - `isinstance(obj, int) `will be True only if `obj.__class__` is `int` or some class derived from `int`
- No private instance variables
  - Convention: `_var` treats member as non-public part of API

## iterators

- `iter()` on a container object returns an iterator object that defines a `__next__()` method to access elements in the container one at a time
  - `__next__()` raises a `StopIteration` exception when no more elements, which indicates the `for` loop to terminate
- `__next__()` and `__iter__()` can be called with `next()` and `iter()`

## generators

- `__iter__()` and `__next__()` are created automatically for a generator function that uses the `yield` keyword
- Easy way to create an iterator by just writing a regular functio
- Generator expressions are similar to list comprehensions except more memory friendly
  - useful when the generator is used immediately by the enclosing function
  - `sum(i * i for i in range(10))`, 
  - `unique_words = set(word for line in page  for word in line.split())`

