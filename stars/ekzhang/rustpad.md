---
project: rustpad
stars: 3945
description: Efficient and minimal collaborative code editor, self-hosted, no database required
url: https://github.com/ekzhang/rustpad
---

Rustpad
=======

**Rustpad** is an _efficient_ and _minimal_ open-source collaborative text editor based on the operational transformation algorithm. It lets users collaborate in real time while writing code in their browser. Rustpad is completely self-hosted and fits in a tiny Docker image, no database required.

  
**rustpad.io**

The server is written in Rust using the warp web server framework and the operational-transform library. We use wasm-bindgen to compile text operation logic to WebAssembly code, which runs in the browser. The frontend is written in TypeScript using React and interfaces with Monaco, the text editor that powers VS Code.

Architecturally, client-side code communicates via WebSocket with a central server that stores in-memory data structures. This makes the editor very fast, allows us to avoid provisioning a database, and makes testing much easier. The tradeoff is that documents are transient and lost between server restarts, or after 24 hours of inactivity.

Development setup
-----------------

To run this application, you need to install Rust, `wasm-pack`, and Node.js. Then, build the WebAssembly portion of the app:

```
wasm-pack build rustpad-wasm
```

When that is complete, you can install dependencies for the frontend React application:

```
npm install
```

Next, compile and run the backend web server:

```
cargo run
```

While the backend is running, open another shell and run the following command to start the frontend portion.

```
npm run dev
```

This command will open a browser window to `http://localhost:5173`, with hot reloading on changes.

Testing
-------

To run integration tests for the server, use the standard `cargo test` command. For the WebAssembly component, you can run tests in a headless browser with

```
wasm-pack test --chrome --headless rustpad-wasm
```

Configuration
-------------

Although the default behavior of Rustpad is to store documents solely in memory and collect garbage after 24 hours of inactivity, this can be configured by setting the appropriate variables. The application server looks for the following environment variables on startup:

-   `EXPIRY_DAYS`: An integer corresponding to the number of days that inactive documents are kept in memory before being garbage collected by the server (default 1 day).
-   `SQLITE_URI`: A SQLite connection string used for persistence. If provided, Rustpad will snapshot document contents to a local file, which enables them to be retained between server restarts and after their in-memory data structures expire. (When deploying a Docker container, this should point to the path of a mounted volume.)
-   `PORT`: Which local port to listen for HTTP connections on (defaults to 3030).
-   `RUST_LOG`: Directives that control application logging, see the env\_logger docs for more information.

Deployment
----------

Rustpad is distributed as a single 6 MB Docker image, which is built automatically from the `Dockerfile` in this repository. You can pull the latest version of this image from Docker Hub. It has multi-platform support for `linux/amd64` and `linux/arm64`.

```
docker pull ekzhang/rustpad
```

(You can also manually build this image with `docker build -t rustpad .` in the project root directory.) To run locally, execute the following command, then open `http://localhost:3030` in your browser.

```
docker run --rm -dp 3030:3030 ekzhang/rustpad
```

We deploy a public instance of this image using Fly.io.

In the media
------------

-   **July 11, 2021:** Featured in Console 61 - The open-source newsletter.
-   **June 5, 2021:** Front-page Hacker News post. Reddit discussions in r/rust and r/programming.

  
All code is licensed under the MIT license.
