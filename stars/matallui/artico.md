---
project: artico
stars: 110
description: Artico - WebRTC made simple
url: https://github.com/matallui/artico
---

Artico
======

Artico is a flexible set of libraries that help you create your own WebRTC-based solutions. It uses a `RTCPeerConnection` abstraction similar to simple-peer, in order to maintain each individual peer-to-peer connection, while providing integrated signaling (via Socket.io), all via simple APIs.

Motivation
----------

WebRTC as a technology has grown significantly in the past few years, making it more and more appealing. However, WebRTC APIs are not always straightforward and easy to use. In addition, WebRTC specifications don't define a signaling protocol or a discovery mechanism.

Multiple projects, like PeerJS and simple-peer, attempt to abstract some of the WebRTC complexities away from the user, facilitating the use of the technology. Even though these are all great projects, they usually fall short on some needed features (i.e., simple-peer doesn't provide signaling, PeerJS provides signaling but misses renegotiation capabilities) or are no longer actively maintained.

Artico aims at being a flexible, yet powerful, set of abstraction tools that should accommodate most WebRTC project needs.

About
-----

Artico provides three core packages:

-   @rtco/peer - `RTCPeerConnection` abstraction, heavily inspired by simple-peer
-   @rtco/client - provides a Socket.io signaling solution on top of @rtco/peer
-   @rtco/server - Socket.io signaling server implementation

You can also find the code to some of our apps:

-   artico-docs - Artico documentation website
-   artico-server - Artico's public Socket.io signaling server
-   artico-examples - Example apps using Artico

The example apps are used to support the development of the Artico ecosystem, whilst demonstrating how to use the library packages.

### @rtco/peer

-   provide WebRTC API abstraction
-   facilitate individual peer to peer connections
-   heavily inspired by simple-peer

### @rtco/client

-   integrated signaling out of the box
-   dynamic number of streams in single connection (via @rtco/peer)
-   facilitate different peer network topologies (e.g., 1-1 Calls or many-many Rooms)
-   multi-platform support (i.e., browser, React Native, Node.js)

### @rtco/server

-   easy to use signaling server
-   integration with existing Node.js servers
-   provide all the needed support for @rtco/client

Usage
-----

Please refer to Artico's documentation for more information.

References
----------

-   PeerJS - This project was inspired by PeerJS and aims at being as simple as PeerJS, while covering more complex scenarios.
-   simple-peer - @rtco/peer is heavily inspired by simple-peer and maintains similar goals.
-   Socket.io - Used as the connection protocol between peers and the signaling server.
-   RTCMultiConnection - Artico aims at providing advanced features found in this great project.
