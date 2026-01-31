---
project: geolix
stars: 193
description: IP information lookup provider
url: https://github.com/elixir-geolix/geolix
---

Geolix
======

IP information lookup provider.

Package Setup
-------------

To use Geolix with your projects, edit your `mix.exs` file and add the project as a dependency:

defp deps do
  \[
    \# ...
    {:geolix, "~> 2.0"},
    \# ...
  \]
end

If you want to use a manual supervision approach (without starting the application) please look at the inline documentation of `Geolix.Supervisor`.

Application Configuration
-------------------------

Every lookup request is passed to all configured databases:

config :geolix,
  databases: \[
    %{
      id: :city,
      adapter: MyAdapter,
      source: "/absolute/path/to/city.db"
    },
    %{
      id: :country,
      adapter: MyAdapter,
      source: "/absolute/path/to/country.db"
    }
  \]

Above configuration will use the adapter `MyAdapter` and return a result for an example `:city` and `:country` database. The exact configuration values you need to provide are defined by the adapter you are using.

More details on database configuration can be found inline at the main `Geolix` module.

Adapters
--------

All the work done by Geolix is handled using adapters. These adapters can use a database, a webservice or any other means available to handle your lookup requests.

Known adapters:

-   `Geolix.Adapter.Fake`
-   `Geolix.Adapter.LookupCache`
-   `Geolix.Adapter.MMDB2`

For detailed information how to configure the adapter of your choice please read the adapter's configuration.

### Fake Adapter

Pre-packaged is a fake/static adapter (`Geolix.Adapter.Fake`) working on a plain `Agent` holding your IP lookup responses. An example of how you might use this adapter:

config :geolix,
  databases: \[
    %{
      id: :country,
      adapter: Geolix.Adapter.Fake,
      data: %{
        {1, 1, 1, 1} \=> %{country: %{iso\_code: "US"}},
        {2, 2, 2, 2} \=> %{country: %{iso\_code: "GB"}}
      }
    }
  \]

Please refer to the inline documentation of the `Geolix.Adapter.Fake` module for more details.

### Custom Adapters

Adapters are expected to adhere to the `Geolix.Adapter` behaviour. As a starting point for writing a custom adapter you can look at the packaged `Geolix.Adapter.Fake`.

Basic Usage
-----------

Lookups are done using `Geolix.lookup/1,2`:

iex(1)\> Geolix.lookup("127.0.0.1")
%{
  city: %{...},
  country: %{...}
}

iex(2)\> Geolix.lookup({127, 0, 0, 1}, where: :my\_database)
%{...}

Full documentation is available inline in the `Geolix` module and at https://hexdocs.pm/geolix.

License
-------

Apache License, Version 2.0
