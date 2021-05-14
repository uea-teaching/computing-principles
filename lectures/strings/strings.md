# Strings

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

--

## Resources

- https://docs.python.org/ 

- https://www.w3schools.com/python/


Note: Take care with online resources, that they are up to date and accurate

--

## Motivation

Powerful formatting options for building well crafted output.

Useful tools for dealing with untidy input.

---

# Strings

--

<div style="font-size: 1.5em;">

```text
"a literal string..."

'a literal string...'
```

</div>

note: string literals can use single or double quotes

--

<div style="font-size: 1.5em;">

```text
"a 'literal' string..."

'a "literal" string...'
```

</div>

note: which means you can have one type inside another

--

<div style="font-size: 1.5em;">

```text
"""multiline strings are possible
by using triple quoting.
Again, single or double
can be used and mixed.
"""
```

</div>

*NB:* newlines, tabs and spaces are all included
<!-- .element: class="fragment" -->

--

Triple quoted strings are used for [documentation](https://www.python.org/dev/peps/pep-0257/)

but can be used as literals.
<!-- .element: class="fragment" -->

--

<div style="font-size: 1.5em;">

```python
s = "multiline strings are possible" \
    " by using line continuation."
```

</div>

*NB:* look out for the leading **spaces**
<!-- .element: class="fragment" -->

--

<div style="font-size: 1.5em;">

```python
s = ("multiline strings are possible"
     " by enclosing in parentheses." )
```

</div>

*NB:* There are **no** commas used
<!-- .element: class="fragment" -->

Note: Take note of the space on the second line... 
if you want a space between lines.

this is the preferred way (PEP 8).

--

[PEP 8](https://www.python.org/dev/peps/pep-0008/) guidelines prefer parentheses

Note: PEP 8 is the Python style guide.

---

<!-- .slide: data-auto-animate -->
## String Methods

--

<!-- .slide: data-auto-animate -->
## String Methods

strings are `iterable` and `immutable`

note: iterable means we can consume a string in a for loop
immutable means we can only replace a string not modify it.

--

<!-- .slide: data-auto-animate -->
## String Methods

we can access strings using *indexing*

<div style="font-size: 1.5em;">

```python
b = "Hello, World!"
print(b[2:5])
```

```text
llo
```

</div>

<!-- .element: class="fragment" -->

Note: indexing works in the same way as lists and tuples.

--

<!-- .slide: data-auto-animate -->
## String Methods

`help(str)`

`str` is the python keyword for the string object type
<!-- .element: class="fragment" -->

Note: there are many methods on the string object. 
Don't forget you can get help interactively in a 
jupyter notebook, or ipython interpreter.

All string methods returns new values. 
They do not change the original string.
Why?

--

<!-- .slide: data-auto-animate -->
## String Methods

```python
s = "Hello, World!"

print("a" in s)
print("a" not in s)
print("llo" in s)
```

```text
False
True
True
```

Note: the in keyword can be used on strings - as it can on other collections.

--

<!-- .slide: data-auto-animate -->
## String Methods

```python
s = "Hello, World!"

print(s.upper())
print(s.lower())
print(s.islower())
print(s.isupper())
```

```text
HELLO, WORLD!
hello, world!
False
False
```

Note: we can manipulate the string, or test attributes

--

<!-- .slide: data-auto-animate -->
## String Methods

```python
s = "Hello, World!"

print(s.split(","))
```

```text
['Hello', ' World!']
```

we can `split` a string using a delimiter
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
## String Methods

```python
parts = ["one", "two", "three"]

print(", ".join(parts))
```

```text
one, two, three
```

the opposite of `split` is `join` 
<!-- .element: class="fragment" -->

Note: the join string is inserted between elements

--

<!-- .slide: data-auto-animate -->
## String Methods

```python
s = "val1, val2, \nval3, val4"
print(s.split(","))
print([x.strip() for x in  s.split(",")])
```

```text
['val1', ' val2', ' \nval3', ' val4']

['val1', 'val2', 'val3', 'val4']
```
<!-- .element: class="fragment" -->


use `strip` to remove whitespace
<!-- .element: class="fragment" -->

---

<!-- .slide: data-auto-animate -->
## String Formatting

Python has extensive formatting tools
<!-- .element: class="fragment" -->

Note: formatting has changed over time, 
I'm showing the most recent, recommended methods.
One exception - logging often uses C style string formatting.

--

<!-- .slide: data-auto-animate -->
## String Formatting

```python
age = 42
txt = "Bob is {} years old"
print(txt.format(age))
```

```text
Bob is 42 years old
```

--

<!-- .slide: data-auto-animate -->
## String Formatting

```python
age = 42
txt = "Bob is {} years old, Alice is also {}!"
print(txt.format(age))
```

<div style="font-size: 0.8em">

```text
-------------------------------------------------------------
IndexError                  Traceback (most recent call last)
~/strings.py in 
      39 age = 42
      40 txt = "Bob is {} years old, Alice is also {}!"
----> 41 print(txt.format(age))

IndexError: Replacement index 1 out of range for positional args tuple
```

</div>

<!-- .element: class="fragment" -->

note: 
we can use an argument more than once, but must use an index

--

<!-- .slide: data-auto-animate -->
## String Formatting

```python
age = 42
txt = "Bob is {0} years old, Alice is also {0}!"
print(txt.format(age))
```

```text
Bob is 42 years old, Alice is also 42!
```

--

<!-- .slide: data-auto-animate -->
## String Formatting

```python
alice = 24
bob = 42
txt = "Bob is {b} years old, Alice is really {a}!"
print(txt.format(a=alice, b=bob))
```

```text
Bob is 42 years old, Alice is really 24!
```

note: 
we can also name the arguments and use in any order

--

<!-- .slide: data-auto-animate -->
## String Formatting

# `f` strings

a compact notation using a literal prefix
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
## String Formatting

```python
name = "Bob"
txt = f"{name} is {6 * 7} years old."
print(txt)
```

```text
Bob is 42 years old.
```

note: 
we can pass arguments in scope, or expressions directly.

--

<!-- .slide: data-auto-animate -->
## String Formatting

```python
pad = 3
big = 2**24
dec = 123.123456789
txt = f"big: {big:,} floats: {dec:0.5f}, padding: {pad:04d}"
print(txt)
```

```text
big: 16,777,216 floats: 123.12346, padding: 0003
```
<!-- .element: class="fragment" -->

note: 
many options for formatting numeric output.

--

<!-- .slide: data-auto-animate -->
## String Formatting

formatting has its own [mini-language](https://docs.python.org/3/library/string.html#formatspec)

* text alignment
<!-- .element: class="fragment" -->
* numeric styling
<!-- .element: class="fragment" -->
* scientific notation
<!-- .element: class="fragment" -->
* and much more...
<!-- .element: class="fragment" -->

--

## FYI

`big_num = 1_123_345_567_890`

this is valid python
<!-- .element: class="fragment" -->

Note: One trillion, 123 billion, 345 million ...

--

<!-- .slide: data-auto-animate -->
## Escape Characters

Note:

An escape character lets you use characters that 
are otherwise impossible to put into a string. 
An escape character consists of a backslash (\) 
followed by the character you want to add to the string.

Many characters that are invisible in normal text may need escaping.

--

<!-- .slide: data-auto-animate -->
## Escape Characters


<div style="font-size: 1.2em;">

```python
s = "if I want to \"quote\" Alice\'s work..."
print(s)
```

```text
if I want to "quote" Alice's work...
```
<!-- .element: class="fragment" -->

</div>

--

<!-- .slide: data-auto-animate -->
## Escape Characters

<div style="font-size: 1.2em;">

```python
s = "if I want to use\nanother line..."
print(s)
```

```text
if I want to use
another line...
```
<!-- .element: class="fragment" -->

</div>

--

<!-- .slide: data-auto-animate -->
## Raw Strings

sometimes we *need* to show escape characters
<!-- .element: class="fragment" -->

we do this using an `r` prefix
<!-- .element: class="fragment" -->

Note: Raw string literals are designed to make it easier to include nested 
characters like quotation marks and backslashes that normally have meanings
as delimiters and escape sequence starts.

--

<!-- .slide: data-auto-animate -->
## Raw Strings

<div style="font-size: 1.2em;">

```python
s = r"if I want to use\nanother line..."
print(s)
```

```text
if I want to use\nanother line...
```
<!-- .element: class="fragment" -->

</div>

--

<!-- .slide: data-auto-animate -->
## Raw Strings

we used a raw string to define a windows `path` object

note: in our lab last week

--

<!-- .slide: data-auto-animate -->
## Raw Strings

another use case for a raw string is a `regex` pattern

--

<!-- .slide: data-auto-animate -->
## Raw Strings

another use case for a raw string is a `regex` pattern

more later...
