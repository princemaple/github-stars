---
project: zombodb
stars: 4744
description: Making Postgres and Elasticsearch work together like it's 2023
url: https://github.com/zombodb/zombodb
---

###### Making Postgres and Elasticsearch work together like it's 2023

Readme
------

ZomboDB brings powerful text-search and analytics features to Postgres by using Elasticsearch as an index type. Its comprehensive query language and SQL functions enable new and creative ways to query your relational data.

From a technical perspective, ZomboDB is a 100% native Postgres extension written in Rust with PGRX. ZomboDB uses Postgres's Index Access Method API to directly manage and optimize ZomboDB's specialized indices. As a native Postgres index type, ZomboDB allows you to `CREATE INDEX ... USING zombodb` on your existing Postgres tables. At that point, ZomboDB takes over and fully manages the remote Elasticsearch index, guaranteeing transactionally-correct text-search query results.

ZomboDB is fully compatible with all of Postgres's query plan types and most SQL commands such as `CREATE INDEX`, `COPY`, `INSERT`, `UPDATE`, `DELETE`, `SELECT`, `ALTER`, `DROP`, `REINDEX`, `(auto)VACUUM`, etc.

It doesn’t matter if you’re using an Elasticsearch cloud provider or managing your own cluster -- ZomboDB communicates with Elasticsearch via its RESTful APIs so you’re covered either way.

ZomboDB allows you to use the power and scalability of Elasticsearch directly from Postgres. You don’t have to manage transactions between Postgres and Elasticsearch, asynchronous indexing pipelines, complex reindexing processes, or multiple data-access code paths -- ZomboDB does it all for you.

Quick Links
-----------

-   Installation from Binaries (sponsors only)
-   Installation from Source (everyone)
-   Getting Started Tutorial
-   Important Things to Know
-   Creating Indexes
-   ZQL (ZomboDB Query Language)
-   Query Builder API
-   Cross-Index Joins
-   Aggregations
-   Scoring and Highlighting
-   SQL Functions
-   Configuration Settings
-   Index Management
-   Type Mapping
-   Elasticsearch \_cat API
-   VACUUM Support

Features
--------

-   MVCC-correct text-search and aggregation results
-   Managed and queried via standard SQL
-   Works with current Elasticsearch releases (no plugins required)
-   Query using
    -   Elasticsearch's query string syntax via `dsl.query_string()`
    -   ZQL -- ZomboDB's custom query language
    -   Raw Elasticsearch QueryDSL JSON
    -   ZomboDB's type-safe query builder SQL syntax
    -   Any combination of the above, even in combination with standard SQL
-   Scoring and Highlighting Support
-   Support for all Elasticsearch aggregations
-   Automatic Elasticsearch Mapping Generation
    -   Ability to map custom domains
    -   Per-field custom mappings
    -   `json/jsonb` automatically mapped as dynamic nested objects
    -   Supports the full set of Elasticsearch language analyzers
    -   Supports Elasticsearch's similarity module
-   Hot standby compatible
-   Support for indexing and searching PostGIS `geometry` and `geography` types

Current Limitations
-------------------

-   Only one ZomboDB index per table
-   ZomboDB indexes with predicates (i.e., partial indexes) are not supported
-   `CREATE INDEX CONCURRENTLY` is not supported

These limitations may be addressed in future versions of ZomboDB.

System Requirements
-------------------

Product

Version

Postgres

12.x, 13.x, 14.x, 15.x

Elasticsearch

\>=7.10

Sponsorship and Downloads
-------------------------

Please see https://github.com/sponsors/eeeebbbbrrrr for sponsorship details. Your sponsorship at any tier is greatly appreciated and helps keep ZomboDB moving forward.

Note that ZomboDB is only available in binary form for certain sponsor tiers.

When you become a sponsor at a tier that provides binary downloads, please request a download key from https://www.zombodb.com/services/. Please do the same if you sponsor a tier that provides access to ZomboDB's private Discord server.

Quick Overview
--------------

Note that this is just a quick overview. Please read the getting started tutorial for more details.

Create the extension:

CREATE EXTENSION zombodb;

Create a table:

CREATE TABLE products (
    id SERIAL8 NOT NULL PRIMARY KEY,
    name text NOT NULL,
    keywords varchar(64)\[\],
    short\_summary text,
    long\_description zdb.fulltext, 
    price bigint,
    inventory\_count integer,
    discontinued boolean default false,
    availability\_date date
);

\-- insert some data

Create a ZomboDB index:

CREATE INDEX idxproducts 
          ON products 
       USING zombodb ((products.\*)) 
        WITH (url\='localhost:9200/');

Query it:

SELECT \* 
  FROM products 
 WHERE products \==> '(keywords:(sports OR box) OR long\_description:"wooden away"~5) AND price:\[1000 TO 20000\]';

Contact Information
-------------------

-   https://www.zombodb.com
-   Google Group: zombodb@googlegroups.com
-   Twitter: @zombodb
-   via GitHub Issues and Pull Requests
-   https://www.zombodb.com/services/ or info@zombodb.com for commercial support

History
-------

The name is an homage to zombo.com and its long history of continuous self-affirmation.

Historically, ZomboDB began in 2013 by Technology Concepts & Design, Inc as a closed-source effort to provide transaction-safe text-search on top of Postgres tables. While Postgres's full-text search features are useful, they're not necessarily adequate for 200-column-wide tables with 100 million rows, each containing large text content.

Initially built on Postgres's Foreign Data Wrapper API, ZomboDB quickly evolved into an index type so that queries are MVCC-safe and standard SQL can be used to query and manage indices.

Elasticsearch was chosen as the backing search index because of its horizontal scaling abilities, performance, and general ease of use.

ZomboDB was open-sourced in July 2015 and has since been used in numerous production systems of various sizes and complexity.

License
-------

Copyright 2018-2023 ZomboDB, LLC

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
