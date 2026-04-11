---
project: ferret
stars: 5964
description: Declarative web scraping
url: https://github.com/MontFerret/ferret
---

Ferret
======

Try it! Docs CLI Test runner Web worker

* * *

> **📢 Notice:** This branch contains the upcoming **Ferret v2**. For the stable v1 release, please visit Ferret v1.

* * *

What is it?
-----------

Ferret is a declarative system for working with web data - extracting it, querying it, and turning it into structured results for testing, analytics, machine learning, and other workflows. It allows users to focus on the data they need while abstracting away the complexity of browser automation, page interaction, and underlying execution details.

### Features

-   Declarative query language
-   Works with static and dynamic web pages
-   Embeddable in Go applications
-   Extensible runtime and function system
-   Portable and fast

Getting started
---------------

go get github.com/MontFerret/ferret/v2@latest

There are currently two ways to start with Ferret v2:

-   Native v2 API - recommended for new projects
-   `compat` module - recommended as a first migration step for existing v1 integrations

### New projects

Use the native v2 API built around the following flow:

```
Engine -> compile query -> create session -> run
```

package main

import (
	"context"
	"fmt"
	"log"

	"github.com/MontFerret/ferret/v2/pkg/engine"
)

func main() {
	ctx := context.Background()

	eng, err := engine.New()
	if err != nil {
		log.Fatal(err)
	}
	defer eng.Close()

	plan, err := eng.Compile(\`RETURN 1 + 1\`)
	if err != nil {
		log.Fatal(err)
	}

	session, err := plan.NewSession()
	if err != nil {
		log.Fatal(err)
	}
	defer session.Close()

	result, err := session.Run(ctx)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println(result.Content)
}

### Migration from v1

Ferret v2 introduces a new architecture and public API, so embedding it directly is different from v1.

To make migration easier, v2 includes a compat module that provides a v1-style API. Its goal is to make upgrades incremental instead of forcing a full rewrite up front.

For many projects, the easiest migration path will be:

-   switch imports from v1 to the compat package
-   get the project compiling again
-   migrate incrementally to the native v2 API over time

A small helper script for rewriting import paths is planned to simplify this process further.

The compatibility layer is intended as a migration aid, not the long-term preferred API. New projects should use the native v2 packages directly.

### Alpha status

Ferret v2 is currently in active development.

Alpha releases are intended for early adopters, experimentation, and feedback. Some APIs and language features may still change before the stable v2 release.
