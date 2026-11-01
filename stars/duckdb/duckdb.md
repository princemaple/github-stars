---
project: duckdb
stars: 42724
description: DuckDB is a high-performance analytical database system
url: https://github.com/duckdb/duckdb
---

  

DuckDB
------

DuckDB is a high-performance analytical database system. It is designed to be fast, reliable, portable, and easy to use. DuckDB runs in-process inside your application, so there is no separate server to manage and no external dependencies. It can also read remote files, query other databases, and connect to other DuckDB instances when needed. It provides a rich SQL dialect with support far beyond basic SQL: arbitrary and nested correlated subqueries, window functions, collations, and complex types (arrays, structs, maps). Its friendly SQL extensions add syntax that makes queries shorter and easier to write.

DuckDB is available as a standalone CLI application and has clients for Python, R, Java, Rust, Go, Wasm, and many more, with deep integrations with packages such as pandas.

For more information on using DuckDB, please refer to the DuckDB documentation.

Reads and writes any data
-------------------------

DuckDB reads and writes a wide range of file formats, including CSV, Parquet, JSON, and Excel, directly from local disk or from remote endpoints such as S3, HTTP(S), Azure, and Google Cloud Storage. For many of these formats, including CSV, Parquet, and JSON, loading data is as simple as referencing the file in the FROM clause:

SELECT \* FROM 'myfile.csv';
SELECT \* FROM 'myfile.parquet';

DuckDB also works with open lakehouse formats. DuckLake stores table metadata in a SQL database rather than in metadata files, which removes the need for a separate catalog server while still providing ACID transactions, snapshots, and time travel. DuckDB also supports the Apache Iceberg and Delta Lake formats. Refer to our Data Import section for more information.

Connects to other databases
---------------------------

DuckDB can attach to other database systems and query them in place, so you can read, join, and move data across engines without a separate ETL step. It speaks the native protocols of PostgreSQL, MySQL, and SQLite.

DuckDB instances can also connect to each other over the quack protocol, which turns a DuckDB instance into a server that other DuckDB clients attach to over HTTP.

Extensible
----------

DuckDB has a modular extension mechanism: core extensions are bundled with DuckDB, while community and third-party extensions can be installed and loaded at runtime. Extensions add file formats, database connectors, and new functions, types, and more.

Installation
------------

If you want to install DuckDB, please see our installation page for instructions.

SQL Reference
-------------

The documentation contains a SQL introduction and reference.

Development
-----------

For development, DuckDB requires CMake, Python 3 and a `C++17` compliant compiler. In the root directory, run `make` to compile the sources. For development, use `make debug` to build a non-optimized debug version. You should run `make unit` and `make allunit` to verify that your version works properly after making changes. To test performance, you can run `BUILD_BENCHMARK=1 BUILD_TPCH=1 make` and then perform several standard benchmarks from the root directory by executing `./build/release/benchmark/benchmark_runner`. The details of benchmarks are in our Benchmark Guide.

Please also refer to our Build Guide and Contribution Guide.

Support
-------

See the Support Options page and the dedicated `endoflife.date` page.
