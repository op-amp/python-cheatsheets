# Python Basic Syntax


###### _Table of Contents_

- Variables
	1. Variable Name
	2. Assignment
- Comments
	1. Single Line
	2. Multiline
- Console I/O
	1. Print
	2. Input
- Control Flow
	1. Conditions
	2. Loops
- Functions
	1. Arguments
	2. Return Values
	3. Variable Scope
	4. Exception Handling
- Classes
- Module Import


## Variables
## Comments
## Console I/O
## Control Flow
## Functions
## Classes
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
	- Multiple functions can be imported together with their names separated by `,`. `*` represents all functions.


## *References*
