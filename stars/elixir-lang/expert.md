---
project: expert
stars: 1742
description: Official Elixir Language Server Protocol implementation
url: https://github.com/elixir-lang/expert
---

Expert
======

Expert is the official language server implementation for the Elixir programming language.

Installation
------------

You can download Expert from the releases page for your operating system and architecture. Put the executable somewhere on your `$PATH`, like `~/.local/bin/expert`

For editor specific installation instructions, please refer to the Installation Instructions

### Nightly Builds

If you want to try out the latest features, you can download a nightly build.

Using the GH CLI, you can run the following command to download the latest nightly build:

gh release download nightly --pattern 'expert\_linux\_amd64' --repo elixir-lang/expert

Then point your editor to the downloaded binary.

### Building from source

Expert can be built in two ways: building a regular release for your own system(a "plain" release), or building a "burrito" release that works on multiple systems.

To build Expert for your system, run the following command:

just release

You can then point your editor to the `start_expert` executable in the generated release. You can also run `start_expert --help` to see available options.

Important

If your editor doesn't do it automatically, make sure to pass the `--stdio` flag to Expert.

To build Expert using burrito, you need Zig `0.15.2` installed on your system. Later versions will not work.

Then you can run the following command:

just burrito-local

This will build the Expert binary and place it in the `apps/expert/burrito_out` directory. You can then point your editor to this binary.

You can find more information in the Installation Instructions.

Sponsorship
-----------

Thank you to our corporate sponsors! Expert is currently in alpha and we have organized all future work, including the first release, as milestones. If you'd like to start sponsoring the project, please read more below.

### Corporate

For companies wanting to directly sponsor full time work on Expert, please reach out to Dan Janowski: EEF Chair of Sponsorship WG at sponsor+expert (at) erlef (dot) org.

### Individual

Individuals can donate using GitHub sponsors. Team members are listed in the sidebar.

Other resources
---------------

-   Architecture
-   Development Guide
-   Glossary
-   Installation Instructions

LICENSE
-------

Expert source code is released under Apache License 2.0.

Check LICENSE file for more information.
