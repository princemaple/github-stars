---
project: kerosene
stars: 230
description: Pagination for Ecto and Pheonix.
url: https://github.com/elixirdrops/kerosene
---

Kerosene
========

Pagination for Ecto and Phoenix.

Installation
------------

The package is available in Hex, the package can be installed as:

Add kerosene to your list of dependencies in `mix.exs`:

def deps do
  \[{:kerosene, "~> 0.9.0"}\]
end

Add Kerosene to your `repo.ex`:

defmodule MyApp.Repo do
  use Ecto.Repo, 
    otp\_app: :testapp,
    adapter: Ecto.Adapters.Postgres
  use Kerosene, per\_page: 2
end

Usage
-----

Start paginating your queries

def index(conn, params) do
  {products, kerosene} \= 
  Product
  |> Product.with\_lowest\_price
  |> Repo.paginate(params)

  render(conn, "index.html", products: products, kerosene: kerosene)
end

Add view helpers to your view

defmodule MyApp.ProductView do
  use MyApp.Web, :view
  import Kerosene.HTML
end

Generate the links using the view helpers

<%\= paginate @conn, @kerosene %\>

Kerosene provides a list of themes for pagination. By default it uses bootstrap. To use some other, add to config/config.exs:

config :kerosene,
	theme: :foundation

If you need reduced number of links in pagination, you can use `simple mode` option, to display only Prev/Next links:

config :kerosene,
	mode:  :simple

Building apis or SPA's, no problem Kerosene has support for Json.

defmodule MyApp.ProductView do
  use MyApp.Web, :view
  import Kerosene.JSON

  def render("index.json", %{products: products, kerosene: kerosene, conn: conn}) do
    %{data: render\_many(products, MyApp.ProductView, "product.json"),
      pagination: paginate(conn, kerosene)}
  end

  def render("product.json", %{product: product}) do
    %{id: product.id,
      name: product.name,
      description: product.description,
      price: product.price}
  end
end

You can also send in options to paginate helper look at the docs for more details.

Contributing
------------

Please do send pull requests and bug reports, positive feedback is always welcome.

Acknowledgement
---------------

I would like to Thank

-   Matt (@mgwidmann)
-   Drew Olson (@drewolson)
-   Akira Matsuda (@amatsuda)

License
-------

Please take a look at LICENSE.md
