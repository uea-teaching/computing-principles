# Regular Expressions

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

--

## Resources

- https://docs.python.org/ 

- https://www.w3schools.com/python/

- https://www.rexegg.com

- https://regexr.com


Note: Take care with online resources, that they are up to date and accurate

--

## Motivation

regular expressions are available in many programs

here we will look at the Python implementation
<!-- .element: class="fragment" -->

Note: However, there are a few details that need to be observed.

---

<!-- .slide: data-auto-animate -->
## Regular Expressions

https://www.regular-expressions.info

more than 200 minor variations

--

<!-- .slide: data-auto-animate -->
## Regular Expressions

Professor David Brailsford 

The [History](https://youtu.be/528Jc3q86F8) of regular expressions.

https://youtu.be/528Jc3q86F8

note: a really nice background on regex

--

<!-- .slide: data-auto-animate -->
## Regular Expressions

find *patterns* in **strings**

Note: A regular expression specifies a set of strings that matches it.

--

### Ordinary Characters

`'A', 'a', 'X', '5', 'abc'`

Note: Ordinary characters are the simplest regular expressions. 
They match themselves exactly and do not have a special meaning in their regular expression syntax.

--

### Meta Characters

<div style="font-size: 0.75em;">

*symbol* | **result**
:----:|:----
.   | Any Character Except New Line
\d  | Digit (0-9)
\D  | Not a Digit (0-9)
\w  | Word Character (a-z, A-Z, 0-9, _)
\W  | Not a Word Character
\s  | Whitespace (space, tab, newline)
\S  | Not Whitespace (space, tab, newline)

</div>

--

### Anchors

<div style="font-size: 0.75em;">

*symbol* | **result**
:----:|:----
\b | Word Boundary
\B | Not a Word Boundary
^  | Beginning of a String
$  | End of a String

</div>

--

### Character Sets

<div style="font-size: 0.75em;">

*symbol* | **result**
:----:|:----
[ ]   | Matches Characters in brackets
[^ ]  | Matches Characters NOT in brackets
\|    | Either Or
( )   | Group

</div>

--

### Quantifiers

<div style="font-size: 0.75em;">

*symbol* | **result**
:----:|:----
\*    | 0 or More
\+    | 1 or More
?     | 0 or One
{3}   | Exact Number
{3,4} | Range of Numbers (Minimum, Maximum)

</div>

Note: I had to escape these characters to display properly in my slides!

---

<!-- .slide: data-auto-animate -->
# Python RegEx

the `re` module


--

<!-- .slide: data-auto-animate -->
# Python RegEx

`re.search(pattern, string, flags=0)`

Find the first location where the regular expression pattern produces a match.
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
# Python RegEx

`re.split(pattern, string, flags=0)`

Split string by the occurrences of pattern.
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
# Python RegEx

`pattern = re.compile((r"[a|b]")`

Compile a Pattern object.
<!-- .element: class="fragment" -->

Note: Compiled regular expression objects support the 
following methods and attributes:

--

### A Useful Pattern

<div style="font-size: 0.75em;">

`[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+`

</div>

Note: what do you think this RegEx matches?
Let's jump into some live examples...

--

<!-- .slide: data-background-image="../assets/img/exit.jpg" -->
# Examples

---

# Conclusion

reading and writing files

strings

regex

