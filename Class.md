# Python Regular Expressions


###### _Table of Contents_

- Definition
	1. Inheritance
	2. Self Reference
- Instantiation
    1. Metaclass
    2. Deconstruction
- Encapsulation
    1. Special Attributes
	2. Operator Overloading
- Polymorphism


## Definition

A **`class` statement** indicates a class definition.
It consists of the following:

- The `class` keyword
- The class name
- The base classes in a pair of round brackets, indicates the inheritance
- A colon
- An indented block of code specifying its variable and method attributes

### Inheritance

Built-in types can be used as base classes for extension by the user.

Multiple inheritance is supported in Python.
`super()` returns a proxy object that allows the access to the methods of all base classes.

### Self Reference

The first argument of a function in class must be the object itself, oftenly called `self`.
It refers to the current instance of the class, and is used to access attributes that belongs to the class.


## Instantiation

Call the class as a function to create a class instance, an object.

Use an assignment statement to assign a variable with an object value.

### Metaclass

Each class in Pyhton is actually an instance of the `type` metaclass.
Thus a class definition can be rewritten as: `type(name, bases, attributes)`, an instantiation where bases is in the form of a tuple and attributes a dictionary.

### Deconstruction

A **`del` statement** deletes objects or properties on objects.


## Encapsulation

Private attributes, denoted by a single or double underscores as the prefix, prevent data from direct modifications.

### Special Attributes

There exist a few special private attributes that most objects have in common:

1. `__init__()` is automatically invoked during class instantiation if defined, initializing a new class instance as its constructor.
2. `__call__()` is invoked when an object is called like a function, to resolve the behaviors of this callable object.
3. `__str__()` is invoked when `print()` or `str()` function are called on the object and returns its content as a string.
4. `__int__()` is invoked when `int` function is called on the object and returns its content as an integer.
5. `__len__()` is invoked when `len()` function is called on the object and returns the length of the container in the form of an integer.
6. `__getitem__()` is invoked when the item access operator `[]` is applied on the object and returns the corresponding element.
7. `__class__` refers to the class from which the object was created.
8. `__doc__` refers to the documentation string (docstring) of that class.
9. `__dict__` refers to a dictionary used to store the public attributes of an object.

### Operator Overloading

Most built-in operators which are interpreted as functions can be redefined for class instances.

| Operator | Interpretation |
|----------|----------------|
| `a + b`  | `a.__add__(b)` |
| `a - b`  | `a.__sub__(b)` |
| `a * b`  | `a.__mul__(b)` |
| `a ** b` | `a.__pow__(b)` |
| `a / b`  | `a.__truediv__(b)`  |
| `a // b` | `a.__floordiv__(b)` |
| `a % b`  | `a.__mod__(b)` |
| `a << b` | `a.__lshift__(b)`   |
| `a << b` | `a.__rshift__(b)`   |
| `a & b`  | `a.__and__(b)` |
| `a \| b` | `a.__or__(b)`  |
| `a ^ b`  | `a.__xor__(b)` |
| `~a`     | `a.__invert__(b)`   |
| `a < b`  | `a.__lt__(b)`  |
| `a <= b` | `a.__le__(b)`  |
| `a == b` | `a.__eq__(b)`  |
| `a != b` | `a.__ne__(b)`  |
| `a > b`  | `a.__gt__(b)`  |
| `a >= b` | `a.__ge__(b)`  |

## Polymorphism

If multiple types of objects share a same attribute, a common interface can be created by a `def` statement and used.

```python
class A:
    def method(self):
        pass
class B:
    def method(self):
        pass

def interface(object):
    object.method()
```


## *Examples*

**Roman Numeral**

```python
pass
```
