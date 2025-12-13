---
project: Rocket
stars: 25540
description: A web framework for Rust.
url: https://github.com/rwf2/Rocket
---

Rocket
======

Rocket is an async web framework for Rust with a focus on usability, security, extensibility, and speed.

#\[macro\_use\] extern crate rocket;

#\[get("/<name>/<age>")\]
fn hello(name: &str, age: u8) -> String {
    format!("Hello, {} year old named {}!", age, name)
}

#\[launch\]
fn rocket() -> \_ {
    rocket::build().mount("/hello", routes!\[hello\])
}

Visiting `localhost:8000/hello/John/58`, for example, will trigger the `hello` route resulting in the string `Hello, 58 year old named John!` being sent to the browser. If an `<age>` string was passed in that can't be parsed as a `u8`, the route won't get called, resulting in a 404 error.

Documentation
-------------

Rocket is extensively documented:

-   Overview: A brief look at what makes Rocket special.
-   Quickstart: How to get started as quickly as possible.
-   Getting Started: How to start your first Rocket project.
-   Guide: A detailed guide and reference to Rocket.
-   API Documentation: The "rustdocs".

Documentation for the `master` branch is available at https://rocket.rs/master and https://api.rocket.rs/master.

Documentation for major release version `${x}` is available at `https://[api.]rocket.rs/v${x}`. For example, the v0.4 docs are available at https://rocket.rs/v0.4 and https://api.rocket.rs/v0.4.

Finally, API docs for active git branches are available at `https://api.rocket.rs/${branch}`. For example, API docs for the `master` branch are available at https://api.rocket.rs/master. Branch rustdocs are built and deployed on every commit.

Examples
--------

The examples directory contains complete crates that showcase Rocket's features and usage. Each example can be compiled and run with Cargo. For instance, the following sequence of commands builds and runs the `hello` example:

cd examples/hello
cargo run

Getting Help
------------

If you find yourself needing help outside of the documentation, you may:

-   Ask questions via GitHub discussions questions.
-   Chat with us at `#rocket:mozilla.org` on Matrix (join via Element).

Contributing
------------

Contributions are absolutely, positively welcomed and encouraged! If you're interested in contributing code, please first read CONTRIBUTING for complete guidelines. Additionally, you could:

1.  Submit a feature request or bug report as an issue.
2.  Ask for improved documentation as an issue.
3.  Comment on issues that require feedback.
4.  Answers questions in GitHub discussions questions.
5.  Share a project in GitHub discussions show & tell.

License
-------

Rocket is licensed under either of the following, at your option:

-   Apache License, Version 2.0, (LICENSE-APACHE or https://www.apache.org/licenses/LICENSE-2.0)
-   MIT License (LICENSE-MIT or https://opensource.org/licenses/MIT)

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in Rocket by you shall be dual licensed under the MIT License and Apache License, Version 2.0, without any additional terms or conditions.

The Rocket website docs are licensed under separate terms. Any contribution intentionally submitted for inclusion in the Rocket website docs by you shall be licensed under those terms.
