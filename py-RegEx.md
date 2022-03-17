# Python Regular Expressions


###### _Table of Contents_

- [RE Module](#re-module)
	1. Functions
	2. Constants
	3. [Regular Expression Objects](#regular-expression-objects)
	4. [Match Objects](#match-objects)
- [Pattern Syntax](#pattern-syntax)
	1. Special Characters
	2. Character Classes
	3. Set
	4. Group
	5. Or
	6. Quantifiers
	7. Start / End


## RE Module

``` python
import re
prog = re.compile(pattern)
result = prog.search(string)
```

### Functions

Major manipulation functions:

1. `re.compile(pattern, flags=0)` compiles a pattern into a regular expression object and returns it.
2. `re.match(pattern, string, flags=0)` matches the pattern at the beginning of the string, and returns a match object or `None` if it does not match.
3. `re.fullmatch(pattern, string, flags=0)` matches the pattern to the whole string, and returns a match object or `None` if it does not match.
4. `re.search(pattern, string, flags=0)` scans through the string for the first occurance of the pattern, and returns a match object or `None` if no position matches.
5. `re.findall(pattern, string, flags=0)` returns all non-overlapping matches of the pattern in the string, as a list of strings or tuples (when the pattern includes multiple groups) in the order found.
6. `re.finditer(pattern, string, flags=0)` returns an iterator yielding match objects over all non-overlapping matches in the order found.
7. `re.sub(pattern, repl, string, count=0, flags=0)` returns the string obtained by replacing the non-overlapping occurrences of the pattern in the string by the replacement string or function. A non-negative integer can be used to specify the maximum number of pattern occurrences to be replaced.
8. `re.split(pattern, string, maxsplit=0, flags=0)` splits the string by the occurrences of the pattern and returns the resultant list. A non-negative integer can be used to specify the number of splits, and the remainder of the string is returned as the final element of the list.

### Constants

Flag constants as the last parameter for most of the manipulation functions:

| Syntax      | Abbr        | Description |
| ----------- | ----------- | ----------- |
| re.IGNORECASE | re.I | Perform case-insensitive matching |
| re.MULTILINE 	| re.M | `^` and `$` match the start and end of each line. By default, `^` only for the first line and `$` for the last line |
| re.DOTALL 	| re.S | `.` matches any character at all. By default, it will match anything except a newline |
| re.VERBOSE 	| re.X | Allow multiline patterns by ignoring whitespace and `#` comments except when in a set |

Values can be combined using bitwise OR (the `|` operator) when passed as the parameter.

### Regular Expression Objects

Compiled regular expression objects support methods:

1. `prog.match(string)` matches the pattern at the beginning of the string, and returns a match object or `None` if it does not match.
2. `prog.fullmatch(string)` matches the pattern to the whole string, and returns a match object or `None` if it does not match.
3. `prog.search(string)` scans through the string for the first occurance of the pattern, and returns a match object or `None` if no position matches.
4. `prog.findall(string)` returns all non-overlapping matches of the pattern in the string, as a list of strings or tuples (when the pattern includes multiple groups) in the order found.
5. `prog.finditer(string)` returns an iterator yielding match objects over all non-overlapping matches in the order found.
6. `prog.sub(repl, string, count=0)` returns the string obtained by replacing the non-overlapping occurrences of the pattern in the string by the replacement string or function. A non-negative integer can be used to specify the maximum number of pattern occurrences to be replaced.
7. `prog.split(string, maxsplit=0)` splits the string by the occurrences of the pattern and returns the resultant list. A non-negative integer can be used to specify the number of splits, and the remainder of the string is returned as the final element of the list.

### Match Objects

Match objects always have a boolean value of `True`. To access their contents, use methods:

1. `result.group(1,2,...,N)` returns a single string if there is a single argument (the whole matched string if the argument equals 0 or is omitted), and returns a tuple with one item per argument if there are multiple arguments.
2. `result.groups()` returns a tuple containing all the subgroups of the match.


## Pattern Syntax

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

### Set

`[]` is used to indicate a set of characters.

Inside sets,
- Characters can be listed individually, or ranges can be indicated by giving two characters and separating them by a `-`;
- If the first character of the set is `^`, it means the complement;
- To match a literal `]`, place it as the first character or precede it with a backslash for an escape character;
- Special characters lose special meanings so no need escape characters for them, but character classes are still accepted.

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


## *Examples*

```python
import re
phoneNum = re.compile(r'\+?(\d{1,3})(-| )([- ()\d]+)')

# Example string content sourced from the National Science Foundation website
numFound = phoneNum.search('Call the Help Desk at 1-800-381-1532')
print('Country code: ' + numFound.group(1))
print('Local phone number: ' + numFound.group(3))
```


## *References*
Python Software Foundation. (2022, March 16). _re — Regular expression operations — Python 3.10.2 documentation_. Docs. https://docs.python.org/3/library/re.html
