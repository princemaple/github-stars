---
project: otp
stars: 12036
description: Erlang/OTP
url: https://github.com/erlang/otp
---

Erlang/OTP
==========

**Erlang** is a programming language and runtime system for building massively scalable soft real-time systems with requirements on high availability.

**OTP** is a set of Erlang libraries, which consists of the Erlang runtime system, a number of ready-to-use components mainly written in Erlang, and a set of design principles for Erlang programs. Learn more about Erlang and OTP.

Learn how to program in Erlang.

Examples
--------

There are several examples on the website to help you get started. The below example defines a function `world/0` that prints "Hello, world" in the Erlang shell:

\-module(hello).
-export(\[world/0\]).

world() \-> io:format("Hello, world\\n").

Save the file as `hello.erl` and run `erl` to enter the Erlang shell to compile the module.

Erlang/OTP 24 \[erts-12.2\] \[source\] \[64-bit\] \[smp:8:8\] \[ds:8:8:10\] \[async-threads:1\] \[jit\]

Eshell V12.2  (abort with ^G)
1> c(hello).
{ok,hello}
2> hello:world().
Hello, world
ok

Learn more about the Erlang syntax of modules, functions and expressions on Erlang.org.

Installation
------------

### Binary Distributions

Erlang/OTP is available as pre-built binary packages by most OS package managers.

apt-get install erlang

### Compiling from source

To compile Erlang from source, run the following commands. The complete building and installation instructions can be found here.

git clone https://github.com/erlang/otp.git
cd otp

Checkout the branch or tag of your choice

git checkout maint-27    # current latest stable version

Configure, build and install

./configure
make
make install

Alternatively, you can use Kerl, a script that lets you easily build Erlang with a few commands.

Bug Reports
-----------

Please visit our GitHub Issues page for reporting bugs. The instructions for submitting bugs reports can be found here.

### Security Disclosure

Please do not report security vulnerabilities through public channels, like GitHub issues, discussions, or pull requests.

Please disclose the security issues following our SECURITY guidelines.

Contributing
------------

We are grateful to the community for contributing bug fixes and improvements. Read below to learn how you can take part in improving Erlang/OTP. We appreciate your help!

### Contribution Guide

Read our contribution guide to learn about our development process, how to propose fixes and improvements, and how to test your changes to Erlang/OTP before submitting a pull request.

### Help Wanted

We have a list of Help Wanted bugs that we would appreciate external help from the community. This is a great place to get involved.

Awesome-Erlang
--------------

You can find more projects, tools and articles related to Erlang/OTP on the awesome-erlang list. Add your project there.

License
-------

Erlang/OTP is released under the Apache License 2.0.

For any license inquiry, please send an email to opensource@ericsson.com

> %CopyrightBegin%
> 
> SPDX-License-Identifier: Apache-2.0
> 
> Copyright Ericsson AB 2010-2025. All Rights Reserved.
> 
> Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at
> 
> ```
> http://www.apache.org/licenses/LICENSE-2.0
> ```
> 
> Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
> 
> %CopyrightEnd%
