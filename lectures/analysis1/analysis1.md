# Analysis of Algorithms

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

Note: introductions

---

# Analysis of Algorithms 

#### Part 1

### A Gentle Introduction

---

# Reading

- Data Structures and Algorithms
    - Michael T. Goodrich
    - Versions available for Python, Java, etc
- Introduction to Algorithms 
    - Thomas H. Cormen et. al.
    - A more formal resource

Note: Take care with online resources, that they are uo to date and accurate

---

## Goal

> **formally** define an algorithm

--

## Goal

> **understand** how we compare the **performance** of different algorithms

--

## Goal

Counting *fundamental operations*

Performance for different *cases*
<!-- .element: class="fragment" -->

*Run-time complexity* as a function of problem size
<!-- .element: class="fragment" -->

--

## How Good is an Algorithm?

> in plain English...

Note: Knowing how to compare algorithms is important so you can make sure you are 
using the correct one for the job at hand!

It would be very useful information if you could tell that sorting 
algorithm a is expected to take x amount of time to sort products on your
website vs. algorithm b that is expected to take x*x

--

## Time and Space

Time complexity - How *long* does it take to run?
<!-- .element: class="fragment" -->

Space complexity - How much *memory* does it need?
<!-- .element: class="fragment" -->

--

## Time and Space

Often a trade-off!

Note:
Typically this is a trade-off, where algorithms that reduce time complexity 
may increase the space complexity, and vice versa.

--

## Time complexity

> We will focus on how long an algorithm takes to run!

Note: In your next year - you will explore in more depth!

---

## What is an Algorithm?

An algorithm is a finite **sequence** of unambiguous **instructions** for 
solving a **problem**, that will always **terminate**.

Note: A reminder of a formal definition of an algorithm.
Emphasise, always correct, and always terminate.

--

## What is an Algorithm?

Algorithms are *developed* through a process of *translation*, 
from an *informal* description to a *formal* description

--

**Formal** descriptions are written in **pseudo code**

--

## Developing Algorithms

### **Specification**
<!-- .element: class="fragment" -->

### **Inputs**
<!-- .element: class="fragment" -->

### **Outputs**
<!-- .element: class="fragment" -->

Note: Three things we need to know? 
What should it do? Feasible inputs, outputs or effect?

--

## Developing Algorithms 

> The first level of understanding is the human one. 
> You should be able to explain in plain terms how the algorithm works.

--

## Developing Algorithms

> The second level is a more detailed, but still informal description 
> that breaks the problem down into sub-problems.

--

## Developing Algorithms

> The third level, is a detailed pseudo code description, with all stages 
> refined until the description is unambiguous.

---

## Writing Pseudocode

There is no universally accepted pseudo-code.

It *should* be language independent.

Note: We will relax that rule to enable runnable code in the labs!

--

<div class="left-center">

pseudocode

```text

scanArray(array[1..n], key): returns boolean
    for i := 1 to n
        if key == array[i]
        return true
    return false


```

</div> <div class="right-center">

python

```python

def scan_values(key, values):
    for value in values:
        if value == key:
            return True
    return False


```

</div>

---

## Case Study

--

### Linear Scan Algorithm

1. *Specification*: for an array of n values, return true if key is in values, otherwise false.
2. *Input*: array, size n, element key
3. *Output*: boolean - true if key is found in array, false otherwise

--

### Formal algorithm

```text

scanArray(array[1..n], key): returns boolean
    for i := 1 to n
        if key == array[i]
        return true
    return false

```

--

# How long will this take to run?

---
