# Python Data Structures


###### _Table of Contents_

- Linear Structures
	1. [List](#1-list)
	2. [Tuple](#2-tuple)
- Non-linear Structures
	1. [Dictionary](#3-dictionary)
	2. [Set](#4-set)


## 1. List
[↑](#table-of-contents)

![Linear Structure](py-Linear.png)

### Concept

> Lists are mutable sequences of object references accessed by position. (Lutz, 2014)

### Features

* The elements in a list have certain positions in the list, and can be sliced
* A list can contain any object in Python
* Every element is mutable
* A list is dynamic

### Common Manipulations

**Declaration**

``` python
EmptyList = []
List = list("spam")
List = ['A', 'B', 'C']
```

**Access**

``` python
val = List[0]
val, vprime = List[0:2] # slice
SubList = List[0:2]
```

**Membership**

``` python
mem = 'A' in List
pos = List.index('A')
freq = List.count('A')
size = len(List)
```

1. `list.index(value)` returns the lowest index of the specified value or raise `ValueError` if not found.
2. `list.count(value)` returns the number of times the specified value occurs.

**Modification**

```python
List[-1] = 'Z'
List[0:2] = 'X', 'Y'
```

**Iteration**

```python
val in List
index, val in enumerate(List)
```

**Insertion**

``` python
List.append('E')
List.insert(3, 'D')
```

1. `list.append(value)` adds the value to the end of the list.
2. `list.insert(index, value)` inserts the value at the specified index in the list.

**Extention**

``` python
List[len(List):] = ['D', 'E', 'F']
List[:0] = ['A']
List += ['G'] # concatenation
List *= 2 # replication
```

**Deletion**

``` python
val = List.pop()
List.remove('A')
del List[1:3]
```

1. `list.pop(index=-1)` removes the element at the given index.
2. `list.remove(value)` remove the first occurrence of the element or raise `ValueError` if not found.

**Order**

``` python
List.reverse()
List.sort()
sorted(List, key = str.lower, reverse = True)
```

1. `list.reverse()` reverses the order of the elements.
2. `list.sort(key=None, reverse=False)` sorts the elements by value. The key parameter is a callable serves as a key for the sort comparison.

**Randomization**

```python
import random
val = random.choice(List)
random.shuffle(List)
```

**Clearance**

``` python
List.clear()
```

## 2. Tuple
[↑](#table-of-contents)

### Concept

> Tuples are immutable sequences of object references accessed by position. Function as fixed lists. (Lutz, 2014)

### Features

* The elements are ordered, and can be sliced
* An element in a tuple can be any object in Python
* Every single element is immutable
* A tuple is static

### Common Manipulations

**Declaration**

```python
EmptyTuple = ()
Tuple = tuple("spam")
Tuple = ([1, 0, 0], [0, 1, 0], [0, 0, 1])
```

**Access**

``` python
val = Tuple[0]
val, vprime = Tuple[0:2] # slice
SubTuple = Tuple[0:2]
```

**Membership**

``` python
[0, 1, 0] in Tuple
pos = Tuple.index([0, 1, 0])
freq = Tuple.count([0, 1, 0])
size = len(Tuple)
```

1. `tuple.index(value)` returns the lowest index of the specified value or raise `ValueError` if not found.
2. `tuple.count(value)` returns the number of times the specified value occurs.

**Iteration**

```python
val in Tuple
index, val in enumerate(Tuple)
```

---

## 3. Dictionary
[↑](#table-of-contents)

![Non-linear Structure](py-Hash.png)

### Concept

> Dictionaries are mutable mappings of object references accessed by key. They are unordered tables that maps keys to values, implemented internally as dynamically expandable hash tables. (Lutz, 2014)

### Features

* Data in a dictionary must be in the form of pairs of a key and a value, and the keys acts as indexes of the values
* Logically, a key must be unique within a dictionary, but two values can be identical
* The keys cannot be mutable objects, but the values can take any object in Python
* The keys are not changeable, but the values are mutable
* A dictionary is dynamic

### Common Manipulations

**Declaration**

`Dict = {key1: value1, key2: value2, key3: value3}`

```python
# declaration
EmptyDict = {}
Dict = dict(zip([1, 2, 3, 4], "spam"))
Dict = dict([(1, 's'), (2, 'p'), (3, 'a'), (4, 'm')])
Dict = {"Amy": [1, 2], "Bob": [2, 3], "Cindy": [3, 4]}

# insertion
Dict["David"] = [4, 5]

# access
Dict["David"] = "Hello" # modification
val = Dict["Amy"]
val = Dict.get("Davis")

# deletion
Dict.popitem()
Dict.pop("Bob")
del Dict["Cindy"]

# extention
Dict.update({"Bob": [2, 3], "Cindy": [3, 4]})

# membership
"Amy" in Dict
key in Dict # keys iteration
Dict.keys()
Dict.values()
Dict.items()
size = len(Dict)

# clearance
Dict.clear()
```

## 4. Set
[↑](#table-of-contents)

### Concept

> Sets are mutable and unordered collections of unique and immutable objects. Function as a key-only (value-less) dictionaries. (Lutz, 2014)

### Features

* The elements are not indexed
* Two elements cannot be identical in a set
* The elements cannot be mutable objects
* A single element is not mutable
* A set is dynamic

### Common Manipulations

**Declaration**

`Set = {key1, key2, key3}`

```python
# declaration
EmptySet = set()
Set = set("spam")
Set = {100, 200, 300}

# insertion
Set.add(400)

# deletion
Set.remove(400)
Set.discard(500)
key = Set.pop()

# extention
Set.update({200})
Set |= EmptySet

# membership
200 in Set
key in Set # elements iteration
size = len(Set)

# mathematical operations
(Set - EmptySet) == Set.difference(EmptySet)
(Set ^ EmptySet) == Set.symmetric_difference(EmptySet)
(Set | EmptySet) == Set.union(EmptySet)
(Set & EmptySet) == Set.intersection(EmptySet)
(Set <= EmptySet) == Set.issubset(EmptySet)
(Set >= EmptySet) == Set.issuperset(EmptySet)

# clearance
Set.clear()
```

## *References*
Lutz, M. (2014). Specific Built-in Types. In _Python Pocket Reference: Python in Your Pocket_ (5th ed.) (pp. 21-66). Sebastopol, CA: O'Reilly Media.
