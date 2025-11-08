---
project: etso
stars: 384
description: Ecto 3 adapter allowing use of Ecto schemas held in ETS tables
url: https://github.com/evadne/etso
---

Etso
====

**Etso** is an ETS adapter, allowing you to use `Ecto` schemas with ETS tables.

Within this library, a bare-bones Ecto Adapter is provided. The Adapter transparently spins up ETS tables for each Ecto Repo and Schema combination. The tables are publicly accessible to enable concurrency, and tracked by reference to ensure encapsulation. Each ETS table is spun up by a dedicated Table Server under a shared Dynamic Supervisor.

For a detailed look as to what is available, check out Northwind Repo Test.

Highlights & Benefits
---------------------

Key highlights of this library are:

-   It transparently handles translations between `Ecto.Schema` structs and ETS tuples.
-   It knows how to form ETS Match Specifications for simple queries.

Key points to consider when adopting this library are:

-   It is suitable for rapid retrieval of simply formatted data, for example presets that do not change frequently.
-   It is not suitable for use as a full-fledged data layer unless your requirements are simple.

Feature Coverage
----------------

The following features are working:

-   Basic query scenarios (C / R / U / D)
    -   Insert all (`c:Ecto.Repo.insert_all/3`, etc.)
    -   Insert one (`c:Ecto.Repo.insert/2`, etc.)
    -   Get all (`c:Ecto.Repo.all/2`, etc.)
    -   Get by ID (`c:Ecto.Repo.get/3`, etc.)
    -   Get where (`Ecto.Query.where/3`, etc.)
    -   Delete by ID (`c:Ecto.Repo.delete/2`, etc.)
-   Selects
-   Assocs
-   Preloads

The Northwind Repo Test should give you a good idea of what’s included.

### Missing Features

The following features, for example, are missing:

-   Composite primary keys
-   Dynamic Repos (`c:Ecto.Repo.put_dynamic_repo/1`)
-   Aggregates (dynamic / static)
-   Joins
-   Windows
-   Transactions
-   Migrations
-   Locking

Installation
------------

Using Etso is a two-step process. First, include it in your application’s dependencies:

defp deps do
  \[
    {:etso, "~> 1.1.0"}
  \]
end

Afterwards, create a new `Ecto.Repo`, which uses `Etso.Adapter`:

defmodule MyApp.Repo do
  @otp\_app Mix.Project.config()\[:app\]
  use Ecto.Repo, otp\_app: @otp\_app, adapter: Etso.Adapter
end

Once this is done, you can use any Schema against the Repo normally, as you would with any other Repo. Check out the Northwind modules for an example.

Utilisation
-----------

Originally, Etso was created to answer the question of whether ETS and Ecto can be married together. It has since found some uses in production applications, serving as a Data Repository for pre-defined nested content. This proved invaluable for rapid iteration.

_If you have other Use Cases for this library, please add it here with a Pull Request._

-   The Erlef Website is using Etso to cache and query news and event posts that are parsed and imported into the Repo on application startup.

Further Note
------------

This repository is extracted from a prior project ETS Playground, which was created to support a session at ElixirConf EU 2019, _Leveraging ETS Effectively._

Specifically, this library was created to illustrate the point that ETS can serve as a scalable storage layer for data which changes infrequently. Check out the Northwind Importer for an example.

Acknowledgements
----------------

This project contains a copy of data obtained from the Northwind database, which is owned by Microsoft. It is included for demonstration and testing purposes only, and is excluded from the distribution. The Author thanks Microsoft Corporation for the inspiration.

The Author also wishes to thank the following individuals:

-   Wojtek Mach, for the inspiration regarding creation of an Ecto adapter for ETS.
    
-   Steven Holdsworth, for initial concept proofing and refinement.
    
-   Igor Kopestenski, for initial reviews.
    
-   David Schainker, for initial reviews, and for finding uses for this library.
    
-   Masanori Iwasaki, for support of `for…in` queries.
    
-   Kohei Noda, for fixing nested `{:orelse, …}` queries.
    
-   William Martins, for fixing primary key unicity check issues.
    
-   Soichiro Nishizawa, for providing the implementation of sorted results.
    
-   Doug W., for providing insights into parallel preloads.
    
-   Atanda Rasheed, for support of JSON extract paths.
