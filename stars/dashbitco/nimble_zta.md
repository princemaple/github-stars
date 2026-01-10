---
project: nimble_zta
stars: 48
description: Add Zero Trust Auth (ZTA) to web apps running in your private cloud
url: https://github.com/dashbitco/nimble_zta
---

NimbleZTA
=========

Add Zero Trust Auth (ZTA) to your Plug/Phoenix web apps. In a nutshell, if you are running applications inside your private cloud, you can use your cloud provider to identify and control access to your app, so you can focus on your application logic.

`nimble_zta` is a collection of strategies for different providers. CloudFlare, Google Cloud Platform, and Tailscale are currently supported, with additional HTTP Basic Auth and Pass Through strategies available for development and testing. Read the docs for more information.

This library was extracted from Livebook.

Installation
------------

You can install `nimble_zta` by adding it to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:nimble\_zta, "~> 0.1"}
  \]
end

Nimble\*
--------

All nimble libraries by Dashbit:

-   NimbleCSV - simple and fast CSV parsing
-   NimbleOptions - tiny library for validating and documenting high-level options
-   NimbleOwnership - resource ownership tracking
-   NimbleParsec - simple and fast parser combinators
-   NimblePool - tiny resource-pool implementation
-   NimblePublisher - a minimal filesystem-based publishing engine with Markdown support and code highlighting
-   NimbleTOTP - tiny library for generating time-based one time passwords (TOTP)
-   NimbleZTA - add Zero Trust Auth (ZTA) to web apps running in your private cloud

License
-------

Copyright 2025 Dashbit

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
  http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
