# Analysis of Algorithms
<!-- .slide: data-auto-animate -->

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

Note: introductions

--

# Analysis of Algorithms 
<!-- .slide: data-auto-animate -->

#### Part 1

### A Gentle Introduction

--

## Reading

- Data Structures and Algorithms
    - Michael T. Goodrich
    - Versions available for Python and Java.
- Introduction to Algorithms 
    - Thomas H. Cormen et. al.
    - A more formal resource

Note: Take care with online resources, that they are up to date and accurate

--

## Synopsis

* Defining and Developing Algorithms
<!-- .element: class="fragment" -->
* Experimental Analysis
<!-- .element: class="fragment" -->
* Analytic Characterisation
<!-- .element: class="fragment" -->
* Big $\mathcal{O}$ notation
<!-- .element: class="fragment" -->

---

<!-- .slide: data-auto-animate -->
## Goal

**formally** define an algorithm

--

<!-- .slide: data-auto-animate -->
## Goal

understand how we *compare* the

performance of **different** algorithms

--

<!-- .slide: data-auto-animate -->
## Goal

Counting *fundamental operations*

Performance for different *cases*
<!-- .element: class="fragment" -->

*Run-time complexity* as a function of problem size
<!-- .element: class="fragment" -->

--

## How Good is an Algorithm?
<!-- .element: class="fragment" -->

> in plain English...

Note: Knowing how to compare algorithms is important so you can make sure you are 
using the correct one for the job at hand!

It would be very useful information if you could tell that sorting 
algorithm a is expected to take x amount of time to sort products on your
website vs. algorithm b that is expected to take x*x

--

<!-- .slide: data-auto-animate -->

## Time and Space

Time complexity ; How *long* does it take to run?
<!-- .element: class="fragment" -->

Space complexity ; How much *memory* does it need?
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->

## Time and Space

Often a trade-off!

Note:
Typically this is a trade-off, where algorithms that reduce time complexity 
may increase the space complexity, and vice versa.

--

## Time complexity

We will focus on how long an algorithm takes to run!

Note: In your next year - you will explore in more depth!

---

<!-- .slide: data-auto-animate -->
## What is an Algorithm?

An algorithm is a finite **sequence** of unambiguous **instructions** for 
solving a **problem**, that will always **terminate**.

Note: A reminder of a formal definition of an algorithm.
Emphasise, always correct, and always terminate.
Etymology <https://www.britannica.com/biography/al-Khwarizmi>

--

<!-- .slide: data-auto-animate -->
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

<!-- .slide: data-auto-animate -->

#### Developing Algorithms 

> The first level of understanding is the human one. 
> You should be able to explain in plain terms how the algorithm works.

--

<!-- .slide: data-auto-animate -->

#### Developing Algorithms

> The second level is a more detailed, but still informal description, 
> that breaks the problem down into sub-problems.

Note: some algorithms may deal with problems 
too trivial to significantly break down.

--

<!-- .slide: data-auto-animate -->

#### Developing Algorithms

> The third level is a detailed pseudo code description, with all stages 
> refined until the description is unambiguous.

--

<!-- .slide: data-auto-animate -->

#### Developing Algorithms

### *There is often more than one solution!*

Note: It's worth stating...there may be more than one solution!

--

## Writing Pseudocode

There is no universally accepted pseudocode.
<!-- .element: class="fragment" -->

It *should* be language independent.
<!-- .element: class="fragment" -->

Note: We will relax that rule to enable runnable code in the labs!
I don't want you to learn another language...

--

<div class="left-center">

`pseudocode`

```text
scanArray(array[1..n], key): boolean
    for i := 1 to n
        if key == array[i]
        return true
    return false
```

</div> 
<div class="right-center">

`python`

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

1. *Specification*
    - return true if key is in array of $n$ values, else false
<!-- .element: class="fragment" -->

2. *Input*
    - array of size $n$,  element key
<!-- .element: class="fragment" -->

3. *Output*
    - boolean - true if key is found in array, else false
<!-- .element: class="fragment" -->


Note: What do I mean by values? What do I mean by a key?
We will just use integers for our example, but items could be any type.

--

### Informal Algorithm

See if we can find an item in a list that matches a key...

--

### Informal Algorithm

- Step through all items.
     - If we find a match, return true
<!-- .element: class="fragment" -->
     - Return false if not found.
<!-- .element: class="fragment" -->

--

### Formal Algorithm

<div style="font-size: 1.85em;">

```text
scanArray(array[1..n], key): boolean
    for i := 1 to n
        if key == array[i]
        return true
    return false
```

</div>

---

# Question?

## How long will this algorithm take to run?
<!-- .element: class="fragment" -->

Note: So, the BIG question is... how long does it take to run...

--

<!-- .slide: data-auto-animate -->

## Experimental Approach

![timer](../assets/img/clock.gif)

Note: Run the code, and use a stop watch...

--

<!-- .slide: data-auto-animate -->

## Experimental Approach

* A large sample of inputs.
<!-- .element: class="fragment" -->
* System time for each run.
<!-- .element: class="fragment" -->
* Plot the results.
<!-- .element: class="fragment" -->

--

![linear scan](../assets/img/lin_scan_experiment.png)

Note: What can we say about this plot? 
How will this algorithm perform on your machine?

--

<!-- .slide: data-auto-animate -->
### Challenges of Experimental Analysis

The machine the algorithm is being run on.
<!-- .element: class="fragment" -->

Multiple runs on the same hardware may be different.
<!-- .element: class="fragment" -->

There may be other processes running.
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
### Challenges of Experimental Analysis

A limited set of test inputs.
<!-- .element: class="fragment" -->

An algorithm must be fully implemented.
<!-- .element: class="fragment" -->

Note:  
Experiments can be done only on a limited set of test inputs
 (and these inputs may be important).

An algorithm must be fully implemented in order to  study its running time experimentally.

---

<!-- .slide: data-auto-animate -->
### Moving Beyond Experimental Analysis

--

<!-- .slide: data-auto-animate -->
### Moving Beyond Experimental Analysis

Take an approach that allows us to...

* gain independence of hardware
<!-- .element: class="fragment" -->
* no need for implementation
<!-- .element: class="fragment" -->
* all possible inputs
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
### Time complexity

<div style="font-size: 1.85em;">

```text
scanArray(array[1..n], key): boolean
    for i := 1 to n
        if key == array[i]
        return true
    return false
```

</div>

Note: let's just remind ourselves of the pseudo code...

--

<!-- .slide: data-auto-animate -->
### Time complexity

1. The size of the input array (i.e. size of $n$).
2. Where element `key` is within the array (if at all).

Note: we want to define the time complexity using only these factors

--

<!-- .slide: data-auto-animate -->
### Time complexity

We count the **fundamental operations** that are performed.

>These will be the same over multiple runs on any hardware 
>thus making comparisons between algorithms more informative.
<!-- .element: class="fragment" -->

--

### operations

<div style="font-size: 1.2em">

```text
loop:
    initialisation: i := 1
    comparison: i <= n
    update: i := i + 1

inside loop:
    key == array[i]
    return

after loop:
    return
```

</div>

--

To reiterate, we assess the time an algorithm takes

i.e. its *time complexity*

by counting the number of operations it performs.

--

We could include all operations...

but many are one-off and incidental to the overall runtime.
<!-- .element: class="fragment" -->

Note: I have already forgotten what all those operations were...

--

Therefore we choose a *fundamental operation* and **characterise** the 
algorithm by counting these fundamental operations.

Note: the time taken to execute a fundamental operation must 
be (approximately) the same whenever that operation is executed 
on any instance on the domain of an algorithm. Independent of the machine...

--

<!-- .slide: data-auto-animate -->
#### Which operations do we count?

<div style="font-size: 1.2em">

```text[ | 7]
loop:
    initialisation: i := 1
    comparison: i <= n
    update: i := i + 1

inside loop:
    key == array[i]
    return

after loop:
    return
```

</div>

--

<!-- .slide: data-auto-animate -->
#### Which operations do we count?

we will only count the operation at the heart of the algorithm.

---

<!-- .slide: data-auto-animate -->
### Fundamental Operation

## `key == array[i]`

Note: this is a comparison... 
a comparison is often the fundamental operation in many 
sorting and searching algorithms

--

<!-- .slide: data-auto-animate -->
### Fundamental Operation

## How many times is the fundamental operation performed?

Note: we have defined the fundamental op, now how do we count...

--

<!-- .slide: data-auto-animate -->
### Fundamental Operation

**Two** things to consider...

**Size** of the input array
<!-- .element: class="fragment" -->

**Where** is ` key ` in the array
<!-- .element: class="fragment" -->


Note:
Remember I said we have 2 things to consider?
We want to find the number of ops for any value of n
e.g. not 6 or 12, but relative (e.g. n operations, or n*n, etc.)

There are different cases. 
This algorithm would be much faster if e is the first element 
(best case scenario is 1 operation) 
than if e isn’t in the array at all (worst case scenario is n operations)

--

<!-- .slide: data-auto-animate -->
### Counting Fundamental Operations

Where ` key ` is in the array decides the **case**.
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
### Counting Fundamental Operations

operation   | count      | case
----------- | ---------- | --------
`key == array[1]`  | op is called once      | **best** case
`key == array[2]`  | op is called twice     |
 |...| 
`key == array[n]`  | op is called $n$ times | **worst** case

--

Generally, we assume the **worst** case.

`key == array[i]` is performed **$n$** times.
<!-- .element: class="fragment" -->


Note:
Unless specifically asked to consider a different case... 
It makes sense to prepare for the worst so you know your algorithm 
will at least always work to a certain level even under the most 
pessimistic circumstances.

So in this case, the worst case is that if key==a[i] will be performed n times

--

### Why Assume the Worst Case?

> In good weather, a commercial airliner requires 150,000$l$ of fuel to cross the Atlantic ocean.
<!-- .element: class="fragment" -->

> In poor weather, it requires 200,000$l$ of fuel.
<!-- .element: class="fragment" -->

> In *most* circumstances it is unacceptable for an algorithm to fail.
<!-- .element: class="fragment" -->

Note: We can compare different cases, but prepare for the worst 
to guarantee the minimum that the algorithm can achieve.

---

## What actually **is** the worst case?

For all possible outcomes...
<!-- .element: class="fragment" -->

which outcome results in the most work being carried out?
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->

### Linear Scan Time Complexity Function

## $$ t(n) = n $$

$t(n)$ is called the run time complexity function
<!-- .element: class="fragment" -->

Note: this is a measure of time not in seconds, 
but in terms of number of operations!

--

<!-- .slide: data-auto-animate -->
## $$ t(n) = n $$

We have **characterised** our function for the *worst* case.

Note: We have ignored constants from incidental operations.

--

<!-- .slide: data-auto-animate -->
## $$ t(n) = n $$

We call this a *linear* time algorithm.

We say this is *order* **$n$**, or...
<!-- .element: class="fragment" -->

### $$\mathcal{O}(n)$$
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
### Big $\mathcal{O}$ Notation

--

<!-- .slide: data-auto-animate -->
### Big $\mathcal{O}$ Notation

...is used to describe an *asymptotic* upper bound

> An *asymptote* is a line that a curve approaches, as it heads towards infinity
<!-- .element: class="fragment" -->

--

<!-- .slide: data-auto-animate -->
### Big $\mathcal{O}$ Notation

$$\begin{aligned}
& f(n)  \text{ is }  \mathcal{O}(g(n))  \newline
& \iff \text{ for constants  } ~ c, ~ n_0 \newline
& f(n) \leq cg(n) \text{ for all } n \geq n_0
\end{aligned}$$

Note: More formally...if and only if, but don't worry about this one!
But, it does qualify that the condition applies for sufficiently large n.

--

<!-- .slide: data-auto-animate -->
### Big $\mathcal{O}$ Notation

![big O notation](../assets/diag/big-o-graph.drawio.svg)

$f(n) = \mathcal{O}(g(n))$

--

## $\Omega$

Just like $\mathcal{O}$ describes an *upper* bound, 

$\Omega$ describes a *lower* bound.

Note: BIG Omega...

--

## $\Theta$

If we have upper and lower bounds

described by $\mathcal{O}$ and $\Omega$

$\Theta$ describes the set of functions *between* those bounds.

Note: BIG Theta...

---

#### Comparing Complexity Functions

<div style="font-size:0.8em">

| **character** | **function**      | **speed**  |
|----|----|:----:|
| constant      | $t(n) = c$        |  fastest   |
| logarithmic   | $t(n) = log(n)$   |$\Uparrow$  |
| linear        | $t(n) = n$        |            |
| log linear    | $t(n) = n~log(n)$ |            |
| polynomial    | $t(n) = n^k$      |            |
| exponential   | $t(n) = 2^n$      |$\Downarrow$|
| factorial     | $t(n) = n!$       |  slowest   |

</div>

Note: fastest and slowest always require sufficiently large n...
By the time we get to exponential, we should be thinking of a different algorithm!

--

<!-- .slide: data-auto-animate -->
#### Constant  Logarithmic  Linear

Regardless the size of $n$ 

*constant* algorithms finish in the **same** time.

--

<!-- .slide: data-auto-animate -->
#### Constant  Logarithmic  Linear

$$\begin{aligned}
2^k =& ~n  \newline
k   =& ~log_{2}(n)
\end{aligned}$$

Note: a quick reminder that logs *are* exponents...
we always assume log base 2 unless clearly stated otherwise 

--

<!-- .slide: data-auto-animate -->
#### Constant  Logarithmic  Linear

$$\begin{aligned}
2^k =& ~n  \newline
k   =& ~log_{2}(n)
\end{aligned}$$

$\therefore$ if $n$ doubles, $t(n)$ increases by 1

Note: a quick reminder that logs *are* exponents...
so logarithmic growth is less than linear

--

<!-- .slide: data-auto-animate -->
#### Constant  Logarithmic  Linear

linear algorithms grow at the same rate as $n$

--

![comparing algoritms](../assets/img/complexity.png)

--

<div style="font-size:0.7em">

| $n$ | $O(1)$ | $O(log(n))$ | $O(n)$ | $O(n log(n))$ | $O(n^2)$ | $O(2^n)$ | $O(n!)$ |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| $  8$ | $1$ | $2.079$ | $  8$ | $16.636$  | $64$    | $  256$              | $40320$|
| $ 16$ | $1$ | $2.773$ | $ 16$ | $44.361$  | $256$   | $65536$              | $2.092\times10^{13}$|
| $ 32$ | $1$ | $3.466$ | $ 32$ | $110.904$	| $1024$  | $4.295\times10^{9}$  | $2.631\times10^{35}$|
| $ 64$ | $1$ | $4.159$ | $ 64$ | $266.169$	| $4096$  | $1.845\times10^{19}$ | $1.269\times10^{89}$|
| $128$ | $1$ | $4.852$ | $128$ | $621.060$	| $16384$ | $3.403\times10^{38}$ | $3.856\times10^{215}$|
| $256$ | $1$ | $5.545$ | $256$ | $1419.565$| $65536$ | $1.158\times10^{77}$ | $8.578\times10^{506}$|

</div>

Note: let me draw your attention to the rightmost column...

--

## Some BIG numbers

--

<!-- .slide: data-auto-animate -->

if 1 fundamental operation takes 1 millisecond... 

$n = 8$

$40320 \approx 40s$

Note: for n = 8

--

<!-- .slide: data-auto-animate -->

if 1 fundamental operation takes 1 millisecond...

$n = 16$

$2.092\times10^{13} \approx 630 \text{ years}$

Note: for n = 16

--

<!-- .slide: data-auto-animate -->

if 1 fundamental operation takes 1 millisecond...

$n = 32$

$2.631\times10^{35} \approx 8 ~ septillion \text{ years}$

Note: for n = 32

--

<!-- .slide: data-auto-animate -->

if 1 fundamental operation takes 1 millisecond...

$n = 32$

$2.631\times10^{35} \approx 8 ~ septillion \text{ years}$

$8,555,783,709,787,818,000,000,000 \text{ years}$

Note: for n = 32

A very rough estimate of 10 trillion galaxies in the the visible universe. 
Multiplied by the Milky Way's estimated 100 billion stars results 
in 1 septillion stars. Although this is likely an underestimate.

---

<!-- .slide: data-auto-animate -->
### *Recap* : Assessing an Algorithm

--

<!-- .slide: data-auto-animate -->
### *Recap* : Assessing an Algorithm

#### Determine the fundamental operation

Note:
It is not usually necessary to count all operations, 
just choose the operation at the heart of the algorithm.

We assess algorithms by identifying fundamental operations and
counting them for any given input size

--

<!-- .slide: data-auto-animate -->
### *Recap* : Assessing an Algorithm

#### Determine the fundamental operation

#### Determine the case

Note:
The algorithm may take different amounts of time under different circumstances.
Consider all cases, but, unless instructed otherwise, assess the worst case.

The number of ops may vary depending on the input 
(ordering of the data affects linear scan, for example)

--

<!-- .slide: data-auto-animate -->
### *Recap* : Assessing an Algorithm

#### Determine the fundamental operation

#### Determine the case

#### Form the runtime complexity function

Note: For the selected case, count the fundamental operations.

--

<!-- .slide: data-auto-animate -->
### *Recap* : Assessing an Algorithm

#### Determine the fundamental operation

#### Determine the case

#### Form the runtime complexity function

#### Characterise the runtime complexity function.

Note: Let's look at some more examples next time.

---

# Summary

* Defining and Developing Algorithms
<!-- .element: class="fragment" -->
* Experimental Analysis
<!-- .element: class="fragment" -->
* Analytic Characterisation
<!-- .element: class="fragment" -->
* Big $\mathcal{O}$ notation
<!-- .element: class="fragment" -->

--

# Questions?

--

# Thank you
