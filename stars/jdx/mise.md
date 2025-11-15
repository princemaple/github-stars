---
project: mise
stars: 21401
description: dev tools, env vars, task runner
url: https://github.com/jdx/mise
---

  
mise-en-place
================

**The front-end to your dev env**

Getting Started • Documentation • Dev Tools • Environments • Tasks

* * *

What is it?
-----------

-   Like asdf (or nvm or pyenv but for any language) it manages dev tools like node, python, cmake, terraform, and hundreds more.
-   Like direnv it manages environment variables for different project directories.
-   Like make it manages tasks used to build and test projects.

Demo
----

The following demo shows how to install and use `mise` to manage multiple versions of `node` on the same system. Note that calling `which node` gives us a real path to node, not a shim.

It also shows that you can use `mise` to install and many other tools such as `jq`, `terraform`, or `go`.

See demo transcript.

Quickstart
----------

### Install mise

See Getting started for more options.

$ curl https://mise.run | sh
$ ~/.local/bin/mise --version
2025.11.5 macos-arm64 (a1b2d3e 2025-11-15)

Hook mise into your shell (pick the right one for your shell):

\# note this assumes mise is located at ~/.local/bin/mise
# which is what https://mise.run does by default
echo 'eval "$(~/.local/bin/mise activate bash)"' >> ~/.bashrc
echo 'eval "$(~/.local/bin/mise activate zsh)"' >> ~/.zshrc
echo '~/.local/bin/mise activate fish | source' >> ~/.config/fish/config.fish
echo '~/.local/bin/mise activate pwsh | Out-String | Invoke-Expression' >> ~/.config/powershell/Microsoft.PowerShell\_profile.ps1

### Execute commands with specific tools

$ mise exec node@22 -- node -v
mise node@22.x.x ✓ installed
v22.x.x

### Install tools

$ mise use --global node@22 go@1
$ node -v
v22.x.x
$ go version
go version go1.x.x macos/arm64

See dev tools for more examples.

### Manage environment variables

# mise.toml
\[env\]
SOME\_VAR = "foo"

$ mise set SOME\_VAR=bar
$ echo $SOME\_VAR
bar

Note that `mise` can also load `.env` files.

### Run tasks

# mise.toml
\[tasks.build\]
description = "build the project"
run = "echo building..."

$ mise run build
building...

See tasks for more information.

### Example mise project

Here is a combined example to give you an idea of how you can use mise to manage your a project's tools, environment, and tasks.

# mise.toml
\[tools\]
terraform = "1"
aws-cli = "2"

\[env\]
TF\_WORKSPACE = "development"
AWS\_REGION = "us-west-2"
AWS\_PROFILE = "dev"

\[tasks.plan\]
description = "Run terraform plan with configured workspace"
run = """
terraform init
terraform workspace select $TF\_WORKSPACE
terraform plan
"""

\[tasks.validate\]
description = "Validate AWS credentials and terraform config"
run = """
aws sts get-caller-identity
terraform validate
"""

\[tasks.deploy\]
description = "Deploy infrastructure after validation"
depends = \["validate", "plan"\]
run = "terraform apply -auto-approve"

Run it with:

mise install # install tools specified in mise.toml
mise run deploy

Find more examples in the mise cookbook.

Full Documentation
------------------

See mise.jdx.dev

GitHub Issues & Discussions
---------------------------

Due to the volume of issue submissions mise received, using GitHub Issues became unsustainable for the project. Instead, mise uses GitHub Discussions which provide a more community-centric platform for communication and require less management on the part of the maintainers.

Please note the following discussion categories, which match how issues are often used:

-   Announcements
-   Ideas: for feature requests, etc.
-   Troubleshooting & Bug Reports

Special Thanks
--------------

We're grateful for Cloudflare's support through Project Alexandria.

Contributors
------------
