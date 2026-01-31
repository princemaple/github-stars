---
project: python-fire
stars: 28082
description: Python Fire is a library for automatically generating command line interfaces (CLIs) from absolutely any Python object.
url: https://github.com/google/python-fire
---

Python Fire
===========

_Python Fire is a library for automatically generating command line interfaces (CLIs) from absolutely any Python object._

-   Python Fire is a simple way to create a CLI in Python. \[1\]
-   Python Fire is a helpful tool for developing and debugging Python code. \[2\]
-   Python Fire helps with exploring existing code or turning other people's code into a CLI. \[3\]
-   Python Fire makes transitioning between Bash and Python easier. \[4\]
-   Python Fire makes using a Python REPL easier by setting up the REPL with the modules and variables you'll need already imported and created. \[5\]

Installation
------------

To install Python Fire with pip, run: `pip install fire`

To install Python Fire with conda, run: `conda install fire -c conda-forge`

To install Python Fire from source, first clone the repository and then run: `python setup.py install`

Basic Usage
-----------

You can call `Fire` on any Python object:  
functions, classes, modules, objects, dictionaries, lists, tuples, etc. They all work!

Here's an example of calling Fire on a function.

import fire

def hello(name\="World"):
  return "Hello %s!" % name

if \_\_name\_\_ \== '\_\_main\_\_':
  fire.Fire(hello)

Then, from the command line, you can run:

python hello.py  # Hello World!
python hello.py --name=David  # Hello David!
python hello.py --help  # Shows usage information.

Here's an example of calling Fire on a class.

import fire

class Calculator(object):
  """A simple calculator class."""

  def double(self, number):
    return 2 \* number

if \_\_name\_\_ \== '\_\_main\_\_':
  fire.Fire(Calculator)

Then, from the command line, you can run:

python calculator.py double 10  # 20
python calculator.py double --number=15  # 30

To learn how Fire behaves on functions, objects, dicts, lists, etc, and to learn about Fire's other features, see the Using a Fire CLI page.

For additional examples, see The Python Fire Guide.

Why is it called Fire?
----------------------

When you call `Fire`, it fires off (executes) your command.

Where can I learn more?
-----------------------

Please see The Python Fire Guide.

Reference
---------

Setup

Command

Notes

install

`pip install fire`

Creating a CLI

Command

Notes

import

`import fire`

Call

`fire.Fire()`

Turns the current module into a Fire CLI.

Call

`fire.Fire(component)`

Turns `component` into a Fire CLI.

Using a CLI

Command

Notes

Help

`command --help` or `command -- --help`

REPL

`command -- --interactive`

Enters interactive mode.

Separator

`command -- --separator=X`

Sets the separator to `X`. The default separator is `-`.

Completion

`command -- --completion [shell]`

Generates a completion script for the CLI.

Trace

`command -- --trace`

Gets a Fire trace for the command.

Verbose

`command -- --verbose`

_Note that these flags are separated from the Fire command by an isolated `--`._

License
-------

Licensed under the Apache 2.0 License.

Disclaimer
----------

This is not an official Google product.
