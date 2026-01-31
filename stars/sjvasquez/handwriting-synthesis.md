---
project: handwriting-synthesis
stars: 4707
description: Handwriting Synthesis with RNNs ✏️
url: https://github.com/sjvasquez/handwriting-synthesis
---

Handwriting Synthesis
=====================

Implementation of the handwriting synthesis experiments in the paper Generating Sequences with Recurrent Neural Networks by Alex Graves. The implementation closely follows the original paper, with a few slight deviations, and the generated samples are of similar quality to those presented in the paper.

Web demo is available here.

Usage
-----

lines \= \[
    "Now this is a story all about how",
    "My life got flipped turned upside down",
    "And I'd like to take a minute, just sit right there",
    "I'll tell you how I became the prince of a town called Bel-Air",
\]
biases \= \[.75 for i in lines\]
styles \= \[9 for i in lines\]
stroke\_colors \= \['red', 'green', 'black', 'blue'\]
stroke\_widths \= \[1, 2, 1, 2\]

hand \= Hand()
hand.write(
    filename\='img/usage\_demo.svg',
    lines\=lines,
    biases\=biases,
    styles\=styles,
    stroke\_colors\=stroke\_colors,
    stroke\_widths\=stroke\_widths
)

Currently, the `Hand` class must be imported from `demo.py`. If someone would like to package this project to make it more usable, please contribute.

A pretrained model is included, but if you'd like to train your own, read these instructions.

Demonstrations
--------------

Below are a few hundred samples from the model, including some samples demonstrating the effect of priming and biasing the model. Loosely speaking, biasing controls the neatness of the samples and priming controls the style of the samples. The code for these demonstrations can be found in `demo.py`.

### Demo #1:

The following samples were generated with a fixed style and fixed bias.

**Smash Mouth – All Star (lyrics)**

### Demo #2

The following samples were generated with varying style and fixed bias. Each verse is generated in a different style.

**Vanessa Carlton – A Thousand Miles (lyrics)**

### Demo #3

The following samples were generated with a fixed style and varying bias. Each verse has a lower bias than the previous, with the last verse being unbiased.

**Leonard Cohen – Hallelujah (lyrics)**

Contribute
----------

This project was intended to serve as a reference implementation for a research paper, but since the results are of decent quality, it may be worthwile to make the project more broadly usable. I plan to continue focusing on the machine learning side of things. That said, I'd welcome contributors who can:

-   Package this, and otherwise make it look more like a usable software project and less like research code.
-   Add support for more sophisticated drawing, animations, or anything else in this direction. Currently, the project only creates some simple svg files.
