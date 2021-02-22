# Analysis of Algorithms

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

Notes: introductions

---

# Analysis of Algorithms: Part 1

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


<div class="r-fit-text">$\sum$</div>

---

<div class="r-fit-text">$O$</div> 

---

# Definitions

--

An asymptote of a curve is a line such that 
the distance between the curve
and the line approaches zero as one or
both of the x or y coordinates tends to infinity.

---

# Summation

<div class="left">

We use the Greek letter 'Sigma' to denote summation.

</div><div class="right"> 

![image](../assets/img/sigma.png) 

</div>

---

---
