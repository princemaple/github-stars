---
project: red
stars: 5976
description: Red is a next-generation programming language strongly inspired by Rebol, but with a broader field of usage thanks to its native-code compiler, from system programming to high-level scripting and cross-platform reactive GUI, while providing modern support for concurrency, all in a zero-install, zero-config, single ~1MB file! 
url: https://github.com/red/red
---

Red Programming Language
========================

**Red** is a programming language strongly inspired by Rebol, but with a broader field of usage thanks to its native-code compiler, from system programming to high-level scripting, while providing modern support for concurrency and multi-core CPUs.

Red tackles the software building complexity using a DSL-oriented approach (we call them _dialects_) . The following dialects are built-in:

-   Red/System: a C-level system programming language compiled to native code
-   Parse: a powerful PEG parser
-   VID: a simple GUI layout creation dialect
-   Draw: a vector 2D drawing dialect
-   Rich-text: a rich-text description dialect

Red has its own complete cross-platform toolchain, featuring an encapper, a native compiler, an interpreter, and a linker, not depending on any third-party library, except for a Rebol2 interpreter, required during the alpha stage. Once 1.0 is reached, Red will be self-hosted. Currently, Red is still at alpha stage and 32-bit only.

Red's main features are:

-   Human-friendly syntax
-   Homoiconic (Red is its own meta-language and own data-format)
-   Functional, imperative, reactive and symbolic programming
-   Prototype-based object support
-   Multi-typing
-   Powerful pattern-matching Macros system
-   Rich set of built-in datatypes (50+)
-   Both statically and JIT-compiled(\*) to native code
-   Cross-compilation done right
-   Produces executables of less than 1MB, with no dependencies
-   Concurrency and parallelism strong support (actors, parallel collections)(\*)
-   Low-level system programming abilities through the built-in Red/System DSL
-   Powerful PEG parser DSL built-in
-   Fast and compacting Garbage Collector
-   Instrumentation built-in for the interpreter, lexer and parser.
-   Cross-platform native GUI system, with a UI layout DSL and a drawing DSL
-   Bridging to the JVM
-   High-level scripting and REPL GUI and CLI consoles included
-   Visual Studio Code plugin, with many helpful features
-   Highly embeddable
-   Low memory footprint
-   Single-file (~1MB) contains whole toolchain, full standard library and REPL (\*\*)
-   No install, no setup
-   Fun guaranteed!

(\*) Not implemented yet. (\*\*) Temporarily split in two binaries

More information at red-lang.org.

Running the Red REPL
====================

Download a GUI or CLI console binary suitable for your operating system, rename it at your convenience, then run it from shell or by double-clicking on it (Windows). You should see the following output:

```
    ---== Red 0.6.5 ==--
    Type HELP for starting information.

    >>
```

A simple Hello World would look like:

```
    >> print "Hello World!"
    Hello World!
```

If you are on the GUI console, a GUI Hello World (prompt omitted):

```
    view [text "Hello World!"]
```

A more sophisticated example that retrieves the last commits from this repo and displays their log messages in a scrollable list:

```
    view [
        text-list data collect [
            foreach event load https://api.github.com/repos/red/red/commits [
                keep event/commit/message
            ]
        ]
    ]
```

Note: check also the following improved version allowing you to click on a given commit log and open the commit page on github.

You can now head to see and try some showcasing scripts here and there. You can run those examples from the console directly using Github's "raw" link. E.g.:

```
    >> do https://raw.githubusercontent.com/red/code/master/Showcase/calculator.red
```

Note: If you are using the Wine emulator, it has some issues with the GUI-Console. Install the `Consolas` font to fix the problem.

Generating a standalone executable
==================================

The Red toolchain comes as a single executable file that you can download for the big-3 platforms (32-bit only for now). Rename the file to `redc` (or `redc.exe` under Windows).

1.  Put the downloaded **redc** binary in the working folder.
    
2.  In a code or text editor, write the following Hello World program:
    
    ```
     Red [
         Title: "Simple hello world script"
     ]
    
     print "Hello World!"
    ```
    
3.  Save it under the name: **hello.red**
    
4.  Generate a compiled executable from that program: (first run will pre-compile libRedRT library)
    
    ```
     $ redc -c hello.red
     $ ./hello
    ```
    
5.  Want to generate a compiled executable from that program with no dependencies?
    
    ```
     $ redc -r hello.red
     $ ./hello
    ```
    
6.  Want to cross-compile to another supported platform?
    
    ```
     $ redc -t Windows hello.red
     $ redc -t Darwin hello.red
     $ redc -t Linux-ARM hello.red
    ```
    

**The full command-line syntax is:**

```
redc [command] [options] [file]
```

`[file]` any Red or Red/System source file.

-   The -c, -r and -u options are mutually exclusive.

`[options]`

```
-c, --compile                  : Generate an executable in the working
                                 folder, using libRedRT. (development mode)

-d, --debug, --debug-stabs     : Compile source file in debug mode. STABS
                                 is supported for Linux targets.

-dlib, --dynamic-lib           : Generate a shared library from the source
                                 file.

-e, --encap                    : Compile in encap mode, so code is interpreted
                                 at runtime. Avoids compiler issues. Required
                                 for some dynamic code.

-h, --help                     : Output this help text.

-o <file>, --output <file>     : Specify a non-default [path/][name] for
                                 the generated binary file.

-r, --release                  : Compile in release mode, linking everything
                                 together (default: development mode).

-s, --show-expanded            : Output result of Red source code expansion by
                                 the preprocessor.

-t <ID>, --target <ID>         : Cross-compile to a different platform
                                 target than the current one (see targets
                                 table below).

-u, --update-libRedRT          : Rebuild libRedRT and compile the input script
                                  (only for Red scripts with R/S code).

-v <level>, --verbose <level>  : Set compilation verbosity level, 1-3 for
                                 Red, 4-11 for Red/System.

-V, --version                  : Output Red's executable version in x.y.z
                                 format.

--config [...]                 : Provides compilation settings as a block
                                 of `name: value` pairs.

--no-compress                  : Omit Redbin format compression.

--no-runtime                   : Do not include runtime during Red/System
                                 source compilation.

--no-view                      : Do not include VIEW module in the CLI console
                                 and the libRedRT.

--view <engine>                : Select the VIEW engine (native, terminal, GTK, test)

--red-only                     : Stop just after Red-level compilation.
                                 Use higher verbose level to see compiler
                                 output. (internal debugging purpose)

--show-func-map                : Output an address/name map of Red/System
                                 functions, for debugging purposes.
```

`[command]`

```
build libRed [stdcall]         : Builds libRed library and unpacks the
                                 libRed/ folder locally.

clear [<path>]                 : Delete all temporary files from current
                                 or target <path> folder.
```

Cross-compilation targets:

```
MSDOS        : Windows, x86, console (+ GUI) applications
Windows      : Windows, x86, GUI applications
WindowsXP    : Windows, x86, GUI applications, no touch API
Linux        : GNU/Linux, x86, console (+ GUI) applications
Linux-GTK    : GNU/Linux, x86, GUI only applications
Linux-musl   : GNU/Linux, x86, musl libc
Linux-ARM    : GNU/Linux, ARMv5, armel (soft-float)
RPi          : GNU/Linux, ARMv7, armhf (hard-float)
RPi-GTK      : GNU/Linux, ARMv7, armhf (hard-float), GUI only applications
Pico         : GNU/Linux, ARMv7, armhf (hard-float), uClibc
Darwin       : macOS Intel, console-only applications
macOS        : macOS Intel, applications bundles
Syllable     : Syllable OS, x86
FreeBSD      : FreeBSD, x86
NetBSD       : NetBSD, x86
Android      : Android, ARMv5
Android-x86  : Android, x86
```

_Note_: The toolchain executable (`redc.exe`) relies on Rebol encapper which does not support being run from a location specified in `PATH` environment variable and you get `PROGRAM ERROR: Invalid encapsulated data` error. If you are on Windows try using PowerShell instead of CMD. You can also provide the full path to the executable, put a copy of it in your working folder or wrap a shell script (see relevant tickets: #543 and #1547).

Running Red from the sources (for contributors)
===============================================

The compiler and linker are currently written in Rebol. Please follow the instructions for installing the compiler toolchain in order to run it from sources:

1.  Clone this git repository or download an archive (`ZIP` button above or from tagged packages).
    
2.  Download a Rebol interpreter suitable for your OS: Windows, Linux (or Linux), Mac OS X, FreeBSD, OpenBSD, Solaris.
    
3.  Extract the `rebol` binary, put it in the root folder, that's all!
    
4.  Let's test it: run `./rebol`, you'll see a `>>` prompt appear. Windows users need to double-click on the `rebol.exe` file to run it.
    
5.  From the REBOL console type:
    
    ```
     >> do/args %red.r "%tests/hello.red"
    ```
    

The compilation process should finish with a `...output file size` message. The resulting binary is in the working folder. Windows users need to open a DOS console and run `hello.exe` from there.

You can compile the Red console from source:

```
    >> do/args %red.r "-r %environment/console/CLI/console.red"
```

To compile the Windows GUI console from source:

```
    >> do/args %red.r "-r -t Windows %environment/console/GUI/gui-console.red"
```

Note: the `-c` argument is not necessary when launching the Red toolchain from sources, as the default action is to compile the input script (the toolchain in binary form default action is to run the input script through the interpreter). The `-r` argument is needed when compiling the Red console to make additional runtime functions available.

Note: The red git repository does not include a `.gitignore` file. If you run the automated tests, several files will be created that are not stored in the repository. Installing and renaming a copy of `.git/.gitignore-sample` file will ignore these generated files.

Contributing
============

If you want to contribute code to the Red project be sure to read the guidelines first.

It is usually a good idea to inform the Red team about what changes you are going to make in order to ensure that someone is not already working on the same thing. You can reach us through our chat room.

Satisfied with the results of your change and want to issue a pull request on Github?

Make sure the changes pass all the existing tests, add relevant tests to the test-suite, and please test on as many platforms as you can. You can run all the tests using (from Rebol console, at repository root):

```
    >> do %run-all-tests.r
```

Git integration with console built from sources
===============================================

If you want git version included in your Red console built from sources, use this command:

call/show ""                                              ;-- patch call bug on Windows
save %build/git.r do %build/git-version.r                 ;-- lookup git version if available
do/args %red.r "-r %environment/console/CLI/console.red"  ;-- build Console
write %build/git.r "none^/"                               ;-- restore git repo status

Anti-virus false positive
=========================

Some anti-virus programs are a bit too sensitive and can wrongly report an alert on some binaries generated by Red (see here for the details). If that happens to you, please report it to your anti-virus vendor as a false positive.

One known way to reduce the false flagging from anti-viruses is to use the `--no-compress` option when compiling Red binaries. That will prevent the internal Rebin data to be compressed using our CRUSH compressor, reducing that file section entropy.

License
=======

Both Red and Red/System are published under BSD license, runtime is under BSL license. BSL is a bit more permissive license than BSD, more suitable for the runtime parts.
