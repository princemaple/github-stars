---
project: sshkit.ex
stars: 164
description: An Elixir toolkit for performing tasks on one or more servers, built on top of Erlang’s SSH application.
url: https://github.com/bitcrowd/sshkit.ex
---

SSHKit
======

SSHKit is an Elixir toolkit for performing tasks on one or more servers, built on top of Erlang’s SSH application.

Documentation for SSHKit is available online.

Usage
-----

SSHKit is designed to enable server task automation in a structured and repeatable way, e.g. in the context of deployment tools:

hosts \= \["1.eg.io", {"2.eg.io", port: 2222}\]

context \=
  SSHKit.context(hosts)
  |> SSHKit.path("/var/www/phx")
  |> SSHKit.user("deploy")
  |> SSHKit.group("deploy")
  |> SSHKit.umask("022")
  |> SSHKit.env(%{"NODE\_ENV" \=> "production"})

\[:ok, :ok\] \= SSHKit.upload(context, ".", recursive: true)
\[{:ok, \_, 0}, {:ok, \_, 0}\] \= SSHKit.run(context, "yarn install")

The `SSHKit` module documentation has more guidance and examples for the DSL.

If you need more control, take a look at the `SSHKit.SSH` and `SSHKit.SCP` modules.

Installation
------------

Just add `sshkit` to your list of dependencies in `mix.exs`:

def deps do
  \[{:sshkit, "~> 0.1"}\]
end

SSHKit should be automatically started unless the `:applications` key is set inside `def application` in your `mix.exs`. In such cases, you need to remove the `:applications` key in favor of `:extra_applications`.

Modules
-------

SSHKit consists of three core modules:

```
+--------------------+
| SSHKit             |
+--------------------+
|       | SSHKit.SCP |
|       +------------+
| SSHKit.SSH         |
+--------------------+
```

1.  **`SSHKit.SSH`** provides convenience functions for working with SSH connections and for executing commands on remote hosts.
    
2.  **`SSHKit.SCP`** provides convenience functions for transferring files or entire directory trees to or from a remote host via SCP. It is built on top of `SSHKit.SSH`.
    
3.  **`SSHKit`** provides the main API for automating tasks on remote hosts in a structured way. It uses both `SSH` and `SCP` to implement its functionality.
    

Additional modules, e.g. for custom client key handling, are available as separate packages:

-   **`ssh_client_key_api`**: An Elixir implementation for the Erlang `ssh_client_key_api` behavior, to make it easier to specify SSH keys and `known_hosts` files independently of any particular user's home directory.

Testing
-------

As usual, to run all tests, use:

mix test

Apart from unit tests, we also have functional tests. These check SSHKit functionality against real SSH server implementations running inside Docker containers. Therefore, you need to have Docker installed.

All functional tests are tagged as such. Hence, if you wish to skip them:

mix test --exclude functional

Hint: We've found functional tests to run significantly faster with Docker Machine compared to Docker for Mac on OS X.

Releasing
---------

-   Make sure tests pass: `mix test`.
-   Increase version number in `mix.exs`, keeping semantic versioning in mind.
-   Update CHANGLOG.md:
    -   Create a new section for the current version.
    -   Reset the `master` section to the empty template.
-   Commit your changes: `git commit -m "Release 0.1.0"`.
-   Tag the commit with the version number: `git tag -a v0.1.0`.
    -   Annotate the tag with the respective section from CHANGLOG.md _(in a git-compatible format)_.
-   Push your commit: `git push`.
-   Push the tag: `git push origin v0.1.0`
-   Publish the new release to hex.pm: `mix hex.publish`.
    -   You can find the hex.pm credentials in the bitcrowd password store.

Contributing
------------

We welcome everyone to contribute to SSHKit and help us tackle existing issues!

Use the issue tracker for bug reports or feature requests. Open a pull request when you are ready to contribute.

If you are planning to contribute documentation, please check the best practices for writing documentation.

Thanks
------

SSHKit is inspired by SSHKit for Ruby which is part of the fantastic Capistrano project.

It deliberately departs from its role model with regard to its API given the very different nature of the two programming languages.

If you are looking for an Elixir deployment tool similar to Capistrano, take a look at Bootleg which is based on top of SSHKit.

License
-------

SSHKit source code is released under the MIT License.

Check the LICENSE file for more information.
