---
project: bauble
stars: 544
description: a playground for making 3D art with lisp and math
url: https://github.com/ianthehenry/bauble
---

Bauble
======

Bauble is a toy for composing signed distance functions in a high-level language (Janet), compiling them to GLSL, and rendering them via WebGL.

Try it out at https://bauble.studio/, or watch this video introduction where I model an infinite number of hot air balloons:

Note that Bauble has changed (for the better!) quite a bit since that video, so it doesn't translate one to one. But it should be able to give you a good idea of the gist.

For more examples, I sometimes tweet videos of Bauble's development, which you can find here:

https://twitter.com/ianthehenry

Dependencies
============

-   For the CLI
    -   `janet`
-   For the web UI
    -   `emscripten`
    -   `redo`
    -   `yarn`
-   For tests
    -   `pngcrush` (tests only)

Bauble requires at least Janet 1.36.0 (the first release with integer literal syntax). It may work with newer versions of Janet, assuming that the image format is compatible, but it's better to update the version of Janet that Bauble includes to match your local version if you want to upgrade.

To build the CLI, install Janet dependencies like this:

```
$ (cd src && jpm -l deps)
```

To build the web UI, install JavaScript dependencies as well:

```
$ yarn
$ (cd studio && yarn)
```

Bauble depends on `codemirror-lang-janet`. If you want to make changes to the grammar, clone that repo and run `yalc publish` from the root of it. Then run `yalc link codemirror-lang-janet` in this repository, and you'll be able to see your changes locally.

Development
===========

To build the CLI:

```
$ (cd src && jpm -l build)
```

To run the CLI:

```
$ src/build/bauble help
```

To build the web UI:

```
$ redo
```

To create a minified, optimized build, use:

```
$ BUILD_MODE=prod redo
```

Lint the JS with:

```
(cd studio && yarn eslint .)
```

And you can serve a local Bauble like this:

```
$ node_modules/.bin/alive-server public
```

Testing
=======

There are two types of tests. Regular Judge unit tests:

```
$ (cd src && judge)
```

And snapshot tests, which require installing separate dependencies:

```
# you only have to do this once
$ (cd tests && jpm -l deps)
```

After installing dependencies, run tests like this:

```
$ (cd tests && jpm -l janet suite.janet)
```

Snapshot tests will write a file called `tests/summary.html`. It's not a very good file.

Before you commit snapshot changes, run:

```
$ (cd tests && jpm -l janet gc.janet)
```

Which will delete old snapshots and compress new ones. This depends on `pngcrush`.

CLI
===

To run the Bauble CLI:

```
$ cd src
$ jpm -l deps
$ jpm -l build
$ build/bauble
```

Or, after installing dependencies, you can just invoke it with the interpreter:

```
$ cd src
$ jpm -l janet cli/init.janet
```

Currently the CLI is the only way to export high-resolution images, render images with non-square aspect ratios, view raw GLSL shader source, and export 3D meshes.
