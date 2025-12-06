---
project: duckdb
stars: 34595
description: DuckDB is an analytical in-process SQL database management system
url: https://github.com/duckdb/duckdb
---

  

DuckDB
------

DuckDB is a high-performance analytical database system. It is designed to be fast, reliable, portable, and easy to use. DuckDB provides a rich SQL dialect with support far beyond basic SQL. DuckDB supports arbitrary and nested correlated subqueries, window functions, collations, complex types (arrays, structs, maps), and several extensions designed to make SQL easier to use.

DuckDB is available as a standalone CLI application and has clients for Python, R, Java, Wasm, etc., with deep integrations with packages such as pandas and dplyr.

For more information on using DuckDB, please refer to the DuckDB documentation.

Installation
------------

If you want to install DuckDB, please see our installation page for instructions.

Data Import
-----------

For CSV files and Parquet files, data import is as simple as referencing the file in the FROM clause:

SELECT \* FROM 'myfile.csv';
SELECT \* FROM 'myfile.parquet';

Refer to our Data Import section for more information.

SQL Reference
-------------

The documentation contains a SQL introduction and reference.

Development
-----------

For development, DuckDB requires CMake, Python 3 and a `C++11` compliant compiler. In the root directory, run `make` to compile the sources. For development, use `make debug` to build a non-optimized debug version. You should run `make unit` and `make allunit` to verify that your version works properly after making changes. To test performance, you can run `BUILD_BENCHMARK=1 BUILD_TPCH=1 make` and then perform several standard benchmarks from the root directory by executing `./build/release/benchmark/benchmark_runner`. The details of benchmarks are in our Benchmark Guide.

Please also refer to our Build Guide and Contribution Guide.

Support
-------

See the Support Options page and the dedicated `endoflife.date` page.
