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
	2. Constructors
	3. Docstrings
	4. The Self Parameter
	5. Object Deletion
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
- The parent class in a pair of round brackets
- A colon
- An indented block of code specifying its attributes

Built-in types can be used as base classes for extension by the user. Most built-in operators can be redefined for class instances.

### Constructors

Class functions that begin with double underscore are called special functions.

When a class defines an `__init__()` method, class instantiation automatically invokes `__init__()` for the newly-created class instance.

### Docstrings

There are also special attributes that begins with double underscores.

For example, `__doc__` gives the docstring of that class.

### The Self Parameter

The first argument of a function in class must be the object itself, oftenly called `self`.
It refers to the current instance of the class, and is used to access variable and method attributes that belongs to the class.

### Object Deletion

A **`del` statement** deletes objects or properties on objects.


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


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
