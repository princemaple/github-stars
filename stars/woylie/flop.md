---
project: flop
stars: 807
description: Filtering, ordering and pagination for Ecto
url: https://github.com/woylie/flop
---

Flop
====

Flop is an Elixir library designed to easily apply filtering, ordering, and pagination to your Ecto queries.

Features
--------

-   **Offset-based pagination:** Allows pagination through `offset`/`limit` or `page`/`page_size` parameters.
-   **Cursor-based pagination:** Also known as key set pagination, provides a more efficient alternative to offset-based pagination. Compatible with Relay pagination arguments.
-   **Sorting:** Applies sort parameters on multiple fields in any direction.
-   **Filtering:** Allows complex data filtering using multiple conditions, operators, and fields.
-   **Parameter validation:** Ensures the validity of provided parameters.
-   **Configurable filterable and sortable fields:** Only applies parameters to the fields that were explicitly configured as filterable or sortable.
-   **Join fields:** Allows the application of pagination, sort, and filter parameters on any named binding. Provides functions to help you to avoid unnecessary join clauses.
-   **Compound fields:** Provides the ability to apply filter parameters on multiple string fields, for example for a full name filter.
-   **Custom fields:** Provides an escape hatch for filters that Flop is not able to build on its own.
-   **Relay connection formatter:** Formats the connection in Relay style, providing edges, nodes, and page info.
-   **UI helpers and URL builders through Flop Phoenix:** Pagination, sortable tables and filter forms.

Installation
------------

To get started, add `flop` to your dependencies list in your project's `mix.exs` file:

def deps do
  \[
    {:flop, "~> 0.26.3"}
  \]
end

You can also configure a default repo for Flop by adding the following line to your config file:

config :flop, repo: MyApp.Repo

Instead of configuring Flop globally, you can also use a configuration module. Please refer to the Flop module documentation for more information.

Usage
-----

### Define sortable and filterable fields

To define sortable and filterable fields in your Ecto schema, you can derive `Flop.Schema`. This step is optional but highly recommended, particularly when the parameters passed to Flop's functions are user-provided. Deriving `Flop.Schema` ensures that Flop applies filtering and sorting parameters only to the fields you've explicitly configured.

defmodule MyApp.Pet do
  use Ecto.Schema

  @derive {
    Flop.Schema,
    filterable: \[:name, :species\],
    sortable: \[:name, :age, :species\]
  }

  schema "pets" do
    field :name, :string
    field :age, :integer
    field :species, :string
    field :social\_security\_number, :string
  end
end

Besides sortable and filterable fields, `Flop.Schema` also allows the definition of join fields, compound fields, or custom fields. You can also set maximum or default limits, among other options. For a comprehensive list of available options, check the `Flop.Schema` documentation.

### Query data

Use the `Flop.validate_and_run/3` or `Flop.validate_and_run!/3` function to both validate the parameters and fetch data from the database, and acquire pagination metadata in one operation.

Here is an example of how you might use this in your code:

defmodule MyApp.Pets do
  import Ecto.Query, warn: false

  alias Ecto.Changeset
  alias MyApp.{Pet, Repo}

  @spec list\_pets(map) ::
          {:ok, {\[Pet.t()\], Flop.Meta.t()}} | {:error, Flop.Meta.t()}
  def list\_pets(params \\\\ %{}) do
    Flop.validate\_and\_run(Pet, params, for: Pet)
  end
end

The `for` option sets the Ecto schema for which you derived `Flop.Schema`. If you haven't derived `Flop.Schema` as described above, this option can be omitted. However, this is not recommended unless all parameters are generated internally and are guaranteed to be safe.

On success, `Flop.validate_and_run/3` returns an `:ok` tuple. The second element of this tuple is another tuple containing the fetched data and metadata.

{:ok, {\[%Pet{}\], %Flop.Meta{}}}

You can learn more about the `Flop.Meta` struct in the module documentation.

Alternatively, you may separate parameter validation and data fetching into different steps using the Flop.validate/2, Flop.validate!/2, and Flop.run/3 functions. This allows you to manipulate the validated parameters, to modify the query depending on the parameters, or to move the parameter validation to a different layer of your application.

with {:ok, flop} <- Flop.validate(params, for: Pet) do
  Flop.run(Pet, flop, for: Pet)
end

The aforementioned functions internally call the lower-level functions `Flop.all/3`, `Flop.meta/3`, and `Flop.count/3`. If you have advanced requirements, you might prefer to use these functions directly. However, it's important to note that these lower-level functions do not validate the parameters. If parameters are generated based on user input, they should always be validated first using `Flop.validate/2` or `Flop.validate!/2` to ensure safe execution.

The examples above assume that you configured a default repo. However, you can also pass the repo directly to the functions:

Flop.validate\_and\_run(Pet, flop, repo: MyApp.Repo)
Flop.all(Pet, flop, repo: MyApp.Repo)
Flop.meta(Pet, flop, repo: MyApp.Repo)

For more detailed information, refer the documentation.

Parameter format
----------------

The Flop library requires parameters to be provided in a specific format as a map. This map can be translated into a URL query parameter string, typically for use in a web framework like Phoenix.

### Pagination

#### Offset / limit

You can specify an offset to start from and a limit to the number of results.

%{offset: 20, limit: 10}

This translates to the following query parameter string:

?offset=20&limit=10

#### Page / page size

You can specify the page number and the size of each page.

%{page: 2, page\_size: 10}

This translates to the following query parameter string:

?page=2&page\_size=10

#### Cursor

You can fetch a specific number of results before or after a given cursor.

%{first: 10, after: "g3QAAAABZAACaWRiAAACDg=="}
%{last: 10, before: "g3QAAAABZAACaWRiAAACDg=="}

These translate to the following query parameter strings:

?first=10&after=g3QAAAABZAACaWRiAAACDg==
?last=10&before=g3QAAAABZAACaWRiAAACDg==

The cursor pagination arguments are based on the GraphQL Cursor Connection Specification, section 4.

### Ordering

To sort the results, specify fields to order by and the direction of sorting for each field.

%{order\_by: \[:name, :age\], order\_directions: \[:asc, :desc\]}

This translates to the following query parameter string:

?order\_by\[\]=name&order\_by\[\]=age&order\_directions\[\]=asc&order\_directions\[\]=desc

### Filters

You can filter the results by providing a field, an operator, and a value. The operator is optional and defaults to `==`. Multiple filters are combined with a logical `AND`. At the moment, combining filters with `OR` is not supported.

%{filters: \[%{field: :name, op: :ilike\_and, value: "Jane"}\]}

This translates to the following query parameter string:

?filters\[0\]\[field\]=name&filters\[0\]\[op\]=ilike\_and&filters\[0\]\[value\]=Jane

Refer to the `Flop.Filter` documentation and `t:Flop.t/0` type documentation for more details on using filters.

Internal parameters
-------------------

Flop is designed to manage parameters that come from the user side. While it is possible to alter those parameters and append extra filters upon receiving them, it is advisable to clearly differentiate parameters coming from outside and the parameters that your application adds internally.

Consider the scenario where you need to scope a query based on the current user. In this case, it is better to create a separate function that introduces the necessary `WHERE` clauses:

def list\_pets(%{} \= params, %User{} \= current\_user) do
  Pet
  |> scope(current\_user)
  |> Flop.validate\_and\_run(params, for: Pet)
end

defp scope(q, %User{role: :admin}), do: q
defp scope(q, %User{id: user\_id}), do: where(q, user\_id: ^user\_id)

If you need to add extra filters that are only used internally and aren't exposed to the user, you can pass them as a separate argument. This same argument can be used to override certain options depending on the context in which the function is called.

def list\_pets(%{} \= params, opts \\\\ \[\], %User{} \= current\_user) do
  flop\_opts \=
    opts
    |> Keyword.take(\[
      :default\_limit,
      :default\_pagination\_type,
      :pagination\_types
    \])
    |> Keyword.put(:for, Pet)

  Pet
  |> scope(current\_user)
  |> apply\_filters(opts)
  |> Flop.validate\_and\_run(params, flop\_opts)
end

defp scope(q, %User{role: :admin}), do: q
defp scope(q, %User{id: user\_id}), do: where(q, user\_id: ^user\_id)

defp apply\_filters(q, opts) do
  Enum.reduce(opts, q, fn
    {:last\_health\_check, dt}, q \-> where(q, \[p\], p.last\_health\_check < ^dt)
    {:reminder\_service, bool}, q \-> where(q, \[p\], p.reminder\_service \== ^bool)
    \_, q \-> q
  end)
end

With this approach, you maintain a clean separation between user-driven parameters and system-driven parameters, leading to more maintainable and less error-prone code.

Relay and Absinthe
------------------

The `Flop.Relay` module is useful if you are using absinthe with absinthe\_relay, or if you simply need to adhere to the Relay cursor specification. This module provides functions that help transform query responses into a format compatible with Relay.

Consider the scenario where you have defined node objects for owners and pets, along with a connection field for pets on the owner node object.

node object(:owner) do
  field :name, non\_null(:string)
  field :email, non\_null(:string)

  connection field :pets, node\_type: :pet do
    resolve &MyAppWeb.Resolvers.Pet.list\_pets/2
  end
end

node object(:pet) do
  field :name, non\_null(:string)
  field :age, non\_null(:integer)
  field :species, non\_null(:string)
end

connection(node\_type: :pet)

Absinthe Relay will establish the arguments `after`, `before`, `first` and `last` on the `pets` field. These argument names align with those used by Flop, facilitating their application.

Next, we'll define a `list_pets_by_owner/2` function in the Pets context.

defmodule MyApp.Pets do
  import Ecto.Query

  alias MyApp.{Owner, Pet, Repo}

  @spec list\_pets\_by\_owner(Owner.t(), map) ::
          {:ok, {\[Pet.t()\], Flop.Meta.t()}} | {:error, Flop.Meta.t()}
  def list\_pets\_by\_owner(%Owner{id: owner\_id}, params \\\\ %{}) do
    Pet
    |> where(owner\_id: ^owner\_id)
    |> Flop.validate\_and\_run(params, for: Pet)
  end
end

Now, within your resolver, you merely need to invoke the function and call `Flop.Relay.connection_from_result/1`, which transforms the result into a tuple composed of the edges and the page\_info, as required by `absinthe_relay`.

defmodule MyAppWeb.Resolvers.Pet do
  alias MyApp.{Owner, Pet}

  def list\_pets(args, %{source: %Owner{} \= owner} \= resolution) do
    with {:ok, result} <- Pets.list\_pets\_by\_owner(owner, args) do
      {:ok, Flop.Relay.connection\_from\_result(result)}
    end
  end
end

In case you want to introduce additional filter arguments, you can employ `Flop.nest_filters/3` to convert simple filter arguments into Flop filters, without necessitating API users to understand the Flop filter format.

Let's add `name` and `species` filter arguments to the `pets` connection field.

node object(:owner) do
  field :name, non\_null(:string)
  field :email, non\_null(:string)

  connection field :pets, node\_type: :pet do
    arg :name, :string
    arg :species, :string

    resolve &MyAppWeb.Resolvers.Pet.list\_pets/2
  end
end

Assuming that these fields have been already configured as filterable with `Flop.Schema`, we can use `Flop.nest_filters/3` to take the filter arguments and transform them into a list of Flop filters.

defmodule MyAppWeb.Resolvers.Pet do
  alias MyApp.{Owner, Pet}

  def list\_pets(args, %{source: %Owner{} \= owner} \= resolution) do
    args \= nest\_filters(args, \[:name, :species\])

    with {:ok, result} <- Pets.list\_pets\_by\_owner(owner, args) do
      {:ok, Flop.Relay.connection\_from\_result(result)}
    end
  end
end

`Flop.nest_filters/3` uses the equality operator `:==` by default. You can override the default operator per field.

args \= nest\_filters(args, \[:name, :species\], operators: %{name: :ilike\_and})

Flop Phoenix
------------

Flop Phoenix is a companion library that provides Phoenix components for pagination, sortable tables, and filter forms, usable with both Phoenix LiveView and in dead views. It also defines helper functions to build URLs with Flop query parameters.

Development
-----------

Pull requests are welcome, but for non-trivial changes like new features or API changes, please open an issue first and describe what you plan to do. Otherwise, you risk spending time on development work that might not be accepted.

The database tests require running Postgres and MySQL instances. There is a docker compose configuration you can use:

docker compose up

Please ensure that the following checks pass before requesting a review:

mix format --check-formatted
mix credo
mix compile --warnings-as-errors
mix test --warnings-as-errors
mix test.postgres --warnings-as-errors
mix dialyzer

Note that the tests are split up. `mix test` only tests common functionality without database interaction, and `mix test.{adapter}` runs tests that involve database queries.

-   `mix test` - common functionality
-   `mix test.postgres`
-   `mix test.mysql`
-   `mix test.sqlite`
-   `mix test.all` - all database adapters

At the moment, only `mix test` and `mix test.postgres` are required to pass.

For general contribution guidelines, refer to https://github.com/woylie/.github/blob/main/CONTRIBUTING.md.
