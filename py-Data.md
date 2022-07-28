# Python Data Structures


###### _Table of Contents_

- Linear Structures (Sequences)
	1. [List](#1-list)
	2. [Tuple](#2-tuple)
- Non-linear Structures (Map and Set)
	1. [Dictionary](#3-dictionary)
	2. [Set](#4-set)


## 1. List
[↑](#table-of-contents)

![Linear Structure](py-Linear.png)

### Concept

> Lists are mutable sequences of object references accessed by position. (Lutz, 2014)

### Features

* The elements are ordered and have certain positions in the list
* A list can be sliced
* An element in a list can be any object in Python
* A list is dynamic and mutable

### Common Manipulations

**Declaration**

``` python
EmptyList = list()
EmptyList = []
List = list("spam")
List = ['', 'A', 'b', 'c']

# comprehension
List = list(v.upper() for v in List if len(v) > 0)
List = [v.upper() for v in List if len(v) > 0]
```

**Access**

``` python
val = List[0]

# slice
val, vprime = List[0:2]
SubList = List[0:2]
```

**Membership**

``` python
mem = 'A' in List
pos = List.index('A')
freq = List.count('A')

size = len(List)
```

1. `list.index(value)` returns the lowest index of the specified value or raises `ValueError` if not found.
2. `list.count(value)` returns the number of times the specified value occurs.

**Iteration**

```python
val in List
index, val in enumerate(List)

# map
map(lambda v: v.upper(), List)
# filter
filter(lambda v: len(v) > 0, List)
```

**Modification**

```python
List[-1] = 'Z'
List[0:2] = 'X', 'Y'
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
List.extend(['E', 'F'])
List[len(List):] = ['G', 'H']
List[:0] = ['A']

# concatenation
List += ['L', 'M', 'N']
# replication
List *= 2
```

**Deletion**

``` python
val = List.pop()
List.remove('A')
del List[1:3]
```

1. `list.pop(index=-1)` removes and returns an element at the given index or raises `IndexError` if index out of range.
2. `list.remove(value)` remove the first occurrence of the element or raises `ValueError` if not found.

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

* The elements are ordered
* A tuple can be sliced
* An element in a tuple can be any object in Python
* A tuple is static and immutable

### Common Manipulations

**Declaration**

```python
EmptyTuple = tuple()
EmptyTuple = ()
Tuple = tuple("spam")
Tuple = ([1, 0, 0], [0, 1, 0], [0, 0, 1])

# comprehension
Tuple = tuple(v for v in Tuple if max(v) > 0)
```

**Access**

``` python
val = Tuple[0]

# slice
val, vprime = Tuple[0:2]
SubTuple = Tuple[0:2]
```

**Membership**

``` python
[0, 1, 0] in Tuple
pos = Tuple.index([0, 1, 0])
freq = Tuple.count([0, 1, 0])

size = len(Tuple)
```

1. `tuple.index(value)` returns the lowest index of the specified value or raises `ValueError` if not found.
2. `tuple.count(value)` returns the number of times the specified value occurs.

**Iteration**

```python
val in Tuple
index, val in enumerate(Tuple)

# map
map(lambda v: v, Tuple)
# filter
filter(lambda v: max(v) > 0, Tuple)
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
* A dictionary is dynamic and mutable

### Common Manipulations

**Declaration**

```python
EmptyDict = dict()
EmptyDict = {}
Dict = dict([(1, 's'), (2, 'p'), (3, 'a'), (4, 'm')])
Dict = dict(zip([1, 2, 3, 4], "spam"))
Dict = {"Alice": "TCP", "Bob": "3-Way", "Cindy": "Handshake"}

# comprehension
Dict = dict((k, Dict[k]) for k in Dict if k.istitle())
Dict = {k: Dict[k] for k in Dict if k.istitle()}
```

**Access**

```python
val = Dict["Alice"]
val = Dict.get("Alice", '')
val = Dict.setdefault("David", "Hello")
```

1. `dict.get(key, fallback=None)` returns the value for the specified key or fallback value if the key is not found.
2. `dict.setdefault(key, default=None)` first inserts key with default value if the key does not exist, and then returns the value for the key.

**Membership**

```python
mem = "Alice" in Dict
mem = "Alice" in Dict.keys()
mem = "TCP" in Dict.values()
mem = ("Alice", "TCP") in Dict.items()

size = len(Dict)
```

**Iteration**

```python
key in Dict
key in Dict.keys()
val in Dict.values()
key, val in Dict.items()

# map
map(lambda k: (k, Dict[k]), Dict)
# filter
filter(lambda k: k.istitle(), Dict)
```

**Modification**

```python
Dict["David"] = {"SYN": 1}
```

**Insertion**

```python
Dict["Eva"] = {"SYN": 1, "ACK": 1}
```

**Deletion**

```python
key, val = Dict.popitem()
val = Dict.pop("Cindy")
del Dict["David"]
```

1. `dict.popitem()` removes and returns a key-value pair in LIFO order or raises `KeyError` if the dictionary is empty.
2. `dict.pop(key)` removes an element having the given key and returns its value, or raises `KeyError` if not found. Optional second parameter can serve as default return value and prevent `KeyError` from being raised.

**Extention**

```python
Dict.update({"Frank": {"ACK": 1}, "Bob": "Three-Way"})
```

**Pretty Printing**

```python
import pprint
pprint.pprint(Dict)
print(pprint.pformat(Dict))
```

**Clearance**

```python
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
* A set is dynamic and mutable

### Common Manipulations

**Declaration**

```python
EmptySet = set()
Set = set("spam")
Set = {101, 202, 303}

# comprehension
Set = set(k % 10 for k in Set if isinstance(k, int))
Set = {k % 10 for k in Set if isinstance(k, int)}
```

**Membership**

```python
mem = 2 in Set

size = len(Set)
```

**Iteration**

```python
key in Set

# map
map(lambda k: k % 10, Set)
# filter
filter(lambda k: isinstance(k, int), Set)
```

**Insertion**

```python
Set.add(4)
```

**Deletion**

```python
key = Set.pop()
Set.remove(4)
Set.discard(5)
```

1. `set.pop()` randomly removes a key and returns the removed key or raises `TypeError` if the set is empty.
2. `set.remove(key)` removes the specified key or raises `KeyError` if the key does not exist.
3. `set.discard(key)` removes the specified key or do nothing if the key does not exist.

**Extention**

```python
Set.update({6, 7})
Set |= {8, 9}
```

**Mathematical Operations**

```python
sub = Set <= set(range(0,9))
sub = Set.issubset(range(0,9))

sup = Set >= set({6: 110})
sup = Set.issuperset({6: 110})

un = Set | {1, 2, 3, 4, 5}
un = Set.union({1, 2, 3, 4, 5})

in = Set & {0, 1, 2}
in = Set.intersection({0, 1, 2})

diff = Set - {0, 1, 2}
diff = Set.difference({0, 1, 2})

sdiff = Set ^ {0, 1, 2}
sdiff = Set.symmetric_difference({0, 1, 2})
```

**Clearance**

```python
Set.clear()
```

## *References*
Lutz, M. (2014). Specific Built-in Types. In _Python Pocket Reference: Python in Your Pocket_ (5th ed.) (pp. 21-66). Sebastopol, CA: O'Reilly Media.
