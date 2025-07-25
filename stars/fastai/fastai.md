---
project: fastai
stars: 27219
description: The fastai deep learning library
url: https://github.com/fastai/fastai
---

Welcome to fastai
=================

Installing
----------

You can use fastai without any installation by using Google Colab. In fact, every page of this documentation is also available as an interactive notebook - click “Open in colab” at the top of any page to open it (be sure to change the Colab runtime to “GPU” to have it run fast!) See the fast.ai documentation on Using Colab for more information.

You can install fastai on your own machines with conda (highly recommended), as long as you’re running Linux or Windows (NB: Mac is not supported). For Windows, please see the “Running on Windows” for important notes.

We recommend using miniconda (or miniforge). First install PyTorch using the conda line shown here, and then run:

conda install fastai::fastai

To install with pip, use: `pip install fastai`.

If you plan to develop fastai yourself, or want to be on the cutting edge, you can use an editable install (if you do this, you should also use an editable install of fastcore to go with it.) First install PyTorch, and then:

```
git clone https://github.com/fastai/fastai
pip install -e "fastai[dev]"
```

Learning fastai
---------------

The best way to get started with fastai (and deep learning) is to read the book, and complete the free course.

To see what’s possible with fastai, take a look at the Quick Start, which shows how to use around 5 lines of code to build an image classifier, an image segmentation model, a text sentiment model, a recommendation system, and a tabular model. For each of the applications, the code is much the same.

Read through the Tutorials to learn how to train your own models on your own datasets. Use the navigation sidebar to look through the fastai documentation. Every class, function, and method is documented here.

To learn about the design and motivation of the library, read the peer reviewed paper.

About fastai
------------

fastai is a deep learning library which provides practitioners with high-level components that can quickly and easily provide state-of-the-art results in standard deep learning domains, and provides researchers with low-level components that can be mixed and matched to build new approaches. It aims to do both things without substantial compromises in ease of use, flexibility, or performance. This is possible thanks to a carefully layered architecture, which expresses common underlying patterns of many deep learning and data processing techniques in terms of decoupled abstractions. These abstractions can be expressed concisely and clearly by leveraging the dynamism of the underlying Python language and the flexibility of the PyTorch library. fastai includes:

-   A new type dispatch system for Python along with a semantic type hierarchy for tensors
-   A GPU-optimized computer vision library which can be extended in pure Python
-   An optimizer which refactors out the common functionality of modern optimizers into two basic pieces, allowing optimization algorithms to be implemented in 4–5 lines of code
-   A novel 2-way callback system that can access any part of the data, model, or optimizer and change it at any point during training
-   A new data block API
-   And much more…

fastai is organized around two main design goals: to be approachable and rapidly productive, while also being deeply hackable and configurable. It is built on top of a hierarchy of lower-level APIs which provide composable building blocks. This way, a user wanting to rewrite part of the high-level API or add particular behavior to suit their needs does not have to learn how to use the lowest level.

Migrating from other libraries
------------------------------

It’s very easy to migrate from plain PyTorch, Ignite, or any other PyTorch-based library, or even to use fastai in conjunction with other libraries. Generally, you’ll be able to use all your existing data processing code, but will be able to reduce the amount of code you require for training, and more easily take advantage of modern best practices. Here are migration guides from some popular libraries to help you on your way:

-   Plain PyTorch
-   Ignite
-   Lightning
-   Catalyst

Windows Support
---------------

Due to python multiprocessing issues on Jupyter and Windows, `num_workers` of `Dataloader` is reset to 0 automatically to avoid Jupyter hanging. This makes tasks such as computer vision in Jupyter on Windows many times slower than on Linux. This limitation doesn’t exist if you use fastai from a script.

See this example to fully leverage the fastai API on Windows.

We recommend using Windows Subsystem for Linux (WSL) instead – if you do that, you can use the regular Linux installation approach, and you won’t have any issues with `num_workers`.

Tests
-----

To run the tests in parallel, launch:

`nbdev_test`

For all the tests to pass, you’ll need to install the dependencies specified as part of dev\_requirements in settings.ini

`pip install -e .[dev]`

Tests are written using `nbdev`, for example see the documentation for `test_eq`.

Contributing
------------

After you clone this repository, make sure you have run `nbdev_install_hooks` in your terminal. This install Jupyter and git hooks to automatically clean, trust, and fix merge conflicts in notebooks.

After making changes in the repo, you should run `nbdev_prepare` and make additional and necessary changes in order to pass all the tests.

Docker Containers
-----------------

For those interested in official docker containers for this project, they can be found here.
