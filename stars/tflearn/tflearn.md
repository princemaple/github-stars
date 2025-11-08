---
project: tflearn
stars: 9618
description: Deep learning library featuring a higher-level API for TensorFlow.
url: https://github.com/tflearn/tflearn
---

TFLearn: Deep learning library featuring a higher-level API for TensorFlow.
===========================================================================

TFlearn is a modular and transparent deep learning library built on top of Tensorflow. It was designed to provide a higher-level API to TensorFlow in order to facilitate and speed-up experimentations, while remaining fully transparent and compatible with it.

TFLearn features include:

-   Easy-to-use and understand high-level API for implementing deep neural networks, with tutorial and examples.
-   Fast prototyping through highly modular built-in neural network layers, regularizers, optimizers, metrics...
-   Full transparency over Tensorflow. All functions are built over tensors and can be used independently of TFLearn.
-   Powerful helper functions to train any TensorFlow graph, with support of multiple inputs, outputs and optimizers.
-   Easy and beautiful graph visualization, with details about weights, gradients, activations and more...
-   Effortless device placement for using multiple CPU/GPU.

The high-level API currently supports most of recent deep learning models, such as Convolutions, LSTM, BiRNN, BatchNorm, PReLU, Residual networks, Generative networks... In the future, TFLearn is also intended to stay up-to-date with latest deep learning techniques.

Note: Latest TFLearn (v0.5) is only compatible with TensorFlow v2.0 and over.

Overview
--------

\# Classification
tflearn.init\_graph(num\_cores\=8, gpu\_memory\_fraction\=0.5)

net \= tflearn.input\_data(shape\=\[None, 784\])
net \= tflearn.fully\_connected(net, 64)
net \= tflearn.dropout(net, 0.5)
net \= tflearn.fully\_connected(net, 10, activation\='softmax')
net \= tflearn.regression(net, optimizer\='adam', loss\='categorical\_crossentropy')

model \= tflearn.DNN(net)
model.fit(X, Y)

\# Sequence Generation
net \= tflearn.input\_data(shape\=\[None, 100, 5000\])
net \= tflearn.lstm(net, 64)
net \= tflearn.dropout(net, 0.5)
net \= tflearn.fully\_connected(net, 5000, activation\='softmax')
net \= tflearn.regression(net, optimizer\='adam', loss\='categorical\_crossentropy')

model \= tflearn.SequenceGenerator(net, dictionary\=idx, seq\_maxlen\=100)
model.fit(X, Y)
model.generate(50, temperature\=1.0)

There are many more examples available _here_.

Compatibility
-------------

TFLearn is based on the original tensorflow v1 graph API. When using TFLearn, make sure to import tensorflow that way:

```
import tflearn
import tensorflow.compat.v1 as tf
```

Installation
------------

**TensorFlow Installation**

TFLearn requires Tensorflow (version 2.0+) to be installed.

To install TensorFlow, simply run:

```
pip install tensorflow
```

or, with GPU-support:

```
pip install tensorflow-gpu
```

For more details see _TensorFlow installation instructions_

**TFLearn Installation**

To install TFLearn, the easiest way is to run

For the bleeding edge version (recommended):

pip install git+https://github.com/tflearn/tflearn.git

For the latest stable version:

pip install tflearn

Otherwise, you can also install from source by running (from source folder):

python setup.py install

-   For more details, please see the _Installation Guide_.

Getting Started
---------------

See _Getting Started with TFLearn_ to learn about TFLearn basic functionalities or start browsing _TFLearn Tutorials_.

Examples
--------

There are many neural network implementation available, see _Examples_.

Documentation
-------------

http://tflearn.org/doc\_index

Model Visualization
-------------------

**Graph**

**Loss & Accuracy (multiple runs)**

**Layers**

Contributions
-------------

This is the first release of TFLearn, if you find any bug, please report it in the GitHub issues section.

Improvements and requests for new features are more than welcome! Do not hesitate to twist and tweak TFLearn, and send pull-requests.

For more info: _Contribute to TFLearn_.

License
-------

MIT License
