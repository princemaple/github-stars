---
project: rasa
stars: 20422
description: 💬   Open source machine learning framework to automate text- and voice-based conversations: NLU, dialogue management, connect to Slack, Facebook, and more - Create chatbots and voice assistants
url: https://github.com/RasaHQ/rasa
---

Rasa Open Source
================

* * *

💡 **We're migrating issues to Jira** 💡

Starting January 2023, issues for Rasa Open Source are located in this Jira board. You can browse issues without being logged in; if you want to create issues, you'll need to create a Jira account.

* * *

Rasa is an open source machine learning framework to automate text and voice-based conversations. With Rasa, you can build contextual assistants on:

-   Facebook Messenger
-   Slack
-   Google Hangouts
-   Webex Teams
-   Microsoft Bot Framework
-   Rocket.Chat
-   Mattermost
-   Telegram
-   Twilio
-   Your own custom conversational channels

or voice assistants as:

-   Alexa Skills
-   Google Home Actions

Rasa helps you build contextual assistants capable of having layered conversations with lots of back-and-forth. In order for a human to have a meaningful exchange with a contextual assistant, the assistant needs to be able to use context to build on things that were previously discussed – Rasa enables you to build assistants that can do this in a scalable way.

There's a lot more background information in this blog post.

* * *

-   🤔 Learn more about Rasa
    
-   🤓 Read The Docs
    
-   😁 Install Rasa
    
-   🚀 Dive deeper in the learning center
    
-   🤗 Contribute
    
-   ❓ Get enterprise-grade support
    
-   🏢 Explore the features of our commercial platform
    
-   📚 Learn more about research papers that leverage Rasa
    

* * *

Where to get help
-----------------

There is extensive documentation in the Rasa Docs. Make sure to select the correct version so you are looking at the docs for the version you installed.

Please use Rasa Community Forum for quick answers to questions.

### README Contents:

-   How to contribute
-   Development Internals
-   Releases
-   License

### How to contribute

We are very happy to receive and merge your contributions into this repository!

To contribute via pull request, follow these steps:

1.  Create an issue describing the feature you want to work on (or have a look at the contributor board)
2.  Write your code, tests and documentation, and format them with `black`
3.  Create a pull request describing your changes

For more detailed instructions on how to contribute code, check out these code contributor guidelines.

You can find more information about how to contribute to Rasa (in lots of different ways!) on our website..

Your pull request will be reviewed by a maintainer, who will get back to you about any necessary changes or questions. You will also be asked to sign a Contributor License Agreement.

Development Internals
---------------------

### Installing Poetry

Rasa uses Poetry for packaging and dependency management. If you want to build it from source, you have to install Poetry first. Please follow the official guide to see all possible options.

To update an existing poetry version to the version, currently used in rasa, run:

    poetry self update <version\>

### Managing environments

The official Poetry guide suggests to use pyenv or any other similar tool to easily switch between Python versions. This is how it can be done:

pyenv install 3.10.10
pyenv local 3.10.10  # Activate Python 3.10.10 for the current project

_Note_: If you have trouble installing a specific version of python on your system it might be worth trying other supported versions.

By default, Poetry will try to use the currently activated Python version to create the virtual environment for the current project automatically. You can also create and activate a virtual environment manually — in this case, Poetry should pick it up and use it to install the dependencies. For example:

python -m venv .venv
source .venv/bin/activate

You can make sure that the environment is picked up by executing

poetry env info

### Building from source

To install dependencies and `rasa` itself in editable mode execute

make install

_Note for macOS users_: under macOS Big Sur we've seen some compiler issues for dependencies. Using `export SYSTEM_VERSION_COMPAT=1` before the installation helped.

#### Installing optional dependencies

In order to install rasa's optional dependencies, you need to run:

make install-full

_Note for macOS users_: The command `make install-full` could result in a failure while installing `tokenizers` (issue described in depth here).

In order to resolve it, you must follow these steps to install a Rust compiler:

brew install rustup
rustup-init

After initialising the Rust compiler, you should restart the console and check its installation:

rustc --version

In case the PATH variable had not been automatically setup, run:

export PATH="$HOME/.cargo/bin:$PATH"

### Running and changing the documentation

First of all, install all the required dependencies:

make install install-docs

After the installation has finished, you can run and view the documentation locally using:

make livedocs

It should open a new tab with the local version of the docs in your browser; if not, visit http://localhost:3000 in your browser. You can now change the docs locally and the web page will automatically reload and apply your changes.

### Running the Tests

In order to run the tests, make sure that you have the development requirements installed:

make prepare-tests-ubuntu # Only on Ubuntu and Debian based systems
make prepare-tests-macos  # Only on macOS

Then, run the tests:

make test

They can also be run at multiple jobs to save some time:

JOBS=\[n\] make test

Where `[n]` is the number of jobs desired. If omitted, `[n]` will be automatically chosen by pytest.

### Running the Integration Tests

In order to run the integration tests, make sure that you have the development requirements installed:

make prepare-tests-ubuntu # Only on Ubuntu and Debian based systems
make prepare-tests-macos  # Only on macOS

Then, you'll need to start services with the following command which uses Docker Compose:

make run-integration-containers

Finally, you can run the integration tests like this:

make test-integration

### Resolving merge conflicts

Poetry doesn't include any solution that can help to resolve merge conflicts in the lock file `poetry.lock` by default. However, there is a great tool called poetry-merge-lock. Here is how you can install it:

pip install poetry-merge-lock

Just execute this command to resolve merge conflicts in `poetry.lock` automatically:

poetry-merge-lock

### Build a Docker image locally

In order to build a Docker image on your local machine execute the following command:

make build-docker

The Docker image is available on your local machine as `rasa:localdev`.

### Code Style

To ensure a standardized code style we use the formatter black. To ensure our type annotations are correct we use the type checker pytype. If your code is not formatted properly or doesn't type check, GitHub will fail to build.

#### Formatting

If you want to automatically format your code on every commit, you can use pre-commit. Just install it via `pip install pre-commit` and execute `pre-commit install` in the root folder. This will add a hook to the repository, which reformats files on every commit.

If you want to set it up manually, install black via `poetry install`. To reformat files execute

```
make formatter
```

#### Type Checking

If you want to check types on the codebase, install `mypy` using `poetry install`. To check the types execute

```
make types
```

### Deploying documentation updates

We use `Docusaurus v2` to build docs for tagged versions and for the `main` branch. To run Docusaurus, install `Node.js 12.x`. The static site that gets built is pushed to the `documentation` branch of this repo.

We host the site on netlify. On `main` branch builds (see `.github/workflows/documentation.yml`), we push the built docs to the `documentation` branch. Netlify automatically re-deploys the docs pages whenever there is a change to that branch.

Releases
--------

Rasa has implemented robust policies governing version naming, as well as release pace for major, minor, and patch releases.

The values for a given version number (MAJOR.MINOR.PATCH) are incremented as follows:

-   MAJOR version for incompatible API changes or other breaking changes.
-   MINOR version for functionality added in a backward compatible manner.
-   PATCH version for backward compatible bug fixes.

The following table describes the version types and their expected _release cadence_:

Version Type

Description

Target Cadence

Major

For significant changes, or when any backward-incompatible changes are introduced to the API or data model.

Every 1 - 2 yrs

Minor

For when new backward-compatible functionality is introduced, a minor feature is introduced, or when a set of smaller features is rolled out.

+/- Quarterly

Patch

For backward-compatible bug fixes that fix incorrect behavior.

As needed

While this table represents our target release frequency, we reserve the right to modify it based on changing market conditions and technical requirements.

### Maintenance Policy

Our End of Life policy defines how long a given release is considered supported, as well as how long a release is considered to be still in active development or maintenance.

The maintentance duration and end of life for every release are shown on our website as part of the Product Release and Maintenance Policy.

### Cutting a Major / Minor release

#### A week before release day

1.  **Make sure the milestone already exists and is scheduled for the correct date.**
2.  **Take a look at the issues & PRs that are in the milestone**: does it look about right for the release highlights we are planning to ship? Does it look like anything is missing? Don't worry about being aware of every PR that should be in, but it's useful to take a moment to evaluate what's assigned to the milestone.
3.  **Post a message on the engineering Slack channel**, letting the team know you'll be the one cutting the upcoming release, as well as:
    1.  Providing the link to the appropriate milestone
    2.  Reminding everyone to go over their issues and PRs and please assign them to the milestone
    3.  Reminding everyone of the scheduled date for the release

#### A day before release day

1.  **Go over the milestone and evaluate the status of any PR merging that's happening. Follow up with people on their bugs and fixes.** If the release introduces new bugs or regressions that can't be fixed in time, we should discuss on Slack about this and take a decision on how to move forward. If the issue is not ready to be merged in time, we remove the issue / PR from the milestone and notify the PR owner and the product manager on Slack about it. The PR / issue owners are responsible for communicating any issues which might be release relevant. Postponing the release should be considered as an edge case scenario.

#### Release day! 🚀

1.  **At the start of the day, post a small message on slack announcing release day!** Communicate you'll be handling the release, and the time you're aiming to start releasing (again, no later than 4pm, as issues may arise and cause delays). This message should be posted early in the morning and before moving forward with any of the steps of the release, in order to give enough time to people to check their PRs and issues. That way they can plan any remaining work. A template of the slack message can be found here. The release time should be communicated transparently so that others can plan potentially necessary steps accordingly. If there are bigger changes this should be communicated.
2.  Make sure the milestone is empty (everything has been either merged or moved to the next milestone)
3.  Once everything in the milestone is taken care of, post a small message on Slack communicating you are about to start the release process (in case anything is missing).
4.  **You may now do the release by following the instructions outlined in the Rasa Open Source README !**

#### After a Major release

After a Major release has been completed, please follow these instructions to complete the documentation update.

### Steps to release a new version

Releasing a new version is quite simple, as the packages are build and distributed by GitHub Actions.

_Release steps_:

1.  Make sure all dependencies are up to date (**especially Rasa SDK**)
    -   For Rasa SDK, except in the case of a patch release, that means first creating a new Rasa SDK release (make sure the version numbers between the new Rasa and Rasa SDK releases match)
    -   Once the tag with the new Rasa SDK release is pushed and the package appears on pypi, the dependency in the rasa repository can be resolved (see below).
2.  If this is a minor / major release: Make sure all fixes from currently supported minor versions have been merged from their respective release branches (e.g. 3.3.x) back into main.
3.  In case of a minor release, create a new branch that corresponds to the new release, e.g.
    
     git checkout -b 1.2.x
     git push origin 1.2.x
    
4.  Switch to the branch you want to cut the release from (`main` in case of a major, the `<major>.<minor>.x` branch for minors and patches)
    -   Update the `rasa-sdk` entry in `pyproject.toml` with the new release version and run `poetry update`. This creates a new `poetry.lock` file with all dependencies resolved.
    -   Commit the changes with `git commit -am "bump rasa-sdk dependency"` but do not push them. They will be automatically picked up by the following step.
5.  If this is a major release, update the list of actively maintained versions in the README and in the docs.
6.  Run `make release`
7.  Create a PR against the release branch (e.g. `1.2.x`)
8.  Once your PR is merged, tag a new release (this SHOULD always happen on the release branch), e.g. using
    
    git checkout 1.2.x
    git pull origin 1.2.x
    git tag 1.2.0 -m "next release"
    git push origin 1.2.0 --tags
    
    GitHub will build this tag and publish the build artifacts.
9.  After all the steps are completed and if everything goes well then we should see a message automatically posted in the company's Slack (`product` channel) like this one
10.  If no message appears in the channel then you can do the following checks:
    -   Check the workflows in Github Actions and make sure that the merged PR of the current release is completed successfully. To easily find your PR you can use the filters `event: push` and `branch: <version number>` (example on release 2.4 you can see here)
    -   If the workflow is not completed, then try to re run the workflow in case that solves the problem
    -   If the problem persists, check also the log files and try to find the root cause of the issue
    -   If you still cannot resolve the error, contact the infrastructure team by providing any helpful information from your investigation
11.  After the message is posted correctly in the `product` channel, check also in the `product-engineering-alerts` channel if there are any alerts related to the Rasa Open Source release like this one

### Cutting a Patch release

Patch releases are simpler to cut, since they are meant to contain only bugfixes.

**The only things you need to do to cut a patch release are:**

1.  Notify the engineering team on Slack that you are planning to cut a patch, in case someone has an important fix to add.
2.  Make sure the bugfix(es) are in the release branch you will use (p.e if you are cutting a `2.0.4` patch, you will need your fixes to be on the `2.0.x` release branch). All patch releases must come from a `.x` branch!
3.  Once you're ready to release the Rasa Open Source patch, checkout the branch, run `make release` and follow the steps + get the PR merged.
4.  Once the PR is in, pull the `.x` branch again and push the tag!

### Additional Release Tasks

**Note: This is only required if the released version is the highest version available. For instance, perform the following steps when version > version on main.**

In order to check compatibility between the new released Rasa version to the latest version of Rasa X/Enterprise, we perform the following steps:

1.  Following a new Rasa release, an automated pull request is created in Rasa-X-Demo.
2.  Once the above PR is merged, follow instructions here, to release a version.
3.  Update the new version in the Rasa X/Enterprise env file. The Rasa-X-Demo project uses the new updated Rasa version to train and test a model which in turn is used by our CI to run tests in the Rasa X/Enterprise repository, thus validating compatibility between Rasa and Rasa X/Enterprise.

### Actively maintained versions

Please refer to the Rasa Product Release and Maintenance Policy page.

License
-------

Licensed under the Apache License, Version 2.0. Copyright 2022 Rasa Technologies GmbH. Copy of the license.

A list of the Licenses of the dependencies of the project can be found at the bottom of the Libraries Summary.
