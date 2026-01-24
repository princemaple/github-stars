---
project: ex_webrtc
stars: 457
description: An Elixir implementation of the W3C WebRTC API
url: https://github.com/elixir-webrtc/ex_webrtc
---

  

* * *

**Elixir WebRTC** is an implementation of the W3C WebRTC API in the Elixir programming language.

Installation
------------

Add `ex_webrtc` to the list of dependencies in `mix.exs`

def deps do
  \[
    {:ex\_webrtc, "~> 0.15.0"}
  \]
end

Elixir WebRTC comes with optional support for DataChannels, but it must be explicitely turned on by adding optional `ex_sctp` dependency

def deps do
  \[
    {:ex\_webrtc, "~> 0.15.0"},
    {:ex\_sctp, "~> 0.1.0"}
  \]
end

Please note that `ex_sctp` requires you to have Rust installed in order to compile.

Getting started
---------------

To get started with Elixir WebRTC, check out:

-   the Introduction to Elixir Webrtc tutorial
-   the examples directory that contains a bunch of very simple usage examples of the library
-   the `apps` repo with example applications built on top of `ex_webrtc`
-   the documentation, especially the `PeerConnection` module page
-   the roadmap to see what we are working on and how you can contribute

If you have any questions, ideas or topics to discuss about Elixir WebRTC, head to the discussions page.

Elixir WebRTC vs Membrane
-------------------------

Elixir WebRTC is the W3C WebRTC standard implementation written in almost pure Elixir. It does not use Membrane under the hood, and it aims to be as close to the W3C (and hence JavaScript) API as possible.

Membrane, on the other hand, is a multimedia framework. It supports a lot of different protocols, codecs and containers. Membrane uses Elixir WebRTC in its membrane\_webrtc\_plugin making it possible to use WebRTC with other Membrane elements.

Credits
-------

Elixir WebRTC is created by Software Mansion.

Since 2012 Software Mansion is a software agency with experience in building web and mobile apps as well as complex multimedia solutions. We are Core React Native Contributors and experts in live streaming and broadcasting technologies. We can help you build your next dream product – Hire us.
