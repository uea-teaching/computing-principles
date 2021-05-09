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
ref - https://snarky.ca/why-pathlib-path-doesn-t-inherit-from-str/
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

note: create a relative path, use absolute to get the absolute path
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

note: You have access to basic file system level 
operations such as moving and deleting. 
These methods do not give a warning or before information or files are lost. 
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
