# Python File Operations


###### _Table of Contents_

- Path Objects
	1. Instantiation
	2. Combination
	3. Special Directories
	4. Components
	5. Validity
	6. Directory Manipulations
	7. File Manipulations
	8. Link Manipulations
- File Objects
	1. Initialization
	2. Properties
	3. Methods
	4. JSON Convertion
- Shelf Objects
	1. Features
	2. Initialization
	3. Methods
- Archive Files
- File System Interfaces
- Common Pathname Manipulations
- Shell Utilities
- Environment Variables



## Path Objects

The path presents the location of a file on the computer. There are two ways to specify a file path:

- An absolute path, which always begins with the root folder (`C:\` for Windows with a drive letter C, and `/` for POSIX);
- A relative path, which is relative to the current working directory.

The **`pathlib` module** offers classes representing filesystem paths with semantics appropriate for different operating systems.

### Instantiation

Multiple arguments can be provided to specify the hierarchy.

``` python
from pathlib import Path
rel = Path('Documents', 'Dev', 'Python', 'main.py')
```

### Path Combination

The slash operator `/` can combine Path objects and strings and helps create child paths.

It is equvalent to the `path.joinpath(*other)` method which combines the path with each of the _other_ arguments in turn.

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
5. `Path.is_mount()` returns `True` if the path is a mount point, or `False` otherwise.

**Absolute and relative paths**

1. `path.is_absolute()` returns whether the path is absolute or not.
2. `path.is_relative_to(*start)` returns whether or not this path is relative to the _start_ path.
3. `path.relative_to(*start)` computes a version of this path relative to the _start_ path, or raises `ValueError` if not possible.
4. `path.resolve(strict=False)` makes the path absolute, resolving any symlinks, and returns the resulting path object.

**Ownership**

1. `path.group()` returns the name of the group owning the file, or raises `KeyError` if not found in the system database.
2. `path.owner()` returns the name of the user owning the file, or raises `KeyError` if not found in the system database.

### Directory Manipulations

**Create**

`path.mkdir(mode=0o777, parents=False, exist_ok=False)` creates a new directory at this path, with _mode_ if given.
If _parents_ is `True`, any missing parents of this path are created as needed, with the default permissions; otherwise, a missing parent raises `FileNotFoundError`.
If the path already exists, `FileExistsError` will be raised when _exist_ok_ is `False`.

**Remove**

`path.rmdir()` removes this directory. The directory must be empty.

**Rename**

`path.rename(target)` renames this directory to the given _target_, and return a new Path instance pointing to _target_.

**List contents**

`path.iterdir()` yields path objects of the directory contents.

`path.glob(pattern)` globs the given relative _pattern_ string in the directory, yielding all matching files.
A `**` in the pattern literal means this directory and all subdirectories, recursively.

### File Manipulations

**Create**

`path.touch(mode=0o666, exist_ok=True)` creates a file at this path, with _mode_ if given.
If the path already exists, `FileExistsError` will be raised when _exist_ok_ is `False`.

**Remove**

`path.unlink(missing_ok=False)` removes this file.
If the path does not exist, `FileNotFoundError` will be raised when _missing_ok_ is `False`.

**Rename**

`path.rename(target)` renames this file to the given _target_, and return a new Path instance pointing to _target_.

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

### Link Manipulations

**Create**

1. `path.symlink_to(target, target_is_directory=False)` makes this path a symbolic link to _target_.
2. `path.hardlink_to(target)` makes this path a hard link to the same file as _target_.

**Remove**

`path.unlink(missing_ok=False)` removes this symbolic link.
If the path does not exist, `FileNotFoundError` will be raised when _missing_ok_ is `False`.

**Read**

`path.readlink()` returns a string representing the path to which the symbolic link points.


## File Objects

### Initialization

The Python build-in `open()` function returns a File object.

`open(path, mode='r', buffering=-1, encoding=None, errors=None, newline=None)` opens the file the path points at or raises `OSError` if the file cannot be opened.
An optional mode string specifies the mode in which the file is opened, including:

| Mode  | Description |
|-------|-------------|
| `'r'` | Open for reading
| `'w'` | Open for writing, truncating the file first
| `'a'` | Open for writing, appending to the end of file if it exists
| `'x'` | Open for exclusive creation, failing if the file already exists
| `'b'` | Open as binary
| `'t'` | Open as Plaintext (default if unspecified)
| `'+'` | Open for updating (both reading and writing)

### Properties

- `file.mode` is the file access mode used while opening this file.
- `file.closed` is `True` if a file is closed.
- `file.name` is the name of this file.
- `file.encoding` is the encoding this file uses.
- `file.newline` is the types of newlines encountered while reading the file.

### Methods

**Read**

- `file.readable()` returns whether the file can be read or not.
- `file.read()` reads the entire contents of a file as a string value, with at most size characters (in text mode) or size bytes (in binary mode).
- `file.readlines()` gets a list of string values from the file, one string for each line of text.

A file object is iterable with each line as a member.

``` python
file = open(path)
lines = list(l for l in file)
file.close()
```

**Write**

- `file.writable()` returns whether the file can be written to or not.
- `file.write(string)` writes the contents of string to the file, returning the number of characters written.
- `file.writelines(strings)` writes a list of strings to the file.

``` python
import pprint

file = open('main.py', 'r+')
file.read()
file.write('dictionary = ' + pprint.pformat(dictionary) + '\n')
file.close()
```

**Seek**

- `file.tell()` returns an integer giving the current position of the file object in the file.
- `file.seekable()` returns whether the file allows us to change the file position.
- `file.seek(offset, whence=0)` changes file object position in the file. The position is computed from adding _offset_ to a reference point.

| Whence Value | Reference Point |
|--------------|-----------------|
| 0 | The beginning of the file
| 1 | The current file position
| 2 | The end of the file

**Close**

`file.close()` closes an opened file.

### JSON

The **`json` module** provides supports to encode and decode JSON according to the convertion table:

| JSON   | Python |
|--------|--------|
| object | dict
| array  | list
| string | str
| number | int, float
| true   | True
| false  | Flase
| null   | None

**Serialization**

- `json.dump(obj, file)` serializes _obj_ as a JSON formatted stream to file (`.write()`-supporting).
- `json.dumps(obj)` serializes _obj_ to a JSON formatted string as return.

**Deserialization**

- `json.load(file)` deserializes _file_ (`.read()`-supporting) to a Python object as return, or raises `JSONDecodeError` if JSON document invalid.
- `json.loads(string)` deserializes _string_ to a Python object as return, or raises `JSONDecodeError` if JSON document invalid.


## Shelf Objects

The **`shelve` module** offers a way to save variables in your Python programs to binary shelf files.

``` python
import shelve
shelf = shelve.open('pydata')
shelf['path'] = {'type': ['absolute', 'relative'], 'component': ['anchor', 'parent', 'stem']}
shelf.close()
```

### Features

A shelf object is a persistent, dictionary-like object, with ordinary strings as keys. The values in a shelf can be arbitrary Python objects.

### Initialization

`shelve.open(filename, *, writeback=False)` opens a persistent dictionary. By default, the file is opened for reading and writing.

### Methods

- `shelf.sync()` writes back all entries in the cache if the shelf was opened with writeback set to `True`.
- `shelf.close()` synchronizes and closes the persistent dict object.

Multiple files with the same name and different extensions might be created.


## Archive Files

The **`zipfile` module** provides supports for file compression.

**Open**

`zipfile.ZipFile(file, mode='r', compression=zipfile.ZIP_STORED)` opens a ZIP file and returns a ZipFile object used to read and write the ZIP.

**Read**

1. `archive.namelist()` returns a list of archive members by name.
2. `archive.infolist()` returns a list containing a [`ZipInfo`](https://docs.python.org/3/library/zipfile.html#zipfile.ZipInfo) object for each archive member.
3. `archive.getinfo(name)` returns a `ZipInfo` object with information about the archive member _name_.

**Extract**

1. `archive.open(name, mode='r', pwd=None)` accesses a member specified by _name_ as a binary file object.
2. `archive.extract(member, path=None, pwd=None)` extracts a member to the current working directory or _path_; _member_ must be its full name or a ZipInfo object.
3. `archive.extractall(path=None, members=None, pwd=None)` extracts all members to the current working directory or _path_.

**Write**

1. `archive.write(filename, arcname=None, compress_type=None)` writes the file named _filename_ to _archive_, with an archive name _arcname_.
2. `archive.writestr(arcname, data, compress_type=None)` writes a file into _archive_, whose contents is _data_, which may be either a str or a bytes instance.

**Close**

`archive.close()` closes the archive file.


## File System Interfaces

The **`os` module** includes a group of functions and properties about the file system.

**Working directory**

1. `os.getcwd()` returns a string representing the current working directory.
2. `os.listdir(path=os.curdir)` returns a list containing the names of the entries in the directory given by _path_.
3. `os.chdir(path)` changes the current working directory to _path_.

**File and directory information**

1. `os.chmod(path, mode, *, follow_symlinks=True)` changes the mode of _path_ to the numeric _mode_.
2. `os.chown(path, uid, gid, *, follow_symlinks=True)` changes the owner and group of _path_ to the numeric _uid_ and _gid_ (-1 leaves unchanged).
3. `os.stat(path, *, follow_symlinks=True)` returns information about _path_ as an [`os.stat_result`](https://docs.python.org/3/library/os.html#os.stat_result) object.

**Miscellaneous system information**

1. `os.curdir` is the constant string used by the operating system to refer to the current directory. This is `'.'` for Windows and POSIX.
2. `os.pardir` is the constant string used by the operating system to refer to the parent directory. This is `'..'` for Windows and POSIX.
3. `os.sep` is the character used by the operating system to separate pathname components. This is `'/'` for POSIX and `'\\'` for Windows.
4. `os.pathsep` is the character used by the operating system to separate path components. Such as `':'` for POSIX or `';'` for Windows.
5. `os.linesep` is the string used by the operating system to separate (i.e. terminate) lines. Such as `'\n'` for POSIX or `'\r\n'` for Windows.


## Common Pathname Manipulations

The **`os.path` module** implements a few useful functions on pathnames.

**Combination**

`os.path.join(path, *paths)` returns the concatenation of _path_ and any members of _paths_ with exactly one separator following each non-empty part except the last.

**Components**

1. `os.path.dirname(path)` returns a string of everything that comes before the last slash in _path_;
2. `os.path.basename(path)` returns a string of everything that comes after the last slash in _path_.
3. `os.path.split(path)` splits _path_ into everything leading up the last without trailing slashes, and the last pathname component;
4. `os.path.splitdrive(path)` splits _path_ into the drive, and everything following up the drive;
5. `os.path.splitext(path)` splits _path_ into everything leading up the extention, and the file extension.

**Home path**

`os.path.expanduser(path)` returns the argument with an initial component of `~` replaced by the absolute path of the home directory.

**Absolute and relative paths**

1. `os.path.isabs(path)` returns a normalized absolutized version of the pathname _path_.
2. `os.path.abspath(path)` returns `True` if _path_ is an absolute pathname.
3. `os.path.relpath(path, start=os.curdir)` returns a relative filepath to _path_ from the start directory.

**Path information**

1. `os.path.getctime(path)` returns the time of the last metadata change or the creation time for _path_;
2. `os.path.getmtime(path)` returns the time of last modification of _path_;
3. `os.path.getatime(path)` returns the time of last access of _path_.
4. `os.path.getsize(path)` returns the size, in bytes, of _path_, or raises `OSError` if the file does not exist or is inaccessible.


## Shell Utilities

The **`shutil` module** offers a number of high-level operations on files and collections of files.

**Copy**

- `shutil.copy(src, dst, *, follow_symlinks=True)` copies the file _src_ to the file or directory _dst_ and returns the path to the newly created file.
If _dst_ is a directory, the file will be copied into dst using the filename from _src_. If _dst_ is a file that already exists, it will be replaced.
- `shutil.copytree(src, dst, symlinks=False)` recursively copies an entire directory tree rooted at _src_ to a directory named _dst_ and returns the destination.
All intermediate directories needed to contain _dst_ will also be created by default.

**Move**

`shutil.move(src, dst)` recursively move a file or directory _src_ to another location _dst_ and returns the destination.
If the destination is an existing directory, then _src_ will be moved inside. If the destination already exists but is not a directory, it may be overwritten.

**Remove**

`shutil.rmtree(path)` deletes an entire directory tree; _path_ must point to a directory (but not a symbolic link to a directory).


## Environment Variables

The **`os` module** offers properties and functions to interact with the system environment.

**Integrated operational object**

`os.environ` is a mapping object where keys and values are strings that represent the process environment.

**Access**

`os.getenv(key, default=None)` returns the value of the environment variable _key_ if it exists, or _default_ if not.
This method uses `os.environ` and may not reflect environment changes in real time.

**Insertion**

`os.putenv(key, value)` sets the environment variable named _key_ to the string _value_.
Assignments to items in `os.environ` are automatically translated into calls to this method; however, calls to this method do not update `os.environ`.

**Deletion**

`os.unsetenv(key)` deletes the environment variable named _key_.
Deletions of items in `os.environ` are automatically translated into calls to this method; however, calls to this method do not update `os.environ`.


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
