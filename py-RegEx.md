# Python Regular Expressions


###### _Table of Contents_

- [Methods](#1-methods)
	1. Compile
	2. Search
	3. FindAll
	4. Sub
	5. Split
- [Regular Expression Objects](#2-regular-expression-objects)
- [Match Objects](#3-match-objects)
- [Special Sequences](#4-special-sequences)
	1. Special Characters
	2. Character Classes
	3. Sets
- [Metacharacters](#5-metacharacters)
	1. Group
	2. Or
	3. Quantifiers
	4. Greed
	5. Start / End


## 1. Methods

### Compile

**Parameters**

1. DotAll
2. IgnoreCase
3. Verbose

**Common Manipulations**

``` python
import re
```

## 2. Regular Expression Objects

## 3. Match Objects

## 4. Special Sequences

### Special Characters

| Syntax      | Description |
| ----------- | ----------- |
| .           | Wildcard 		|
| \n          | Newline / Linefeed 	|
| \r          | Carriage Return 	|
| \t          | Horizontal Tab 		|
| \v          | Vertical Tab 		|
| \f          | Formfeed 		|
| \0          | Null 			|
| \a          | Bell 					|
| \b          | Backspace character (only inside sets) 	|
| \c          | Control character 			|
| \\          | Backslash 				|

### Character Classes

| Syntax      | Description | ASCII Set Equivalence |
| ----------- | ----------- | ----------- |
| \d          | Matches decimal digits						| `[0-9]` 		|
| \D          | Matches any character which is not a decimal digit		| `[^0-9]` 		|
| \w          | Matches whitespace characters					| `[a-zA-Z0-9_]` 	|
| \W          | Matches any character which is not a whitespace character	| `[^a-zA-Z0-9_]` 	|
| \s          | Matches word characters						| `[ \t\n\r\f\v]` 	|
| \S          | Matches any character which is not a word character		| `[^ \t\n\r\f\v]` 	|

### Sets

`[]` is used to indicate a set of characters. Inside sets,

- Characters can be listed individually, or ranges can be indicated by giving two characters and separating them by a `-`;
- If the first character of the set is `^`, it means the complement;
- To match a literal `]`, place it as the first character or precede it with a backslash for an escape character;
- Special characters lose special meanings so no need escape characters for them, but character classes are still accepted.

## 5. Metacharacters

### Group

`()` is used to create and capture a group of characters.

### Or

`|` is used to create a regular expression that will match characters on either side.

### Quantifiers

`?`
