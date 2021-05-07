# Jupyter

Dr. David Greenwood

david.greenwood@uea.ac.uk

Room SCI 2.16a

---

> The name Jupyter, is inspired by the programming languages **Ju**lia, **Py**thon and **R**.

> from an [article](https://www.nature.com/articles/d41586-018-07196-1) on nature.com

Note:
Jupyter is a free, open-source, interactive web tool known as a computational notebook. 
Named jupyter according to co-founder Fernando Pérez

--

Jupyter Notebooks consist of two parts:

1. User input, in the form of a file read by a browser.
2. A computational **kernel**, either *local* or *remote*.

Note: The file extension ipynb infers ipython notebook.
The file is in fact legitimate JSON, and can be parsed as such. 

--

## Widgets

You can use widgets to build interactive GUIs for your notebooks.
<!-- .element: class="fragment" -->

Note:

Widgets are eventful python objects that have a representation in the browser, 
often as a control like a slider, textbox, etc.

https://github.com/jupyter-widgets/ipywidgets/blob/master/docs/source/examples/Widget%20Basics.ipynb

--

## Types of Widget

Most basic types have a corresponding widget.

There are *password*, *html* and *image* widgets...
<!-- .element: class="fragment" -->

...and **many** others.
<!-- .element: class="fragment" -->

--

<!-- .slide: data-background-image="../assets/img/sortie.jpg" -->

# Example

[notebook-widgets-1](https://github.com/uea-teaching/computing-principles/blob/main/notebooks/widget_basics.ipynb)

--

## Interact

Interact allows us to pass values from widgets to python functions.

Note:
At the most basic level, interact auto generates UI controls for function 
arguments, and then calls the function with those arguments when you 
manipulate the controls interactively. 
To use interact, you need to define a function that you want to explore.

--

<!-- .slide: data-background-image="../assets/img/exit.jpg" -->

# Example

[notebook-interact](https://github.com/uea-teaching/computing-principles/blob/main/notebooks/widget_interact.ipynb)

--

### Jupyter project blog

https://blog.jupyter.org

--

### IPython Cookbook

https://ipython-books.github.io

---

## Conclusion

Python shell
<!-- .element: class="fragment" -->
iPython
<!-- .element: class="fragment" -->
Jupyter widgets
<!-- .element: class="fragment" -->
