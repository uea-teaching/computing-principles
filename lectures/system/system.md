# System Interaction

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

---

## Resources

- https://docs.python.org/ 

- https://www.w3schools.com/python/


Note: Take care with online resources, that they are up to date and accurate

---

## Contents

working with *files* and *folders* on your **system**
<!-- .element: class="fragment" -->

running **external** programs from python
<!-- .element: class="fragment" -->

---

## Paths

--

paths are **not** well represented as strings

different platforms treat the *serialisation* of paths differently
<!-- .element: class="fragment" -->

`path/to/my/file` vs `path\to\my\file`
<!-- .element: class="fragment" -->

note:
a string does not have the same restrictions a path has
character limits, character types etc...

--

### `os.path`

lots of examples on the web using this module
<!-- .element: class="fragment" -->
still valid and current
<!-- .element: class="fragment" -->
requires paths as strings - *fragile*
<!-- .element: class="fragment" -->

note: this does work for making cross platform code,
but you need caution to keep it robust. 

Of course, some things will never work identically across different platforms.

--

### universal approach

represent a path as an object comprised of parts
<!-- .element: class="fragment" -->

--

## `pathlib`

in python use...

`pathlib.Path`
<!-- .element: class="fragment" -->

[documents](https://www.python.org/dev/peps/pep-0428/)
<!-- .element: class="fragment" -->

note: in python this is the pathlib module - particularly the Path object
this is part of the standard library - no need for installs
other languages may have similar approaches

Lets look at some examples...

--

### current working directory

<span style="font-size:1.5em">

```python
path = Path().cwd()
print(path)
```
<!-- .element: class="fragment" -->

```text
/Users/davegreenwood/dev/computing-principles/examples
```
<!-- .element: class="fragment" -->

</span>

--

### relative or absolute

<span style="font-size:1.5em">

```python
path = Path("labs")
print(path.absolute())
```
<!-- .element: class="fragment" -->

```text
/Users/davegreenwood/dev/computing-principles/examples/labs
```
<!-- .element: class="fragment" -->

</span>

note: here I create a relative path, then use absolute() to get the absolute path
The absolute path includes all parents up to the root of the file system

--

### home directory

<span style="font-size:1.5em">

```python
path = Path("~")
print(path.expanduser())
```
<!-- .element: class="fragment" -->

```text
/Users/davegreenwood
```
<!-- .element: class="fragment" -->

</span>

note: often the home directory uses a shorthand tilde - expand user gives the full path.

--

### home directory

<span style="font-size:1.5em">

```python
path = Path().home()
print(path)
```
<!-- .element: class="fragment" -->

```text
/Users/davegreenwood
```
<!-- .element: class="fragment" -->

</span>

note: if you want to start at the users home directory - there is a method for that. 

--

### logical tests

<span style="font-size:1.5em">

```python
path = Path("labs")
print(path.exists())
print(path.is_dir())
print(path.is_file())
print(path.is_symlink())
```
<!-- .element: class="fragment" -->

```text
True
True
False
False
```
<!-- .element: class="fragment" -->

</span>

note: there are others - check the docs!

--

### path parts

<span style="font-size:1.5em">

```python
path = Path("/Users/Shared/Epic Games")

print(path.parts)

for p in path.parts:
    print(type(p), p)
```
<!-- .element: class="fragment" -->

```text
('/', 'Users', 'Shared', 'Epic Games')

<class 'str'> /
<class 'str'> Users
<class 'str'> Shared
<class 'str'> Epic Games
```
<!-- .element: class="fragment" -->

</span>

note: notice I used a long path in a string to instantiate the path object
backslash on windows causes problems though...

--

windows tip - use raw strings

<span style="font-size:1.5em">

```python
path = Path(r'C:\Users\davegreenwood\file.txt')
```

</span>

note: the raw string negates the need to escape the backslash for windows paths.
I will try and get a bit done on strings next week...

--

to construct long paths use `joinpath()` 

<span style="font-size:1.5em">

```python
path = Path().joinpath("long", "path", "to", "file.txt")
```

</span>

note: this is a useful way of building a directory structure. 

--

### path parts as properties

* `path.parent` the containing directory
* `path.name `  the file or directory
* `path.stem`   file name without extension
* `path.suffix` file extension
* `path.anchor` the root of the path

note: The different parts of a path are conveniently available as properties.

--

## Moving and Deleting

--

<!-- .slide: data-background-image="../assets/img/danger.jpg" -->

note: You have access to basic system level file
operations such as moving and deleting. 
These methods do not give a warning before data or files are lost. 
Be very careful when using these methods.

--

## Dangers

* accidental deletion
<!-- .element: class="fragment" -->
* race conditions
<!-- .element: class="fragment" -->

note: the first point is obvious - but it happens to the best of us!
race conditions are more difficult - and can result in unexpected behaviour

--

## Moving and Deleting

<span style="font-size:1.5em">

```python
# directory contains "source.file" NOT "dest.file"
source = Path("source.file")
destination = Path("dest.file")

source.replace(destination)
# directory now contains "dest.file" NOT "source.file"
```

</span>

note: To move a file, use .replace(). 
If the destination already exists, .replace() will overwrite it.
There is no safety net!! This is similar behaviour to the MV command...
Moving is analogous to renaming a file. 

--

### race condition

<span style="font-size:1.8em">

```python
if not destination.exists():
    source.replace(destination)
```
</span>

note: there is a potential race condition here - what if another process
writes to destination after the if statement, but before the replace??

--

### deleting files and directories

`.rmdir()`

`.unlink()`

# CAUTION

note: Directories and files can be deleted using .rmdir() and .unlink() respectively. Extreme caution!!!

--

### creating directories

<span style="font-size:1.2em">

```python [ 1-3 | 1 | 2 | 3 | 1-3 ]
fold = Path("dir")
sub1 = fold.joinpath("sub1")
sub1.mkdir(exist_ok=True, parents=True)
```

</span>

note: 
if the parent does not exist - it is created
if any already exist, no exception is raised
this is a pretty safe way of creating directories...

--

## Exploring Directories

## `path.iterdir()`

note: iterdir provides an iterator over the contents of the directory - 
files, sub directories, sym-links. You will discover more on the difference
between hard and soft links next year.

--

`path.iterdir()`

<span style="font-size:1.2em">

```python
path = Path("dir")

for p in path.iterdir():
    t = "other"
    if p.is_symlink():
        t = "link"
    if p.is_dir():
        t = "dir"
    if p.is_file():
        t = "file"
    print(f"{p} is a {t}")
```

</span>

--

### pattern matching

`path.glob()` `path.rglob()`

note: using glob or rglob (recursive) to match a pattern in the path.
not as powerful as a regex - but very useful.

--

### recursively find **jpg** files

<span style="font-size:1.2em">

```python
path = Path("/Users/Shared/Epic Games")
for p in path.rglob("*.jpg"):
    print(p.name)
```

```text
circle.jpg
selection_add_cursor.jpg
360stereo_test.jpg
image002.jpg
image001.jpg
help.jpg
hdf_logo.jpg
Picture12.jpg
...
```
<!-- .element: class="fragment" -->

</span>

---

## copying files

copying files is somewhat more complex

what about...
<!-- .element: class="fragment" -->
ownership?
<!-- .element: class="fragment" -->
permissions?
<!-- .element: class="fragment" -->
creation time?
<!-- .element: class="fragment" -->

note: it's more than just the data in the file
if you only want the file data do it a different way...

--

## shutil

the shutil module 

--

from the [documents](https://docs.python.org/3/library/shutil.html)

<span style="font-size:0.6em">

> Warning Even the higher-level file copying functions ( shutil.copy(), shutil.copy2() ) cannot copy all file metadata.
>
> On POSIX platforms, this means that file owner and group are lost as well as ACLs.
>
> On Mac OS, the resource fork and other metadata are not used. 
> This means that resources will be lost and file type and creator codes will not be correct.
>
> On Windows, file owners, ACLs and alternate data streams are not copied.

</span>

--

## `shutil.copy2(source, destination)`

copies a file from source path to destination
<!-- .element: class="fragment" -->
attempts to preserve as much meta data as possible
<!-- .element: class="fragment" -->
possibly slower than `shutil.copy()`
<!-- .element: class="fragment" -->

note: for interacting with system files I suggest copy2 as without much penalty
as much meta data is preserved as possible.

--

## `shutil.copytree(source, destination)`

copies an entire directory structure with all children

note: use this one with great caution too!

---

## Interacting with other programs

### `subprocess`

note: the way to do this is with the subprocess module

--

# <span style="color: red"> WARNING </span>
<!-- .slide: data-background-image="../assets/img/warning.jpg" -->

note: Be very clear about what you are executing with subprocess.

--

### `ls.py`

```python
import subprocess

process = subprocess.run(['ls', '-l'])
print('returncode:', process.returncode)
```
<!-- .element: class="fragment" -->

```text
$ python ls.py 
```
<!-- .element: class="fragment" -->

```text
drwxr-xr-x@  7 tcg09yzu  1157254639   224  8 May 12:54 labs
drwxr-xr-x@ 11 tcg09yzu  1157254639   352  7 May 15:32 lectures
-rw-r--r--@  1 tcg09yzu  1157254639   103  9 May 18:24 ls.py
drwxr-xr-x@  9 tcg09yzu  1157254639   288  8 May 12:52 notebooks
drwxr-xr-x@  3 tcg09yzu  1157254639    96 22 Mar 09:29 pdf
drwxr-xr-x@  3 tcg09yzu  1157254639    96  4 May 14:13 seminars
returncode: 0
```
<!-- .element: class="fragment" -->

note: create a file ls.py

--

## notebook

if we run in a notebook we get...
<!-- .element: class="fragment" -->

```text
returncode: 0
```
<!-- .element: class="fragment" -->

note: what happened?? only what we printed went to std out in the notebook
the stdout from the process wasn't captured.

--

## piping

> pass the output of one program to another

note: a big topic - varies according to platform - but with python we can 
write cross platform code - provided the package exists.

--

### notebook

```python
import subprocess
process = subprocess.run(['ls', '-al'], stdout=subprocess.PIPE)
print(process.stdout.decode("utf-8"))
```

pipe the output of `ls` to our python process
<!-- .element: class="fragment" -->

note: subprocess is an advanced module, but very powerful. 
You can run almost anything on your system.
In the same way as piping stdout you can pipe stderr - for warnings and so on.

Lets leave it there...

---

## conclusion

working with *files* and *folders* on your **system**
<!-- .element: class="fragment" -->

running **external** programs from python
<!-- .element: class="fragment" -->

---

### glossary

* ACL - access control list
* POSIX - The Portable Operating System Interface
* UNIX - Uniplexed Information Computing System
