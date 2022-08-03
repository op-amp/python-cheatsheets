# Python Basic Syntax


###### _Table of Contents_

- Variables
	1. Variable Name
	2. Assignment
	3. References
- Comments
	1. Single Line
	2. Multiline
- Console I/O
	1. Print
	2. Input
- Flow Control
	1. Condition
	2. Loop
	3. Pass
- Pattern Matching
- Exceptions
	1. Exception Raising
	2. Exception Handling
	3. Manual Program Termination
	4. Assertions
- Functions
	1. Parameters
	2. Return Values
	3. Variable Scope
	4. Decorators
	5. Anonymous Functions
- Modules
- Logging


## Variables

### Variable Name

1. Only be one word with no spaces.
2. Only contain letters, numbers, and the underscore character.
3. Only begin with something other than a number.

### Assignment

An assignment statement with an operator `=` stores values in variables.

Multiple assignment is supported using `,` to separate variable names and values.

Conditional assignment is supported using `if` and `else` with the condition in between and values ahead and behind.

### References

Variables do not directly store values. Instead, they store references to computer memory locations where the values are stored.

**Object identity**

This reference, i.e. the identity of memory locations, can be obtained by `id()` function.

**Shallow and deep copy**

In contrast with C, where each variable occupy certain memory space,

![C memory](https://files.realpython.com/media/c_memory3.5afe110faf4d.png)

Normally variable assignment in python are through copying the reference. Thus when modifying mutable values, every variable will be affected.

![Python memory](https://files.realpython.com/media/py_memory3_1.ea43471d3bf6.png)

To avoid this behavior, use `copy.copy()` in the `copy` module to make a duplicate copy of a mutable value, or `copy.deepcopy()` for inner mutable values as well.

**Garbage collection**

- The memory consumption of an object in bytes can be retrieved through [`sys.getsizeof(object)`](https://docs.python.org/3/library/sys.html#sys.getsizeof).
- The reference count of the object can be retrieved through [`sys.getrefcount(object)`](https://docs.python.org/3/library/sys.html#sys.getrefcount).

An object with with a reference count of 0 will get cleaned up by the Python garbage collector.


## Comments

### Single Line Comments

Any text for the rest of the line following a hash mark `#` is part of a comment and will be ignored by Python interpretor during executions.

### Multiline Comments

Multiline strings are often used for comments that span multiple lines.


## Console I/O

### Print

`print(object, sep=' ', end='\n', file=sys.stdout, flush=False)` prints the object to where the file parameter points at and returns `None`.
Multiple objects (possibly of different types) can be printed if they are listed together as multiple arguments.

### Input

`input(prompt)` prints the prompt to standard output and returns the content from standard input as a string.


## Flow Control

### Condition

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

### Loop

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

### Pass

A **`pass` statement** is a null statement. `pass` is not ignored by the interpreter. However, nothing happens when it is executed.


## Pattern Matching

A **`match` statement** takes an expression and compares its value to successive patterns given as one or more `case` blocks; only the first pattern that matches gets executed, and none executed if no matches.
It consists of the following:

- The `match` keyword
- An evaluable expression
- A colon
- An indented block of code with one or more `case` clauses, each with code to be executed when the pattern is matched

Literals in the `case` statement can be combined by `|` to form a single pattern; `_` or any identifier acts as a wildcard that always matches.


## Exceptions

Errors detected during execution are called exceptions (in contrast with syntax errors).

### Exception Raising

A **`raise` statement** allows the programmer to force a specified exception to occur.

### Exception Handling

A **`try` statement** can be used to handle selected exceptions. It can have 4 types of clauses:

1. The code that could potentially casue an error is put in the `try` clause.
2. The program execution moves to the corresponding `except` clause if an error happens.
3. An optional `else` clause following all `except` clauses will be executed if the try clause does not raise an exception.
4. An optional `finally` clause will be unconditionally executed as the last task before the `try` statement completes.

If an exception occurs which does not match any exception named in the `except` clauses, it is passed on to outer `try` statements.
A raise statement inside an `except` clause re-raise the handled exception.

### Manual Program Termination

[`sys.exit(arg=0)`](https://docs.python.org/3/library/sys.html#sys.exit) specifically raises a `SystemExit` exception, signaling an intention to exit the interpreter.

### Assertions

An assertion is a sanity check performed by **`assert` statements**. If the check fails, an `AssertionError` is raised. It consists of the following:

- The `assert` keyword
- A conditional expression
- A comma
- A string to display when the condition is False and the exception raised


## Functions

A function returns a value based on the given arguments with potentially generated side effects.

### Parameters

A **`def` statement** indicates a function definition.
It consists of the following:

- The `def` keyword
- The function name
- Parameters of the function in a pair of round brackets, with positional parameters in front of keyword parameters
- A colon
- An indented block of code (the function body)

Values passed to a function during the function call are called arguments, identified by either position or keyword. Parameters are variables that contain arguments.

Arguments can be variable in length by adding `*` for positional arguments and `**` for keyword arguments.
Arguments in place of `*args` will be combined to a tuple-like object and `**kwargs` to a dict-like object.

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

### Decorators

A function decorator is a special function that wraps another function. It takes a function as the only argument, and completes tasks based on the supplied function.

If a decorator requires other arguments, define an outer function that handles the arguments to the decorator and returns the decorator.

```python
def converter(default=None):
    def decorator(func):
        def conv_no_error(value):
            try:
                result = func(value)
                return result
            except (ValueError, TypeError):
                return default
        return conv_no_error
    return decorator
```

To use a decorator, decorate a function during its definition by

```python
@converter(default=0)
def integer(value):
    return int(value)
```

Or decorate an already defined function by

```python
Int = converter(default=0)(int)
```

### Anonymous Functions

An anonymous function is a function that is defined without a name by `lambda` keyword in the form of `lambda arguments: expression`.

A lambda function can have any number of arguments but only one expression, which is evaluated and returned.


## Modules

Each python program is a module. Usually the module name is just the file name omitting the `.py` suffix.
To use a module:

1. Import the module through `import module`.

	1. The module namespace must then be stated in a function call, likely `module.function()`.
	2. Optional `as` following an imported module bounds the module a new name.
	3. Multiple modules can be imported together with their names separated by `,`.

2. Import specific functions from the module through `from module import function`.

	1. The function can then be called with no namespace.
	2. Optional `as` following an imported function bounds the function a new name.
	3. Multiple functions can be imported together with their names separated by `,`, and `*` represents all functions.


## Logging

The **`logging` module** makes it easy to create a record of custom messages.

``` python
import logging
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s - %(levelname)s - %(message)s')

logging.debug('Test of debug msg')
logging.info('Test of info msg')
logging.warning('Test of warning msg')
logging.error('Test of error msg')
logging.critical('Test of critical msg')

logging.disable(logging.CRITICAL)
```

- `logging.basicConfig(*, level, format, filename=None, filemode='a')` does basic configuration for the logging system.
- `logging.disable(level=CRITICAL)` suppress all log messages at that level or lower.

| Level | Numeric value | Description |
|-------|---------------|-------------|
| logging.CRITICAL | 50 | The lowest level. Used for small details.
| logging.ERROR    | 40 | Used to record information on general events or confirm that things are working at their point.
| logging.WARNING  | 30 | Used to indicate a potential problem that might prevent the program from working in the future.
| logging.INFO     | 20 | Used to record an error that causes the program to fail to do something.
| logging.DEBUG    | 10 | The highest level. Used to indicate a fatal error that causes the program to stop running entirely.


## *Examples*

**Base convertion**

```python
def base_convert(num, base1, base2):
    '''
    Converts numbers in base 1 to base 2.
    '''
    if base2 == base1:
        return num
    elif num == 0:
        return 0
    else:
        return num % base2 + base_convert(num // base2, base1, base2) * base1
```

**Ordinal**

```python
def ordinal(num):
    '''
    Converts numbers to ordinals.
    '''
    if type(num) != int:
        raise TypeError("ordinal() arg must be int")
    elif num < 0:
        raise ValueError("no ordinals for negative integers")
    elif num // 10 % 10 != 1 and 0 < num % 10 < 4:
        suffix = {1:'st', 2:'nd', 3:'rd'}[num % 10]
    else:
        suffix = 'th'
    return str(num) + suffix
```


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
