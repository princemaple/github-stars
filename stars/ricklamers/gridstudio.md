---
project: gridstudio
stars: 8862
description: Grid studio is a web-based application for data science with full integration of open source data science frameworks and languages.
url: https://github.com/ricklamers/gridstudio
---

Grid studio is a web-based spreadsheet application with full integration of the Python programming language.

main-video.mp4

It intends to provide an integrated workflow for loading, cleaning, manipulating, and visualizing data. This is achieved through a spreadsheet backend written in Go with integration of the Python runtime to manipulate its contents.

### Architecture overview

The application is structured in two parts:

1.  The (centralized) workspace manager
    1.  CRUD interface for creating, copying, editing and deleting workspaces.
    2.  Proxy to send traffic to the right workspace environment (part 2)
2.  Workspace Go execution environment
    1.  Go cell parsing and evaluating spreadsheet backend
    2.  Node.js terminal session
    3.  Python interpreter integration

For more details about each part check out the code in the repository. If anything is unclear (or unreadable - not all code is equally pretty!) make an issue and details will be provided.

### Features

#### Spreadsheet functions that you know

feature-spreadsheet.mp4

#### Powerful scripting, fully integrated

feature-python.mp4

#### Run any command on Ubuntu Linux

feature-terminal.mp4

### Installation

To run Grid studio locally refer to the Installation page of the Wiki.

It comes down to pulling the latest Grid studio Docker image that has all dependencies configured (mainly: Go language, Python 3 with packages, Node.js) and starting the Docker container.

For more information check out our Wiki.
