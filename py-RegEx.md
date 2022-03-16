# Python Regular Expressions


###### _Table of Contents_

- [RE Module](#re-module)
	1. Functions
	2. Constants
	3. Regular Expression Objects
	4. Match Objects
- [Regular Expression Objects](#regular-expression-objects)
- [Match Objects](#match-objects)
- [Special Sequences](#special-sequences)
	1. Special Characters
	2. Character Classes
	3. Sets
- [Metacharacters](#metacharacters)
	1. Group
	2. Or
	3. Quantifiers
	4. Start / End


## RE Module

``` python
import re
phoneNum = re.compile(r'\+?(\d{1,3})(-| )([- ()\d]+)')

# Example string content sourced from the National Science Foundation website
numFound = phoneNum.search('Call the Help Desk at 1-800-381-1532')
print('Country code: ' + numFound.group(1))
print('Local phone number: ' + numFound.group(3))
```

### Functions

**Compile**

**Search**

**Match**

### Constants

Flag constants as the last parameter for most of the manipulation functions:

| Syntax      | Abbr        | Description |
| ----------- | ----------- | ----------- |
| re.IGNORECASE | re.I | Perform case-insensitive matching |
| re.MULTILINE 	| re.M | `^` and `$` match the start and end of each line. By default, `^` only for the first line and `$` for the last line |
| re.DOTALL 	| re.S | `.` matches any character at all. By default, it will match anything except a newline |
| re.VERBOSE 	| re.X | Allow multiline patterns by ignoring whitespace and `#` comments except when in a set |

### Regular Expression Objects

### Match Objects


## Special Sequences

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

`[]` is used to indicate a set of characters.

Inside sets,
- Characters can be listed individually, or ranges can be indicated by giving two characters and separating them by a `-`;
- If the first character of the set is `^`, it means the complement;
- To match a literal `]`, place it as the first character or precede it with a backslash for an escape character;
- Special characters lose special meanings so no need escape characters for them, but character classes are still accepted.


## Metacharacters

### Group

`()` is used to create and capture a group of characters.

### Or

`|` is used to create a regular expression that will match characters on either side.

### Quantifiers

`{}` is used to specifies some repeated occurrences of the preceding character or characters grouped by round brackets.

- A single number indicates an exact number of occurrences;
- Two numbers seperated by a `,` indicates a range of numbers of occurrences;
- An omitted left bound means a lower bound of zero, and an omitted right bound means an infinite upper bound.

There are also special qualifiers for more convenient usage:

| Syntax      | Description | Equivalent Curly Bracket Denotation |
| ----------- | ----------- | ----------- |
| ?           | zero or one occurrences 	| `{,1}` |
| *           | zero or more occurrences 	| `{,}`  |
| +           | one or more occurrences 	| `{1,}` |

By default, qualifiers and quantifiers are all greedy (try to match as much text as possible).
`?` is used to change their behaviors to a non-greedy fashion when postponed to qualifiers or quantifiers.

### Start / End

| Syntax      | Description |
| ----------- | ----------- |
| ^           | Matches the start of the line 		|
| $           | Matches the end of the line 		|
| \A          | Matches only at the start of the string |
| \Z          | Matches only at the end of the string 	|
| \b          | Matches the empty string, but only at the beginning or end of a word (works as word boundaries) |
| \B          | Matches the empty string, but only when it is not at the beginning or end of a word 		|
