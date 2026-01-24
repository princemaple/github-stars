---
project: honey-potion
stars: 292
description: Writing eBPF programs with Elixir!
url: https://github.com/lac-dcc/honey-potion
---

🍯 Honey Potion - Writing eBPF with Elixir 🍯
=============================================

🐝 About
--------

**Honey Potion** is a framework that brings the power of **eBPF** to Elixir, allowing users to write Elixir code that is transformed into eBPF bytecode.

In this alpha version, Honey Potion translates Elixir code into a subset of C that leverages libbpf. The generated C code is then compiled using `clang` to produce the eBPF bytecode, which can be loaded into the kernel.

* * *

📦 Dependencies
---------------

Honey Potion requires the following dependencies, listed with their Ubuntu package names (equivalents exist for other distributions):

-   **Erlang & Elixir** – Required for running Honey Potion
-   **libbpf** – Version 1.1 (installation guide)
-   **gcc-multilib** – Required for certain C libraries (`asm/types.h`)
-   **make** – For Makefile-based compilation
-   **llvm** – Provides `llc`
-   **clang** – Required for compilation
-   **bpftool** – Used for skeleton generation

> ℹ️ **Note:** You can manually compile `clang`, `llc`, and `bpftool`, as long as they are available in your `$PATH`.

* * *

🎥 Video Guide
--------------

Prefer a video tutorial? Check out the Honey Potion YouTube playlist with step-by-step guides.

* * *

🚀 Installation
---------------

Add `honey` to your project's dependencies in `mix.exs`:

def deps do
  \[
    {:honey, git: "https://github.com/lac-dcc/honey-potion/", submodules: true}
  \]
end

* * *

📝 Usage
--------

When you `use Honey` in your module, it will be translated to C the next time you compile your project.

defmodule Minimal do
  use Honey, license: "Dual BSD/GPL"
  \# ...
end

This generates the following directories:

-   **`src/`** – Stores the generated C code (e.g., `Minimal.bpf.c`)
-   **`obj/`** – Stores compilation objects (e.g., `Minimal.o`)
-   **`bin/`** – Stores the final executable (e.g., `Minimal`)

To run your program, navigate to the `bin/` directory and execute the binary with appropriate privileges.

### 🔧 Command-line Options

-   `-p` → Prints all eBPF maps
-   `-t <seconds>` → Specifies the duration the program should run

#### 🎯 The `main/1` Function

Every module using `Honey` must define a `main/1` function that serves as the entry point for the eBPF program.

defmodule Example.Minimal do
  use Honey, license: "Dual BSD/GPL"

  @sec "tracepoint/syscalls/sys\_enter\_kill"
  def main(ctx) do
    \# ...
  end
end

-   `@sec` specifies the **program type** according to `libbpf`.
-   `ctx` is a struct whose fields vary depending on the program type.
-   The `main/1` function **must** return an integer; otherwise, a runtime exception is thrown.

For detailed documentation and examples, see:

-   `Language`
-   Example programs in `/examples`:
    -   `hello_world`
    -   `maps`
    -   `count_syscalls`
    -   `force_kill`

Or watch the YouTube tutorial.

* * *

⚠️ Runtime Exceptions
---------------------

As Elixir is a dynamically typed language, we simulate runtime exceptions when translating programs to eBPF.

In this Alpha version, if an exception occurs, it will be printed to the debug pipe, and the program will exit with status `0`.

* * *

🚧 Current Limitations
----------------------

Honey Potion is still in **Alpha**, and many features are still being developed. Some known limitations include:

-   **Pattern Matching:** No destructuring; `=` behaves like an assignment operator.
-   **Control Flow:** No `case` or `if-else` blocks (unless optimized out at compile time).
-   **Operators:** Limited to `+`, `-`, `*`, `/`, and `==`.
-   **Function Guards:** Not supported.
-   **Default Arguments:** Not supported.
-   **Recursion:** No mutual recursion support.
-   **Structs:** User-defined structs are not supported.
-   **Execution Requirements:** Executable must reside in `bin/`, and the object file must be in `obj/`.

We are actively working to improve Honey Potion. Stay tuned!

* * *

🤝 Contributing
---------------

Contributions are welcome! To avoid redundant work, please reach out before submitting major changes.

Feedback and suggestions are highly appreciated! You can:

-   Open a GitHub issue
-   Contact us at **kaelsoaresaugusto@gmail.com**

* * *

📜 License
----------

**Honey Potion** is maintained by the **Compilers Laboratory** at the **Federal University of Minas Gerais (UFMG), Brazil**.

This program is **free software** under the terms of the **GNU General Public License (GPLv3)**.

For details, see the full license: GNU GPL v3.

* * *
