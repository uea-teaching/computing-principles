# Reading and Writing Files

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

--

## Resources

- https://docs.python.org/ 

- https://www.w3schools.com/python/


Note: Take care with online resources, that they are up to date and accurate

--

## Contents

- reading and writing files
- handling special file types

--

## Motivation

Computer programs rarely exist in isolation.

We often need to read and write data.

---

## Reading Files

We use the built-in `open()` function to read files in Python.

note: luckily, it is quite easy to do this in python

--

### `test.txt`

<span style="font-size:1.6em">

```text
A short text file
with
more than
one
line
```

</span>

note: lets consider a small text file, and use it in a few examples.

--

## Contexts

Python has a useful construct: the *context manager*

A context helps us open files safely with minimal code.
<!-- .element: class="fragment" -->

We create a context using the keyword `with`
<!-- .element: class="fragment" -->

--

## Example

<span style="font-size:1.2em">

```python
with open("test.txt") as f:
    data = f.read()

print(data)
```

</span>

<span style="font-size:1.2em">

```text
'A short text file\nwith\nmore than\none\nline\n'
```

</span>

<!-- .element: class="fragment" -->

note: for the slides, I show a string as the file argument, but open accepts
a pathlib path object for creating cross platform solutions.

--

### without using a context

<span style="font-size:1.2em">

```python
try:
    f = open('test.txt')
    data = f.read()
except Exception:
    raise 
finally:
    f.close()
```

</span>


### <span class="bright"> Don't do it! </span>
<!-- .element: class="fragment" -->

--

Our example reads a plain text file.

The data is returned as a `string`.

Note: there are other file types than text...

--

To read a file it must exist.

<span style="font-size:1.2em">

```python
with open("missing.txt") as f:
    pass
```

</span>
<span style="font-size:1.2em">

```text
FileNotFoundError: [Errno 2] No such file or directory: 'missing.txt'
```

</span>

<!-- .element: class="fragment" -->

--

## Writing Files

Writing also makes use of a *context*.

--

## Example

<span style="font-size:1.2em">

```python
with open("out.txt", "w") as f:
    f.write("a line to write\n")
```

</span>

The second argument to `open` is the file *mode*.
<!-- .element: class="fragment" -->

--

# Warning

*if you open an existing file in write mode...*

**it will erase any contents without warning**
<!-- .element: class="fragment" -->

--

## File modes

- `"r"` read from a file (default)
- `"w"` writes to a file
- `"a"` opens the file for appending
- `"x"` create a file - error if it already exists
- `"r+"` opens the file for both reading and writing

--

## Text or Binary

- `"t"` Text - human readable (Default)
- `"b"` Binary mode

Note: In most cases - read and write text files. Binary files
need a good specification to ensure future compatibility.

--

## Methods of File Objects

There are other options aside from `read()` and `write()`.

--

### Example - read one line

```python
with open("test.txt") as f:
    data = f.readline()

print(data)
```

```text
'A short text file\n'
```
<!-- .element: class="fragment" -->

--

### Example - read to list

```python
with open("test.txt") as f:
    data = f.readlines()

print(data)
```

```text
['A short text file\n', 'with\n', 'more than\n', ...]
```
<!-- .element: class="fragment" -->

--

For reading lines from a file, 
you can loop over the file object.

This is memory *efficient* and *fast*.
<!-- .element: class="fragment" -->

--

### Example - iterable

```python
with open("test.txt") as f:
    for line in f:
        print(line, end="")
```

```text
A short text file
with
more than
one
line
```
<!-- .element: class="fragment" -->

--

## Finer Control

--

This is our test file

```text
A short text file
with
more than
one
line
```

--

## Case Study

```python [1 | 2 | 3 | 4 | 5 | 6 | 7]
with open("test.txt") as f:
    while True:
        chunk = f.read(3)
        if not chunk:
            print("<end of file>")
            break
        print(chunk, end="*")
```

--

```python 
with open("test.txt") as f:
    while True:
        chunk = f.read(3)
        if not chunk:
            print("<end of file>")
            break
        print(chunk, end="*")
```

```text
A s*hor*t t*ext* fi*le
*wit*h
m*ore* th*an
*one*
li*ne
*<end of file>
```
<!-- .element: class="fragment" -->

---

# Special File Types

--

<!-- .slide: data-auto-animate -->
## JSON
### JavaScript Object Notation

https://docs.python.org/3/library/json.html

--

<!-- .slide: data-auto-animate -->
## JSON


**objects** as *key: value* pairs
<!-- .element: class="fragment" -->

**arrays** can contain objects, values, arrays
<!-- .element: class="fragment" -->

objects and arrays can be *nested* to any depth
<!-- .element: class="fragment" -->

note: a recursive approach is appropriate to navigating nested file structures.

--

<!-- .slide: data-auto-animate -->
## JSON

The JSON format only supports basic `types`

User defined classes, numpy arrays, etc. are not supported.

note: FYI

--

JSON exists as a `string`

```python
s = '{"name": "red", "values": [255, 0, 0]}'
```

Note: This format follows the python dictionary container, in other languages
this data structure might be called a map, and in javascript it's an object.

--

```python
import json

s = '{"name": "red", "values": [255, 0, 0]}'
col = json.loads(s)
```

`col` is a `dictionary`
<!-- .element: class="fragment" -->

```python
print(col["name"])
```
<!-- .element: class="fragment" -->

```text
red
```
<!-- .element: class="fragment" -->

--

convert a `dictionary` to a JSON `string`

```python
import json

col = dict(name="red", values=[255, 0, 0])
s = json.dumps(col)

print(s)
```

```text
{"name": "red", "values": [255, 0, 0]}
```
<!-- .element: class="fragment" -->

--

## Reading from file

```python
import json

with open("colours.json") as f:
    cold = json.load(f)
```

The `json.load()` method accepts a  `file`  object.
<!-- .element: class="fragment" -->

`cold` is a `dictionary`
<!-- .element: class="fragment" -->

Note: very similar to earlier examples...

--

### Formatting

The `json.dumps()` method has a formatting option.

```python
import json

with open("colours.json") as f:
    cold = json.load(f)

cols = json.dumps(cold, indent=4)
print(cols)
```

--

```text
{
    "colors": [
        {
            "name": "red",
            "values": [
                255,
                0,
                0
            ]
        },
        {
            "name": "green",
            "values": [
...
```

Note: the output is truncated on the slide

--

## Writing JSON

```python
import json

col = dict(name="red", values=[255, 0, 0])

with open("red.json", "w") as f:
    json.dump(col, f)
```

--

### Formatting

The `json.dump()` method also has a formatting option.

note: just like the dumps method, you can set options for indent to
make the result far more human readable.

---

<!-- .slide: data-auto-animate -->
## CSV

### Comma Separated Values

note: very common data format - spreadsheets, excel etc.
the values don't need to be separated by commas

--

<!-- .slide: data-auto-animate -->
## CSV

tabular data - rows and columns
<!-- .element: class="fragment" -->

well suited to iterative exploration
<!-- .element: class="fragment" -->

note: csv data is tabular - not nested in a hierarchy - it is well suited
to iteration. Unlike nested file structures.

--

## `example.csv`

```csv
index,name,city
1,Alice,Aberdeen
2,Bob,Bristol
3,Carol,Chester
4,Dave,Derby
```

note: file extension is irrelevant, it is the structure that matters

--

## CSV in Python

<span style="font-size:2em">

```python
import csv
```

</span>

note: because of the nature of the data, it is quite easy to parse files manually,
but python includes a library that helps.


--

## reading

```python [1-6 | 1 | 3 | 4 | 5-6 | 1-6]
import csv

with open('example.csv') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

note: reader is iterable

--

each row is a list of strings

```
['index', 'name', 'city']
['1', 'Alice', 'Aberdeen']
['2', 'Bob', 'Bristol']
['3', 'Carol', 'Chester']
['4', 'Dave', 'Derby']
```

--

### delimiters

<span style="font-size:2em">

```python
reader = csv.reader(file, delimiter = '\t')
```
</span>

note: different delimiters are available with a keyword argument - this one is a tab
we can also use the same choice of delimiter when writing...

--

<!-- .slide: data-auto-animate -->
### writing

```python [1-7 | 1 | 3 | 4 | 5 | 6-7 | 1-7]
import csv

with open("out.csv", "w") as f:
    writer = csv.writer(f)
    writer.writerow(["index", "name", "city"])
    writer.writerow(['1', 'Alice', 'Aberdeen'])
    writer.writerow(['2', 'Bob', 'Bristol'])
```

note: to write, we must open a file object in write mode...

--

<!-- .slide: data-auto-animate -->
### writing

```python
rowlist = [
    ['index', 'name', 'city'],
    ['1', 'Alice', 'Aberdeen'],
    ['2', 'Bob', 'Bristol'],
    ['3', 'Carol', 'Chester'],
]

with open("out.csv", "w") as f:
    writer = csv.writer(f)
    writer.writerows(rowlist)
```

note: we can also write a list of lists directly

---

## Other formats

--

The Python standard library has modules for reading and writing...

`.html` <!-- .element: class="fragment" -->
`.xml` <!-- .element: class="fragment" -->
`.ini` <!-- .element: class="fragment" -->
`.zip` <!-- .element: class="fragment" -->
`.tar` <!-- .element: class="fragment" -->

and more...
<!-- .element: class="fragment" -->

--

Third party modules are available for reading and writing...

`.rar` <!-- .element: class="fragment" -->
`.h5` <!-- .element: class="fragment" -->

and many, many others...
<!-- .element: class="fragment" -->
