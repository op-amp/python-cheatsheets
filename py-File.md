# Python File Operations


###### _Table of Contents_

- Path Objects
	1. Initialization
	2. Combination
	3. Special Directories
	4. Components
	5. Validity
	6. Common Operations
	7. Directory Operations
	8. File Operations
	9. Link Operations
- Pathname Manipulation Functions
- File Objects
	1. ?
	2. ?
- Shelf Objects
	1. ?
	2. ?


## Path Objects

The path presents the location of a file on the computer. There are two ways to specify a file path:

- An absolute path, which always begins with the root folder (`C:\` for Windows with a drive letter C, and `/` for POSIX);
- A relative path, which is relative to the current working directory.

`pathlib` module offers classes representing filesystem paths with semantics appropriate for different operating systems.

### Initialization

Multiple arguments can be provided to specify the hierarchy.

``` python
from pathlib import Path
rel = Path('Documents', 'Dev', 'Python', 'main.py')
```

### Path Combination

The slash operator `/` can combine Path objects and strings and helps create child paths.

It is equvalent to the `path.joinpath(*other)` method which combines the path with each of the other arguments in turn.

``` python
rel = Path('Documents') / 'Dev' / 'Python' / 'main.py'
rel = Path('Documents').joinpath('Dev', 'Python', 'main.py')
```

### Special Directories

Class method `Path.home()` returns the absolute path of the home directory.

``` python
abs = Path.home() / rel
```

Class method `Path.cwd()` returns the absolute path of the current working directory.

``` python
abs = Path.cwd() / rel
```

### Path Components

`path.parts` is a tuple giving access to the various components of a path.

``` python
abs = Path(*abs.parts)
```

Several object properties can be used to extract a certain part:

![The parts of a file path](https://automatetheboringstuff.com/2e/images/000033.jpg)

1. `path.drive` is a string representing the drive letter or name, if any;
2. `path.root` is a string representing the root, if any;
3. `path.anchor` is the concatenation of the drive and root.
4. `path.parent` is the logical parent of the path.
5. `path.name` is a string representing the final path component;
6. `path.suffix` is the file extension of the final component;
7. `path.stem` is the final path component, without its suffix.

### Path Validity

**Type and existence**

1. `path.exists()` returns `True` if the path exists or `False` if not.
2. `path.is_file()` returns `True` if the path exists and is a file, or `False` otherwise.
3. `path.is_dir()` returns `True` if the path exists and is a directory, or `False` otherwise.
4. `path.is_symlink()` returns `True` if the path points to a symbolic link, or `False` otherwise.

**Absolute and relative paths**

1. `path.is_absolute()` returns whether the path is absolute or not.
2. `path.is_relative_to(*start)` returns whether or not this path is relative to the start path.
3. `path.relative_to(*start)` computes a version of this path relative to the start path, or raises `ValueError` if not possible.
4. `path.resolve(strict=False)` makes the path absolute, resolving any symlinks, and returns the resulting path object.
5. `path.expanduser()` returns a new path with expanded `~`.

**Ownership**

1. `path.group()` returns the name of the group owning the file, or raises `KeyError` if not found in the system database.
2. `path.owner()` returns the name of the user owning the file, or raises `KeyError` if not found in the system database.

**Information**

`path.stat(*, follow_symlinks=True)` returns information about the path with an [`os.stat_result`](https://docs.python.org/3/library/os.html#os.stat_result) object.

### Common Operations

**Change mode**

`path.chmod(mode, *, follow_symlinks=True)` changes the file mode and permissions.

**Rename**

`path.rename(target)` renames this file or directory to the given target, and return a new Path instance pointing to target.

### Directory Operations

**Create**

`path.mkdir(mode=0o777, parents=False, exist_ok=False)` creates a new directory at this path, with the mode if given.
If parents is `True`, any missing parents of this path are created as needed, with the default permissions; otherwise, a missing parent raises `FileNotFoundError`.
If the path already exists, `FileExistsError` will be raised when exist_ok is `False`.

**Remove**

`path.rmdir()` removes this directory. The directory must be empty.

**List contents**

`path.iterdir()` yields path objects of the directory contents.

`path.glob(pattern)` globs the given relative pattern string in the directory, yielding all matching files.
A `**` in the pattern literal means this directory and all subdirectories, recursively.

### File Operations

**Create**

`path.touch(mode=0o666, exist_ok=True)` creates a file at this path, with the mode if given.
If the path already exists, `FileExistsError` will be raised when exist_ok is `False`.

**Remove**

`path.unlink(missing_ok=False)` removes this file.
If the path does not exist, `FileNotFoundError` will be raised when missing_ok is `False`.

**Open**

`path.open(mode='r', buffering=-1, encoding=None, errors=None, newline=None)` opens the file the path points to and returns a `file` object.

**Read and write**

Computer files can be categorized into two types:

- Plaintext files contain only basic text characters and do not include font, size, or color information;
- Binary files are all other file types.

``` python
# text files
path.write_text('Text file contents')
content = path.read_text()

# binary files
path.write_bytes(b'Binary file contents')
content = path.read_bytes()
```

### Link Operations

**Create**

1. `path.symlink_to(target, target_is_directory=False)` makes this path a symbolic link to target.
2. `path.hardlink_to(target)` makes this path a hard link to the same file as target.

**Remove**

`path.unlink(missing_ok=False)` removes this symbolic link.
If the path does not exist, `FileNotFoundError` will be raised when missing_ok is `False`.

**Read**

`path.readlink()` returns a string representing the path to which the symbolic link points.


## Pathname Manipulation Functions

The `os.path` module implements useful functions on pathnames.

`os.chdir()`
`os.makedirs()`
`os.path.abspath(path)`
`os.path.isabs(path)`
`os.path.relpath(path, start)`


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
