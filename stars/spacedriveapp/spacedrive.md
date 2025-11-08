---
project: spacedrive
stars: 35555
description: Spacedrive is an open source cross-platform file explorer, powered by a virtual distributed filesystem written in Rust.
url: https://github.com/spacedriveapp/spacedrive
---

**Spacedrive**
==============

A file explorer from the future.  
**spacedrive.com »**  
  
**Download for** macOS (Apple Silicon | Intel) · Windows · Linux · iOS · Android  
_~ Links for iOS & Android will be added once a release is available. ~_

Spacedrive is an open source cross-platform file manager, powered by a virtual distributed filesystem (VDFS) written in Rust.  
  

Important

We regret to inform our valued Spacedrive community that we must temporarily pause our development roadmap beyond our latest update. Due to current funding constraints and related challenges, we cannot deliver new features or updates for the foreseeable future.

While this was a tough decision, our team remains committed to Spacedrive's vision and will explore options to resume development when circumstances allow. We deeply appreciate your understanding and continued support during this challenging period.

The Spacedrive Team

Organize files across many devices in one place. From cloud services to offline hard drives, Spacedrive combines the storage capacity and processing power of your devices into one personal distributed cloud, that is both secure and intuitive to use.

For independent creatives, hoarders and those that want to own their digital footprint, Spacedrive provides a free file management experience like no other.

  
  
  

What is a VDFS?
===============

A VDFS (virtual distributed filesystem) is a filesystem designed to work across a variety of storage layers. With a uniform API to manipulate and access content across many devices, VDFS is not restricted to a single machine. It achieves this by maintaining a virtual index of all storage locations, synchronizing the database between clients in realtime. This implementation also uses CAS (Content-addressable storage) to uniquely identify files, while keeping record of logical file paths relative to the storage locations.

The first implementation of a VDFS can be found in this UC Berkeley paper by Haoyuan Li. This paper describes its use for cloud computing, however the underlying concepts can be translated to open consumer software.

Motivation
==========

Many of us have multiple cloud accounts, drives that aren’t backed up and data at risk of loss. We depend on cloud services like Google Photos and iCloud, but are locked in with limited capacity and almost zero interoperability between services and operating systems. Photo albums shouldn’t be stuck in a device ecosystem, or harvested for advertising data. They should be OS agnostic, permanent and personally owned. Data we create is our legacy, that will long outlive us—open source technology is the only way to ensure we retain absolute control over the data that defines our lives, at unlimited scale.

Roadmap
=======

View a list of our planned features here: spacedrive.com/roadmap

Developer Guide
===============

Please refer to the contributing guide for how to install Spacedrive from sources.

Security Policy
===============

Please refer to the security policy for details and information on how to responsibly report a security vulnerability or issue.

Architecture
============

This project is using what I'm calling the **"PRRTT"** stack (Prisma, Rust, React, TypeScript, Tauri).

-   Prisma on the front-end? 🤯 Made possible thanks to prisma-client-rust, developed by Brendonovich. Gives us access to the powerful migration CLI in development, along with the Prisma syntax for our schema. The application bundles with the Prisma query engine and codegen for a beautiful Rust API. Our lightweight migration runner is custom built for a desktop app context.
-   Tauri allows us to create a pure Rust native OS webview, without the overhead of your average Electron app. This brings the bundle size and average memory usage down dramatically. It also contributes to a more native feel, especially on macOS due to Safari's close integration with the OS.
-   We also use rspc, created by Oscar Beaumont, which allows us to define functions in Rust and call them on the TypeScript frontend in a completely typesafe manner.
-   The core (`sdcore`) is written in pure Rust.

Monorepo structure:
-------------------

### Apps:

-   `desktop`: A Tauri app.
-   `mobile`: A React Native app.
-   `web`: A React webapp.
-   `landing`: A React app using Next.js.
-   `server`: A Rust server for the webapp.
-   `cli`: A Rust command line interface. (planned)
-   `storybook`: A React storybook for the UI components.

### Core:

-   `core`: The Rust core, referred to internally as `sdcore`. Contains filesystem, database and networking logic. Can be deployed in a variety of host applications.
-   `crates`: Shared Rust libraries used by the core and other Rust applications.

### Interface:

-   `interface`: The complete user interface in React (used by apps `desktop`, `web`)

### Packages:

-   `assets`: Shared assets (images, fonts, etc).
    
-   `client`: A TypeScript client library to handle dataflow via RPC between UI and the Rust core.
    
-   `config`: `eslint` configurations (includes `eslint-config-next`, `eslint-config-prettier` and all `tsconfig.json` configs used throughout the monorepo).
    
-   `ui`: A React Shared component library.
    
-   `macos`: A Swift Native binary for MacOS system extensions (planned).
    
-   `ios`: A Swift Native binary (planned).
    
-   `windows`: A C# Native binary (planned).
    
-   `android`: A Kotlin Native binary (planned).
