# Python Basic Syntax


###### _Table of Contents_

- Variables
	1. Variable Name
	2. Assignment
- Comments
	1. Single Line
	2. Multiline
	3. Pass
- Console I/O
	1. Print
	2. Input
- Flow Control
	1. Conditions
	2. Loops
- Functions
	1. Parameters
	2. Return Values
	3. Variable Scope
	4. Exception Handling
- Classes
	1. Inheritance
	2. Instantiation
	3. Encapsulation
	4. Self Reference
	5. Operator Overloading
	6. Polymorphism
- Modules


## Variables

### Variable Name

1. Only be one word with no spaces.
2. Only contain letters, numbers, and the underscore character.
3. Only begin with something other than a number.

### Assignment

An assignment statement with an operator `=` stores values in variables.
Multiple assignment is supported in Python.


## Comments

### Single Line Comments

Any text for the rest of the line following a hash mark `#` is part of a comment and will be ignored by Python interpretor during executions.

### Multiline Comments

Multiline strings are often used for comments that span multiple lines.

### Pass

The **`pass` statement** is a null statement. `pass` is not ignored by the interpreter. However, nothing happens when it is executed.


## Console I/O

### Print

`print(object, sep=' ', end='\n', file=sys.stdout, flush=False)` prints the object to where the file parameter points at and returns `None`.
Multiple objects (possibly of different types) can be printed if they are listed together as multiple arguments.

### Input

`input(prompt)` prints the prompt to standard output and returns the content from standard input as a string.


## Flow Control

### Conditions

An **`if` statement** executes when its conditional expression is evaluated as `True`.
It consists of the following:

- The `if` keyword
- A conditional expression
- A colon
- An indented block of code (the `if` clause)

An **`elif` statement** executes when the last previous `if` or `elif` statement is conditioned as `False`, and its conditional expression is evaluated as `True`.
It consists of the following:

- The `elif` keyword
- A conditional expression
- A colon
- An indented block of code (the `elif` clause)

An **`else` statement** executes when the last previous `if` or `elif` statement is conditioned as `False`.
It consists of the following:

- The `else` keyword
- A colon
- An indented block of code (the `else` clause)

### Loops

A **`while` statement** executes repeatedly as long as its conditional expression is evaluated as `True`.
It consists of the following:

- The `while` keyword
- A conditional expression
- A colon
- An indented block of code (the `while` clause)

A **`for` statement** iterates over a sequence, executes once at each step of iteration, and exits after the iteration finishes.
It consists of the following:

- The `for` keyword
- An iterative expression
- A colon
- An indented block of code (the `for` clause)

A **`break` statement** causes the execution to immediately exit the loop.

A **`continue` statement** causes the execution to immediately jump back to the start of the loop and reevaluate the conditional expression.

An **`else` statement** that follows a loop executes when the loop exits normally (i.e. not caused by a `break` statement).


## Functions

### Parameters

A **`def` statement** indicates a function definition.
It consists of the following:

- The `def` keyword
- The function name
- Parameters of the function in a pair of round brackets
- A colon
- An indented block of code (the function body)

Values passed to a function during the function call is called arguments. In a function call, arguments can be identified by position or keyword.

Parameters are variables that contain arguments.

### Return Values

In general, the value that a function call evaluates to is called the return value of the function (Sweigart, 2015).

A **`return` statement** specify the return value of a function.
It consists of the following:

- The `return` keyword
- The value or expression that the function should return

Multiple values can be returned if listed together, separated by `,`.

### Variable Scope

Normally, global variables can be read from a local scope, but local variables cannot be used in the global scope or other local scopes.

In a local scope, whenever a variable is to be written (at the left side of `=` sign), it will be initialized and treated as a local variable.

A **`global` statement** can change the default behavior and make local assignments directly refer to the global variable. No local variable will be initialized then.

### Exception Handling

Errors detected during execution are called exceptions (in contrast with syntax errors).

The **`try` statement** can be used to handle selected exceptions. It can have 4 types of clauses:

1. The code that could potentially casue an error is put in the `try` clause.
2. The program execution moves to the corresponding `except` clause if an error happens.
3. An optional `else` clause following all `except` clauses will be executed if the try clause does not raise an exception.
4. An optional `finally` clause will be unconditionally executed as the last task before the `try` statement completes.

If an exception occurs which does not match any exception named in the `except` clauses, it is passed on to outer `try` statements.


## Classes

### Inheritance

A **`class` statement** indicates a class definition.
It consists of the following:

- The `class` keyword
- The class name
- The base classes in a pair of round brackets, indicates the inheritance
- A colon
- An indented block of code specifying its attributes

Built-in types can be used as base classes for extension by the user.

### Instantiation

Call the class as a function and use an assignment statement to create a class instance, an object.

Each class in Pyhton is actually an instance of the `type` metaclass.
Thus a class definition can be rewritten as: `type(name, bases, attributes)`, an instantiation where the bases is a tuple and the attributes is a dictionary.

A **`del` statement** deletes objects or properties on objects.

### Encapsulation

Private attributes, denoted by a single or double underscores as the prefix, prevent data from direct modifications.

A few common special private attributes of objects:

1. `__init__()` is automatically invoked during class instantiation if defined, initializing a new class instance as its constructor.
2. `__call__()` is invoked when an object is called like a function, to resolve the behaviors of this callable object.
3. `__str__()` is invoked when `print()` or `str()` function are called on the object and returns the object as a string.
4. `__class__` refers to the class from which the object was created.
5. `__doc__` refers to the documentation string (docstring) of that class.
6. `__dict__` refers to a dictionary used to store the public attributes of an object.

### Self Reference

The first argument of a function in class must be the object itself, oftenly called `self`.
It refers to the current instance of the class, and is used to access variable and method attributes that belongs to the class.

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

### Polymorphism

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


## Modules

Each python program is a module. Usually the module name is just the file name omitting the `.py` suffix.
To use the functions and object classes inside a module:

1. Import the module through `import module`.

	- The module namespace must then be stated in a function call, likely `module.function()`.
	- Optional `as` following an imported module bounds the module a new name.
	- Multiple modules can be imported together with their names separated by `,`.

2. Import specific functions from the module through `from module import function`.

	- The function can then be called with no namespace.
	- Optional `as` following an imported function bounds the function a new name.
	- Multiple functions can be imported together with their names separated by `,`, and `*` represents all functions.


## *Examples*

**RTS Game Units Information**

```python
class Entity:
    '''Any abstract solid entity use this as base class'''
    def __init__(self, name, cost, hitpoints, prerequisite, armor):
        self.name = name
        self.cost = cost
        self.hitpoints = hitpoints
        self.prerequisite = prerequisite
        self.armor = armor

class Support:
    '''Abstract support powers'''
    def __init__(self, name, cost, cooldown, prerequisite, power):
        self.name = name
        self.cost = cost
        self.cooldown = cooldown
        self.prerequisite = prerequisite
        self.power = power

class Structure(Entity):
    '''Any abstract structure use this as base class'''
    type = 'Structure'
    def __init__(self, name, cost, hitpoints, prerequisite, armor, power):
        super().__init__(name, cost, hitpoints, prerequisite, armor)
        self.power = power

class Base(Structure):
    '''Abstract buildings'''
    def production_line(self):
        return 'ConYard1'

class Defense(Structure):
    '''Abstract armory'''
    def production_line(self):
        return 'ConYard2'

class Unit(Entity):
    '''Any abstract mobile unit use this as base class'''
    type = 'Unit'
    def __init__(self, name, cost, hitpoints, prerequisite, armor, speed, equipment):
        super().__init__(name, cost, hitpoints, prerequisite, armor)
        self.speed = speed
        self.equipment = equipment

class Infantry(Unit):
    '''Abstract infantry'''
    type = 'Infantry'
    def production_line(self):
        return 'Barrack'

class Vehicle(Unit):
    '''Abstract vehicles'''
    def production_line(self):
        return 'WarFact'

class Ship(Unit):
    '''Abstract ships'''
    def production_line(self):
        return 'Shipyard'

class Aircraft(Unit):
    '''Abstract general Aircrafts'''
    def production_line(self):
        return 'WarFact'

class Jet(Aircraft):
    '''Abstract jet Aircrafts'''
    def production_line(self):
        return 'Airfield'

def get_info(obj):
    info = {}
    info['Name'] = obj.name
    info['Category'] = obj.__class__.type
    info['Cost'] = obj.cost
    info['Prerequisite'] = obj.prerequisite
    try:
        info['Recharge Time'] = obj.cooldown
        info['Requires Power'] = obj.power
    except AttributeError:
        info['Hitpoints'] = obj.hitpoints
        info['Armor'] = obj.armor
        try:
            info['Speed'] = obj.speed
            info['Equipment'] = obj.equipment
        except AttributeError:
            info['Power'] = obj.power
    info['Production Line'] = obj.production_line()
    return info

e2 = Infantry('Conscript', 60, 125, 'Barracks', 'Flak', 7, 'PPSh 41')
print(get_info(e2))
```


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
