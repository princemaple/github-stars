---
project: arbor
stars: 243
description: Ecto elixir adjacency list and tree traversal. Supports Ecto versions 2 and 3.
url: https://github.com/coryodaniel/arbor
---

Arbor
=====

Ecto adjacency list and tree traversal using CTEs. Arbor uses a `parent_id` field and CTEs to create simple deep tree-like SQL hierarchies.

Installation
------------

If available in Hex, the package can be installed as:

Add `arbor` to your list of dependencies in `mix.exs`:

For Ecto SQL 3+:

  def deps do
    \[{:arbor, "~> 1.1.0"}\]
  end

For Ecto 2:

  def deps do
    \[{:arbor, "~> 1.0.6"}\]
  end

Benchmarks
----------

Arbor has been benchmarked on 10mm+ record tables with efficient results:

10,000,000 rows, 25% root

```
Running siblings
	10000 runs
	Total time: 1.793026000000013
	Avg: 1.7930260000000131e-4
Running children
	10000 runs
	Total time: 1.5967949999999786
	Avg: 1.5967949999999787e-4
Running descendants
	10000 runs
	Total time: 2.5418830000000012
	Avg: 2.5418830000000013e-4
Running ancestors
	10000 runs
	Total time: 2.87076499999998
	Avg: 2.87076499999998e-4
```

Usage
-----

defmodule Comment do
  use Ecto.Schema
  \# See config options below
  use Arbor.Tree, foreign\_key\_type: :binary\_id

  schema "comments" do
    field :body, :string
    belongs\_to :parent, \_\_MODULE\_\_

    timestamps
  end
end

All methods return composable Ecto queries. For in depth examples see the tests

### Roots

Returns root level records.

roots \= Comment.roots
        |> Repo.all

### Siblings

Return the siblings of a record.

siblings \= my\_comment
           |> Comment.siblings
           |> Comment.order\_by\_popularity
           |> Repo.all

### ancestors

Returns the entire ancestor (parent's parent's parent, etc) path to the record, but not including the record.

ancestors \= my\_comment
              |> Comment.ancestors
              |> Comment.order\_by\_inserted\_at
              |> Repo.all

### Descendants

Returns the entire descendant tree of a record, but not including the record.

descendants \= my\_comment
              |> Comment.descendants
              |> Comment.order\_by\_inserted\_at
              |> Repo.all

A second parameter can be passed to `descendants` to specify how deep from the root of the tree to retrieve the descendants from.

descendants \= my\_comment
              |> Comment.descendants(2)
              |> Comment.order\_by\_inserted\_at
              |> Repo.all

### Children

Returns the immediate children of a record.

children \= my\_comment
           |> Comment.children
           |> Repo.all

### Parent

Returns the record's parent.

parent \= my\_comment
         |> Comment.parent
         |> Repo.first

Options
-------

-   _table\_name_ - set the table name to use in CTEs
-   _tree\_name_ - set the name of the CTE
-   _primary\_key_ - defaults to field from Ecto's `@primary_key`
-   _primary\_key\_type_ - defaults to type from Ecto's `@primary_key`
-   _foreign\_key_ - defauts to `:parent_id`
-   _foreign\_key\_type_ - defaults to type from Ecto's `@primary_key`
-   _orphan\_strategy_ - defaults to `:nothing` currently unimplemented

Contributing
------------

You'll need PostgreSQL installed and a user that can create and drop databases.

There is a docker-compose file for your convienence.

You can specify it with the environment variable `ARBOR_DB_USER`.

The `mix test` task will drop and create the database for each run.

docker-compose up -d
ARBOR\_DB\_USER=postgres mix test
docker-compose down
