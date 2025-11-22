---
project: paginator
stars: 812
description: Cursor-based pagination for Elixir Ecto
url: https://github.com/duffelhq/paginator
---

Paginator
=========

Cursor based pagination for Elixir Ecto.

Why?
----

There are several ways to implement pagination in a project and they all have pros and cons depending on your situation.

### Limit-offset

This is the easiest method to use and implement: you just have to set `LIMIT` and `OFFSET` on your queries and the database will return records based on this two parameters. Unfortunately, it has two major drawbacks:

-   Inconsistent results: if the dataset changes while you are querying, the results in the page will shift and your user might end seeing records they have already seen and missing new ones.
    
-   Inefficiency: `OFFSET N` instructs the database to skip the first N results of a query. However, the database must still fetch these rows from disk and order them before it can returns the ones requested. If the dataset you are querying is large this will result in significant slowdowns.
    

### Cursor-based (a.k.a keyset pagination)

This method relies on opaque cursor to figure out where to start selecting records. It is more performant than `LIMIT-OFFSET` because it can filter records without traversing all of them.

It's also consistent, any insertions/deletions before the current page will leave results unaffected.

It has some limitations though: for instance you can't jump directly to a specific page. This may not be an issue for an API or if you use infinite scrolling on your website.

### Learn more

-   http://use-the-index-luke.com/no-offset
-   http://use-the-index-luke.com/sql/partial-results/fetch-next-page
-   https://www.citusdata.com/blog/2016/03/30/five-ways-to-paginate/
-   https://developer.twitter.com/en/docs/tweets/timelines/guides/working-with-timelines

Getting started
---------------

defmodule MyApp.Repo do
  use Ecto.Repo,
    otp\_app: :my\_app,
    adapter: Ecto.Adapters.Postgres

  use Paginator
end

query \= from(p in Post, order\_by: \[asc: p.inserted\_at, asc: p.id\])

page \= MyApp.Repo.paginate(query, cursor\_fields: \[:inserted\_at, :id\], limit: 50)

\# \`page.entries\` contains all the entries for this page.
\# \`page.metadata\` contains the metadata associated with this page (cursors, limit, total count)

Installation
------------

Add `:paginator` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:paginator, "~> 1.2.0"}
  \]
end

Usage
-----

Add `Paginator` to your repo:

defmodule MyApp.Repo do
  use Ecto.Repo,
    otp\_app: :my\_app,
    adapter: Ecto.Adapters.Postgres

  use Paginator
end

Use the `paginate` function to paginate your queries:

query \= from(p in Post, order\_by: \[asc: p.inserted\_at, asc: p.id\])

\# return the first 50 posts
%{entries: entries, metadata: metadata}
  \= Repo.paginate(
    query,
    cursor\_fields: \[:inserted\_at, :id\],
    limit: 50
  )

\# assign the \`after\` cursor to a variable
cursor\_after \= metadata.after

\# return the next 50 posts
%{entries: entries, metadata: metadata}
  \= Repo.paginate(
    query,
    after: cursor\_after,
    cursor\_fields: \[{:inserted\_at, :asc}, {:id, :asc}\],
    limit: 50
  )

\# assign the \`before\` cursor to a variable
cursor\_before \= metadata.before

\# return the previous 50 posts (if no post was created in between it should be
\# the same list as in our first call to \`paginate\`)
%{entries: entries, metadata: metadata}
  \= Repo.paginate(
    query,
    before: cursor\_before,
    cursor\_fields: \[:inserted\_at, :id\],
    limit: 50
  )

\# return total count
\# NOTE: this will issue a separate \`SELECT COUNT(\*) FROM table\` query to the
\# database.
%{entries: entries, metadata: metadata}
  \= Repo.paginate(
    query,
    include\_total\_count: true,
    cursor\_fields: \[:inserted\_at, :id\],
    limit: 50
  )

IO.puts "total count: #{metadata.total\_count}"

Dynamic expressions
-------------------

  query \=
    from(
      f in Post,
      \# Alias for fragment must match witch cursor field name in fetch\_cursor\_value\_fun and cursor\_fields
      select\_merge: %{
        rank\_value:
          fragment("ts\_rank(document, plainto\_tsquery('simple', ?)) AS rank\_value", ^q)
      },
      where: fragment("document @@ plainto\_tsquery('simple', ?)", ^q),
      order\_by: \[
        desc: fragment("rank\_value"),
        desc: f.id
      \]
    )
    query
    |> Repo.paginate(
      limit: 30,
      fetch\_cursor\_value\_fun: fn
        \# Here we build the rank\_value for each returned row
        schema, :rank\_value \->
          {:ok, %{rows: \[\[rank\_value\]\]}} \=
            Repo.query("SELECT ts\_rank($1, plainto\_tsquery('simple', $2))", \[
              schema.document,
              q
            \])
          rank\_value
        schema, field \->
          Paginator.default\_fetch\_cursor\_value(schema, field)
      end,
      cursor\_fields: \[
        {:rank\_value, \# Here we build the rank\_value that will be used in the where clause
         fn \->
           dynamic(
             \[x\],
             fragment("ts\_rank(document, plainto\_tsquery('simple', ?))", ^q)
           )
         end},
        :id
      \]
    )

Security Considerations
-----------------------

`Repo.paginate/4` will throw an `ArgumentError` should it detect an executable term in the cursor parameters passed to it (`before`, `after`). This is done to protect you from potential side-effects of malicious user input, see paginator\_test.exs.

Indexes
-------

If you want to reap all the benefits of this method it is better that you create indexes on the columns you are using as cursor fields.

### Example

\# If your cursor fields are: \[:inserted\_at, :id\]
\# Add the following in a migration

create index("posts", \[:inserted\_at, :id\])

Caveats
-------

-   This method requires a deterministic sort order. If the columns you are currently using for sorting don't match that definition, just add any unique column and extend your index accordingly.
-   You need to add `:order_by` clauses yourself before passing your query to `paginate/2`. In the future we might do that for you automatically based on the fields specified in `:cursor_fields`.
-   There is an outstanding issue where Postgrex fails to properly builds the query if it includes custom PostgreSQL types.
-   This library has only be tested with PostgreSQL.

Documentation
-------------

Documentation is written into the library, you will find it in the source code, accessible from `iex` and of course, it all gets published to hexdocs.

Contributing
------------

### Running tests

Clone the repo and fetch its dependencies:

```
$ git clone https://github.com/duffelhq/paginator.git
$ cd paginator
$ mix deps.get
$ mix test
```

### Building docs

```
$ mix docs
```

Copyright and License
---------------------

Copyright (c) 2017 Steve Domin.

This software is licensed under the MIT license.
