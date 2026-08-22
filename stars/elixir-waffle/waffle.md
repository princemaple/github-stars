---
project: waffle
stars: 821
description: Flexible file upload and attachment library for Elixir
url: https://github.com/elixir-waffle/waffle
---

Waffle
======

Waffle is a flexible file upload library for Elixir with straightforward integrations for Amazon S3 and ImageMagick.

Documentation · Hex

Presentation at ElixirConf · Thinking Elixir Podcast 80

* * *

Already using Waffle in your org? I'd love to learn more. Let's have a chat or just send me an email.

* * *

Why use Waffle?
---------------

You want to apply file transformations, manage access rules, save files, or process files asynchronously.

Quick start
-----------

Add the `:waffle` dependency to `mix.exs`.

**mix.exs**

{:waffle, "== 2.0.0-rc.1"},
{:waffle\_ecto, "~> 0.0"}

Configure file storage

config :waffle, storage: Waffle.Storage.Local

_Read more about storage configuration and the supported adapters (including S3)._

Create an uploader module with `mix waffle.g avatar`

defmodule MyApp.Avatar do
  use Waffle.Definition
  use Waffle.Ecto.Definition

  def storage\_dir(\_version, {\_file, user}) do
    "users/#{user.id}/avatar/"
  end
end

Update the user schema

schema "users" do
  field :avatar, Avatar.Type
end

Cast the file payload with a changeset

changeset
|> cast\_attachments(
  params,
  \[:avatar\],
  allow\_paths: true,
  allow\_urls: true
)

_Read more about Ecto integration in the WaffleEcto documentation._ _WaffleEcto supports changeset integration and versioned URLs for cache busting._

More Examples
-------------

-   An example for the Local storage driver
-   An example for the S3 storage driver

Attribution
-----------

This library was forked from Arc at version `v0.11.0`. Special thanks to Sean Stavropoulos (@stavro) for creating Arc.

Sponsors
--------

-   Evrone, custom software development company
-   Oficinaria, marketplace for in-person creative workshops in Brazil

License
-------

Copyright 2019 Boris Kuznetsov me@achempion.com

Copyright 2015 Sean Stavropoulos

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
  http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
