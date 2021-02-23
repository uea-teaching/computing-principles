# Computing Principles

This module segment covers introductory computing principles. 


## Lectures

The material is presented as a series of lectures and some code examples.

The online lectures are available [here](https://uea-teaching.github.io/computing-principles/).

I will make the slides available online *and* I will try to keep this material low-bandwidth.


## Viewing offline

If you want to view the slides offline, 
clone this repository and cd to the lectures directory.

Run a local http server:

    python -m http.server

The slides can then be viewed at `http://localhost:8000`


## PDF

I discourage printing of the slides. 
If you want a static pdf version of the slides I recommend, 
and use, [decktape](https://github.com/astefanutti/decktape).

> I also recommend using the docker image provided at the link.

For example, to generate a pdf file of the first analysis lecture:

    decktape reveal  \
        --size 1600x900 \
        https://uea-teaching.github.io/computing-principles/lectures/analysis1 \
        analysis1.pdf
