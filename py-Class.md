# Python Classes


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
7. `__bool__()` returns the boolean value of the object. By default, it evaluates to `True`.
8. `__class__` refers to the class from which the object was created.
9. `__doc__` refers to the documentation string (docstring) of that class.
10. `__dict__` refers to a dictionary used to store the public attributes of an object.

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
class RomanNum():
    '''
    Roman numeral type, with common numeric operations supported.
    '''

    reference = [
        ('M', 1000), ('CM', 900), ('D', 500), ('CD', 400),
        ('C', 100), ('XC', 90), ('L', 50), ('XL', 40),
        ('X', 10), ('IX', 9), ('V', 5), ('IV', 4),
        ('I', 1)
    ]

    def __a_r(self, anum) -> str:
        if not 0 < anum < 4000:
            raise ValueError("integer value requested to be between 1 and 3999 for RomanNum()")
        rnum = ''
        for (rchars, achars) in self.reference:
            while anum >= achars:
                rnum += rchars
                anum -= achars
        return rnum

    def __r_a(self, rnum) -> int:
        anum = 0
        for (rchars, achars) in self.reference:
            while rnum.startswith(rchars):
                anum += achars
                rnum = rnum[len(rchars):len(rnum)]
        if rnum:
            raise ValueError("invalid roman numeral string literal for RomanNum()")
        return anum

    def __init__(self, value):
        if type(value) == RomanNum:
            self.__roman = value.roman()
            self.__arabic = value.arabic()
        elif type(value) == int:
            self.__roman = self.__a_r(value)
            self.__arabic = value
        elif type(value) == str:
            self.__arabic = self.__r_a(value)
            self.__roman = value
        else:
            raise TypeError("RomanNum() only takes a decimal integer or a roman numeral string")

    __call__ = __init__

    def __str__(self) -> str:
        '''
        Returns the roman numeral as string.
        '''
        return self.__roman

    __repr__ = __str__
    roman = __str__

    def __int__(self) -> int:
        '''
        Returns the corresponding arabic numeral as integer.
        '''
        return self.__arabic

    __index__ = __int__
    arabic = __int__

    def __len__(self) -> int:
        '''
        Returns the length of the roman numeral string.
        '''
        return len(self.__roman)

    def __eq__(self, other):
        return self.__arabic == int(other)
    def __ne__(self, other):
        return self.__arabic != int(other)
    def __lt__(self, other):
        return self.__arabic < int(other)
    def __le__(self, other):
        return self.__arabic <= int(other)
    def __gt__(self, other):
        return self.__arabic > int(other)
    def __ge__(self, other):
        return self.__arabic >= int(other)

    def __add__(self, other):
        return RomanNum(self.__arabic + int(other))
    def __sub__(self, other):
        return RomanNum(self.__arabic - int(other))
    def __mul__(self, other):
        return RomanNum(self.__arabic * int(other))
    def __pow__(self, other):
        return RomanNum(self.__arabic ** int(other))
    def __floordiv__(self, other):
        return RomanNum(self.__arabic // int(other))
    def __mod__(self, other):
        return RomanNum(self.__arabic % int(other))
```
