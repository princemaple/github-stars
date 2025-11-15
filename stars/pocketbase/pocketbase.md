---
project: pocketbase
stars: 52683
description: Open Source realtime backend in 1 file
url: https://github.com/pocketbase/pocketbase
---

PocketBase is an open source Go backend that includes:

-   embedded database (_SQLite_) with **realtime subscriptions**
-   built-in **files and users management**
-   convenient **Admin dashboard UI**
-   and simple **REST-ish API**

**For documentation and examples, please visit https://pocketbase.io/docs.**

Warning

Please keep in mind that PocketBase is still under active development and therefore full backward compatibility is not guaranteed before reaching v1.0.0.

API SDK clients
---------------

The easiest way to interact with the PocketBase Web APIs is to use one of the official SDK clients:

-   **JavaScript - pocketbase/js-sdk** (_Browser, Node.js, React Native_)
-   **Dart - pocketbase/dart-sdk** (_Web, Mobile, Desktop, CLI_)

You could also check the recommendations in https://pocketbase.io/docs/how-to-use/.

Overview
--------

### Use as standalone app

You could download the prebuilt executable for your platform from the Releases page. Once downloaded, extract the archive and run `./pocketbase serve` in the extracted directory.

The prebuilt executables are based on the `examples/base/main.go` file and comes with the JS VM plugin enabled by default which allows to extend PocketBase with JavaScript (_for more details please refer to Extend with JavaScript_).

### Use as a Go framework/toolkit

PocketBase is distributed as a regular Go library package which allows you to build your own custom app specific business logic and still have a single portable executable at the end.

Here is a minimal example:

1.  Install Go 1.23+ (_if you haven't already_)
    
2.  Create a new project directory with the following `main.go` file inside it:
    
    package main
    
    import (
        "log"
    
        "github.com/pocketbase/pocketbase"
        "github.com/pocketbase/pocketbase/core"
    )
    
    func main() {
        app := pocketbase.New()
    
        app.OnServe().BindFunc(func(se \*core.ServeEvent) error {
            // registers new "GET /hello" route
            se.Router.GET("/hello", func(re \*core.RequestEvent) error {
                return re.String(200, "Hello world!")
            })
    
            return se.Next()
        })
    
        if err := app.Start(); err != nil {
            log.Fatal(err)
        }
    }
    
3.  To init the dependencies, run `go mod init myapp && go mod tidy`.
    
4.  To start the application, run `go run main.go serve`.
    
5.  To build a statically linked executable, you can run `CGO_ENABLED=0 go build` and then start the created executable with `./myapp serve`.
    

_For more details please refer to Extend with Go._

### Building and running the repo main.go example

To build the minimal standalone executable, like the prebuilt ones in the releases page, you can simply run `go build` inside the `examples/base` directory:

1.  Install Go 1.23+ (_if you haven't already_)
2.  Clone/download the repo
3.  Navigate to `examples/base`
4.  Run `GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build` (_https://go.dev/doc/install/source#environment_)
5.  Start the created executable by running `./base serve`.

Note that the supported build targets by the pure Go SQLite driver at the moment are:

```
darwin  amd64
darwin  arm64
freebsd amd64
freebsd arm64
linux   386
linux   amd64
linux   arm
linux   arm64
linux   loong64
linux   ppc64le
linux   riscv64
linux   s390x
windows 386
windows amd64
windows arm64
```

### Testing

PocketBase comes with mixed bag of unit and integration tests. To run them, use the standard `go test` command:

go test ./...

Check also the Testing guide to learn how to write your own custom application tests.

Security
--------

If you discover a security vulnerability within PocketBase, please send an e-mail to **support at pocketbase.io**.

All reports will be promptly addressed and you'll be credited in the fix release notes.

Contributing
------------

PocketBase is free and open source project licensed under the MIT License. You are free to do whatever you want with it, even offering it as a paid service.

You could help continuing its development by:

-   Contribute to the source code
-   Suggest new features and report issues

PRs for new OAuth2 providers, bug fixes, code optimizations and documentation improvements are more than welcome.

But please refrain creating PRs for _new features_ without previously discussing the implementation details. PocketBase has a roadmap and I try to work on issues in specific order and such PRs often come in out of nowhere and skew all initial planning with tedious back-and-forth communication.

Don't get upset if I close your PR, even if it is well executed and tested. This doesn't mean that it will never be merged. Later we can always refer to it and/or take pieces of your implementation when the time comes to work on the issue (don't worry you'll be credited in the release notes).
