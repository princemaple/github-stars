---
project: ecto_psql_extras
stars: 388
description: Ecto PostgreSQL database performance insights. Locks, index usage, buffer cache hit ratios, vacuum stats and more.
url: https://github.com/pawurb/ecto_psql_extras
---

Ecto PSQL Extras
================

Elixir port of Heroku PG Extras. The goal of this project is to provide powerful insights into the PostgreSQL database for Elixir apps that are not using the Heroku PostgreSQL plugin.

Queries can be used to obtain information about a Postgres instance, that may be useful when analyzing performance issues. This includes information about locks, index usage, buffer cache hit ratios and vacuum statistics. Elixir API enables developers to easily integrate the tool into e.g. automatic monitoring tasks.

You can check out this blog post for detailed step by step tutorial on how to optimize PostgreSQL using PG Extras library.

This library is an optional dependency of Phoenix.LiveDashboard. Check it out if you want to see SQL metrics in the UI instead of a command line interface.

Alternative versions:

-   Ruby
    
-   Ruby on Rails
    
-   Rust
    
-   NodeJS
    
-   Python
    
-   Haskell
    

Installation
------------

`mix.exs`

 def deps do
    \[
      {:ecto\_psql\_extras, "~> 0.8"}
    \]
 end

Some of the queries (e.g., `calls` and `outliers`) require pg\_stat\_statements extension enabled.

You can check if it is enabled in your database by running:

EctoPSQLExtras.query(:extensions, YourApp.Repo)

You should see the similar line in the output:

| pg\_stat\_statements  | 1.7  | 1.7 | track execution statistics of all SQL statements executed |

Usage
-----

You can run queries using a simple API:

EctoPSQLExtras.cache\_hit(YourApp.Repo)

+----------------+------------------------+
|        Index and table hit rate         |
+----------------+------------------------+
| name           | ratio                  |
+----------------+------------------------+
| index hit rate | 0.97796610169491525424 |
| table hit rate | 0.96724294813466787989 |
+----------------+------------------------+

By default the ASCII table is displayed. Alternatively you can return the raw query results:

EctoPSQLExtras.index\_cache\_hit(YourApp.Repo, format: :raw)

%Postgrex.Result{
  columns: \["name", "buffer\_hits", "block\_reads", "total\_read", "ratio"\],
  command: :select,
  connection\_id: 413,
  messages: \[\],
  num\_rows: 1,
  rows: \[\["schema\_migrations", 0, 1, 1, "0"\]\]
}

You can also run queries by passing their name to the `query` method:

EctoPSQLExtras.query(:cache\_hit, YourApp.Repo)

Some methods accept an optional `args` param allowing you to customize queries:

EctoPSQLExtras.long\_running\_queries(YourApp.Repo, args: \[threshold: "200 milliseconds"\])

Diagnose report
---------------

The simplest way to start using `ecto_psql_extras` is to execute a `diagnose` method. It runs a set of checks and prints out a report highlighting areas that may require additional investigation:

EctoPSQLExtras.diagnose(YourApp.Repo)

Keep reading to learn about methods that `diagnose` uses under the hood.

Available methods
-----------------

### `missing_fk_indexes`

This method lists columns likely to be foreign keys (i.e. column name ending in `_id` and related table exists) which don't have an index. It's recommended to always index foreign key columns because they are used for searching relation objects.

You can add indexes on the columns returned by this query and later check if they are receiving scans using the unused\_indexes method. Please remember that each index decreases write performance and autovacuuming overhead, so be careful when adding multiple indexes to often updated tables.

```
EctoPSQLExtras.missing_fk_indexes(YourApp.Repo, args: [ table_name: "users" ])

+---------------------------------+
| Missing foreign key indexes     |
+-------------------+-------------+
| table             | column_name |
+-------------------+-------------+
| feedbacks         | team_id     |
| votes             | user_id     |
+-------------------+-------------+

```

`table_name` argument is optional, if omitted, the method will display missing fk indexes for all the tables.

`missing_fk_constraints`
------------------------

Similarly to the previous method, this one shows columns likely to be foreign keys that don't have a corresponding foreign key constraint. Foreign key constraints improve data integrity in the database by preventing relations with nonexisting objects. You can read more about the benefits of using foreign keys in this blog post.

```
EctoPSQLExtras.missing_fk_constraints(YourApp.Repo, args: [ table_name: "users" ])

+---------------------------------+
| Missing foreign key constraints |
+-------------------+-------------+
| table             | column_name |
+-------------------+-------------+
| feedbacks         | team_id     |
| votes             | user_id     |
+-------------------+-------------+

```

`table_name` argument is optional, if omitted, method will display missing fk constraints for all the tables.

### `cache_hit`

```

EctoPSQLExtras.cache_hit(YourApp.Repo)

      name      |         ratio
----------------+------------------------
 index hit rate | 0.99957765013541945832
 table hit rate |                   1.00
(2 rows)
```

This command provides information on the efficiency of the buffer cache, for both index reads (`index hit rate`) as well as table reads (`table hit rate`). A low buffer cache hit ratio can be a sign that the Postgres instance is too small for the workload.

More info

### `index_cache_hit`

```

EctoPSQLExtras.index_cache_hit(YourApp.Repo)

| name                  | buffer_hits | block_reads | total_read | ratio             |
+-----------------------+-------------+-------------+------------+-------------------+
| teams                 | 187665      | 109         | 187774     | 0.999419514948821 |
| subscriptions         | 5160        | 6           | 5166       | 0.99883855981417  |
| plans                 | 5718        | 9           | 5727       | 0.998428496595076 |
(truncated results for brevity)
```

The same as `cache_hit` with each table's indexes cache hit info displayed separately.

More info

### `table_cache_hit`

```

EctoPSQLExtras.table_cache_hit(YourApp.Repo)

| name                  | buffer_hits | block_reads | total_read | ratio             |
+-----------------------+-------------+-------------+------------+-------------------+
| plans                 | 32123       | 2           | 32125      | 0.999937743190662 |
| subscriptions         | 95021       | 8           | 95029      | 0.999915815172211 |
| teams                 | 171637      | 200         | 171837     | 0.99883610631005  |
(truncated results for brevity)
```

The same as `cache_hit` with each table's cache hit info displayed separately.

More info

### `db_settings`

```

EctoPSQLExtras.db_settings(YourApp.Repo)

             name             | setting | unit |
------------------------------+---------+------+
 checkpoint_completion_target | 0.7     |      |
 default_statistics_target    | 100     |      |
 effective_cache_size         | 1350000 | 8kB  |
 effective_io_concurrency     | 1       |      |
(truncated results for brevity)

```

This method displays values for selected PostgreSQL settings. You can compare them with settings recommended by PGTune and tweak values to improve performance.

More info

### `index_usage`

```

EctoPSQLExtras.index_usage(YourApp.Repo)

       relname       | percent_of_times_index_used | rows_in_table
---------------------+-----------------------------+---------------
 events              |                          65 |       1217347
 app_infos           |                          74 |        314057
 app_infos_user_info |                           0 |        198848
 user_info           |                           5 |         94545
 delayed_jobs        |                          27 |             0
(5 rows)
```

This command provides information on the efficiency of indexes, represented as what percentage of total scans were index scans. A low percentage can indicate under indexing, or wrong data being indexed.

### `locks`

```

EctoPSQLExtras.locks(YourApp.Repo)

 procpid | relname | transactionid | granted |     query_snippet     | mode             |       age
---------+---------+---------------+---------+-----------------------+-------------------------------------
   31776 |         |               | t       | <IDLE> in transaction | ExclusiveLock    |  00:19:29.837898
   31776 |         |          1294 | t       | <IDLE> in transaction | RowExclusiveLock |  00:19:29.837898
   31912 |         |               | t       | select * from hello;  | ExclusiveLock    |  00:19:17.94259
    3443 |         |               | t       |                      +| ExclusiveLock    |  00:00:00
         |         |               |         |    select            +|                  |
         |         |               |         |      pg_stat_activi   |                  |
(4 rows)
```

This command displays queries that have taken out an exclusive lock on a relation. Exclusive locks typically prevent other operations on that relation from taking place, and can be a cause of "hung" queries that are waiting for a lock to be granted.

More info

### `all_locks`

EctoPSQLExtras.all\_locks(YourApp.Repo)

This command displays all the current locks, regardless of their type.

### `outliers`

```

EctoPSQLExtras.outliers(YourApp.Repo, args: [limit: 20])

                   query                 |    exec_time     | prop_exec_time |   ncalls    | sync_io_time
-----------------------------------------+------------------+----------------+-------------+--------------
 SELECT * FROM archivable_usage_events.. | 154:39:26.431466 | 72.2%          | 34,211,877  | 00:00:00
 COPY public.archivable_usage_events (.. | 50:38:33.198418  | 23.6%          | 13          | 13:34:21.00108
 COPY public.usage_events (id, reporte.. | 02:32:16.335233  | 1.2%           | 13          | 00:34:19.784318
 INSERT INTO usage_events (id, retaine.. | 01:42:59.436532  | 0.8%           | 12,328,187  | 00:00:00
 SELECT * FROM usage_events WHERE (alp.. | 01:18:10.754354  | 0.6%           | 102,114,301 | 00:00:00
 UPDATE usage_events SET reporter_id =.. | 00:52:35.683254  | 0.4%           | 23,786,348  | 00:00:00
 INSERT INTO usage_events (id, retaine.. | 00:49:24.952561  | 0.4%           | 21,988,201  | 00:00:00
(truncated results for brevity)
```

This command displays statements, obtained from `pg_stat_statements`, ordered by the amount of time to execute in aggregate. This includes the statement itself, the total execution time for that statement, the proportion of total execution time for all statements that statement has taken up, the number of times that statement has been called, and the amount of time that statement spent on synchronous I/O (reading/writing from the file system).

Typically, an efficient query will have an appropriate ratio of calls to total execution time, with as little time spent on I/O as possible. Queries that have a high total execution time but low call count should be investigated to improve their performance. Queries that have a high proportion of execution time being spent on synchronous I/O should also be investigated.

More info

### `calls`

```

EctoPSQLExtras.calls(YourApp.Repo, args: [limit: 20])

                   query                 |    exec_time     | prop_exec_time |   ncalls    | sync_io_time
-----------------------------------------+------------------+----------------+-------------+--------------
 SELECT * FROM usage_events WHERE (alp.. | 01:18:11.073333  | 0.6%           | 102,120,780 | 00:00:00
 BEGIN                                   | 00:00:51.285988  | 0.0%           | 47,288,662  | 00:00:00
 COMMIT                                  | 00:00:52.31724   | 0.0%           | 47,288,615  | 00:00:00
 SELECT * FROM  archivable_usage_event.. | 154:39:26.431466 | 72.2%          | 34,211,877  | 00:00:00
 UPDATE usage_events SET reporter_id =.. | 00:52:35.986167  | 0.4%           | 23,788,388  | 00:00:00
 INSERT INTO usage_events (id, retaine.. | 00:49:25.260245  | 0.4%           | 21,990,326  | 00:00:00
 INSERT INTO usage_events (id, retaine.. | 01:42:59.436532  | 0.8%           | 12,328,187  | 00:00:00
(truncated results for brevity)
```

This command is much like `pg:outliers`, but ordered by the number of times a statement has been called.

More info

### `blocking`

```

EctoPSQLExtras.blocking(YourApp.Repo)

 blocked_pid |    blocking_statement    | blocking_duration | blocking_pid |                                        blocked_statement                           | blocked_duration
-------------+--------------------------+-------------------+--------------+------------------------------------------------------------------------------------+------------------
         461 | select count(*) from app | 00:00:03.838314   |        15682 | UPDATE "app" SET "updated_at" = '2013-03-04 15:07:04.746688' WHERE "id" = 12823149 | 00:00:03.821826
(1 row)
```

This command displays statements that are currently holding locks that other statements are waiting to be released. This can be used in conjunction with `pg:locks` to determine which statements need to be terminated in order to resolve lock contention.

More info

### `total_index_size`

```

EctoPSQLExtras.total_index_size(YourApp.Repo)

  size
-------
 28194 MB
(1 row)
```

This command displays the total size of all indexes on the database, in MB. It is calculated by taking the number of pages (reported in `relpages`) and multiplying it by the page size (8192 bytes).

### `index_size`

```

EctoPSQLExtras.index_size(YourApp.Repo)

                             name                              |  size
---------------------------------------------------------------+---------
 idx_activity_attemptable_and_type_lesson_enrollment           | 5196 MB
 index_enrollment_attemptables_by_attempt_and_last_in_group    | 4045 MB
 index_attempts_on_student_id                                  | 2611 MB
 enrollment_activity_attemptables_pkey                         | 2513 MB
 index_attempts_on_student_id_final_attemptable_type           | 2466 MB
 attempts_pkey                                                 | 2466 MB
 index_attempts_on_response_id                                 | 2404 MB
 index_attempts_on_enrollment_id                               | 1957 MB
 index_enrollment_attemptables_by_enrollment_activity_id       | 1789 MB
 enrollment_activities_pkey                                    |  458 MB
(truncated results for brevity)
```

This command displays the size of each each index in the database, in MB. It is calculated by taking the number of pages (reported in `relpages`) and multiplying it by the page size (8192 bytes).

### `table_size`

```

EctoPSQLExtras.table_size(YourApp.Repo)

                             name                              |  size
---------------------------------------------------------------+---------
 learning_coaches                                              |  196 MB
 states                                                        |  145 MB
 grade_levels                                                  |  111 MB
 charities_customers                                           |   73 MB
 charities                                                     |   66 MB
(truncated results for brevity)
```

This command displays the size of each table and materialized view in the database, in MB. It is calculated by using the system administration function `pg_table_size()`, which includes the size of the main data fork, free space map, visibility map and TOAST data.

### `table_indexes_size`

```

EctoPSQLExtras.table_indexes_size(YourApp.Repo)

                             table                             | indexes_size
---------------------------------------------------------------+--------------
 learning_coaches                                              |    153 MB
 states                                                        |    125 MB
 charities_customers                                           |     93 MB
 charities                                                     |     16 MB
 grade_levels                                                  |     11 MB
(truncated results for brevity)
```

This command displays the total size of indexes for each table and materialized view, in MB. It is calculated by using the system administration function `pg_indexes_size()`.

### `total_table_size`

```

EctoPSQLExtras.total_table_size(YourApp.Repo)

                             name                              |  size
---------------------------------------------------------------+---------
 learning_coaches                                              |  349 MB
 states                                                        |  270 MB
 charities_customers                                           |  166 MB
 grade_levels                                                  |  122 MB
 charities                                                     |   82 MB
(truncated results for brevity)
```

This command displays the total size of each table and materialized view in the database, in MB. It is calculated by using the system administration function `pg_total_relation_size()`, which includes table size, total index size and TOAST data.

### `unused_indexes`

```

EctoPSQLExtras.unused_indexes(YourApp.Repo, args: [min_scans: 20])

          table      |                       index                | index_size | index_scans
---------------------+--------------------------------------------+------------+-------------
 public.grade_levels | index_placement_attempts_on_grade_level_id | 97 MB      |           0
 public.observations | observations_attrs_grade_resources         | 33 MB      |           0
 public.messages     | user_resource_id_idx                       | 12 MB      |           0
(3 rows)
```

This command displays indexes that have < 50 scans recorded against them, and are greater than 5 pages in size, ordered by size relative to the number of index scans. This command is generally useful for eliminating indexes that are unused, which can impact write performance, as well as read performance should they occupy space in memory.

More info

### `duplicate_indexes`

```

EctoPSQLExtras.duplicate_indexes(YourApp.Repo)

| size       |  idx1        |  idx2          |  idx3    |  idx4     |
+------------+--------------+----------------+----------+-----------+
| 128 k      | users_pkey   | index_users_id |          |           |
```

This command displays multiple indexes that have the same set of columns, same opclass, expression and predicate - which make them equivalent. Usually it's safe to drop one of them.

### `null_indexes`

```

EctoPSQLExtras.null_indexes(YourApp.Repo, args: [min_relation_size_mb: 10])

   oid   |         index      | index_size | unique | indexed_column | null_frac | expected_saving
---------+--------------------+------------+--------+----------------+-----------+-----------------
  183764 | users_reset_token  | 1445 MB    | t      | reset_token    |   97.00%  | 1401 MB
   88732 | plan_cancelled_at  | 539 MB     | f      | cancelled_at   |    8.30%  | 44 MB
 9827345 | users_email        | 18 MB      | t      | email          |   28.67%  | 5160 kB

```

This commands displays indexes that contain `NULL` values. A high ratio of `NULL` values means that using a partial index excluding them will be beneficial in case they are not used for searching.

More info

### `seq_scans`

```

EctoPSQLExtras.seq_scans(YourApp.Repo)


               name                |  count
-----------------------------------+----------
 learning_coaches                  | 44820063
 states                            | 36794975
 grade_levels                      | 13972293
 charities_customers               |  8615277
 charities                         |  4316276
 messages                          |  3922247
 contests_customers                |  2915972
 classroom_goals                   |  2142014
(truncated results for brevity)
```

This command displays the number of sequential scans recorded against all tables, descending by count of sequential scans. Tables that have very high numbers of sequential scans may be under-indexed, and it may be worth investigating queries that read from these tables.

More info

### `long_running_queries`

```

EctoPSQLExtras.long_running_queries(YourApp.Repo, args: [threshold: "200 milliseconds"])


  pid  |    duration     |                                      query
-------+-----------------+---------------------------------------------------------------------------------------
 19578 | 02:29:11.200129 | EXPLAIN SELECT  "students".* FROM "students"  WHERE "students"."id" = 1450645 LIMIT 1
 19465 | 02:26:05.542653 | EXPLAIN SELECT  "students".* FROM "students"  WHERE "students"."id" = 1889881 LIMIT 1
 19632 | 02:24:46.962818 | EXPLAIN SELECT  "students".* FROM "students"  WHERE "students"."id" = 1581884 LIMIT 1
(truncated results for brevity)
```

This command displays currently running queries, that have been running for longer than 5 minutes, descending by duration. Very long running queries can be a source of multiple issues, such as preventing DDL statements completing or vacuum being unable to update `relfrozenxid`.

### `records_rank`

```

EctoPSQLExtras.records_rank(YourApp.Repo)

               name                | estimated_count
-----------------------------------+-----------------
 tastypie_apiaccess                |          568891
 notifications_event               |          381227
 core_todo                         |          178614
 core_comment                      |          123969
 notifications_notification        |          102101
 django_session                    |           68078
 (truncated results for brevity)
```

This command displays an estimated count of rows per table, descending by estimated count. The estimated count is derived from `n_live_tup`, which is updated by vacuum operations. Due to the way `n_live_tup` is populated, sparse vs. dense pages can result in estimations that are significantly out from the real count of rows.

### `bloat`

```

EctoPSQLExtras.bloat(YourApp.Repo)


 type  | schemaname |           object_name         | bloat |   waste
-------+------------+-------------------------------+-------+----------
 table | public     | bloated_table                 |   1.1 | 98 MB
 table | public     | other_bloated_table           |   1.1 | 58 MB
 index | public     | bloated_table::bloated_index  |   3.7 | 34 MB
 table | public     | clean_table                   |   0.2 | 3808 kB
 table | public     | other_clean_table             |   0.3 | 1576 kB
 (truncated results for brevity)
```

This command displays an estimation of table "bloat" – space allocated to a relation that is full of dead tuples, that has yet to be reclaimed. Tables that have a high bloat ratio, typically 10 or greater, should be investigated to see if vacuuming is aggressive enough, and can be a sign of high table churn.

More info

### `vacuum_stats`

```

EctoPSQLExtras.vacuum_stats(YourApp.Repo)

 schema |         table         | last_vacuum | last_autovacuum  |    rowcount    | dead_rowcount  | autovacuum_threshold | expect_autovacuum
--------+-----------------------+-------------+------------------+----------------+----------------+----------------------+-------------------
 public | log_table             |             | 2013-04-26 17:37 |         18,030 |              0 |          3,656       |
 public | data_table            |             | 2013-04-26 13:09 |             79 |             28 |             66       |
 public | other_table           |             | 2013-04-26 11:41 |             41 |             47 |             58       |
 public | queue_table           |             | 2013-04-26 17:39 |             12 |          8,228 |             52       | yes
 public | picnic_table          |             |                  |             13 |              0 |             53       |
 (truncated results for brevity)
```

This command displays statistics related to vacuum operations for each table, including an estimation of dead rows, last autovacuum and the current autovacuum threshold. This command can be useful when determining if current vacuum thresholds require adjustments, and to determine when the table was last vacuumed.

### `kill_all`

EctoPSQLExtras.kill\_all(YourApp.Repo)

This commands kills all the currently active connections to the database. It can be useful as a last resort when your database is stuck in a deadlock.

### `extensions`

EctoPSQLExtras.extensions(YourApp.Repo)

This command lists all the currently installed and available PostgreSQL extensions.

### `mandelbrot`

EctoPSQLExtras.mandelbrot(YourApp.Repo)

This command outputs the Mandelbrot set, calculated through SQL.

### `connections`

```

EctoPSQLExtras.connections(YourApp.Repo)
+----------------------------------------------+
|  Shows all the active database connections   |
+----------+----------------+------------------+
| username | client_address | application_name |
+----------+----------------+------------------+
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | your_app         |
| postgres | 172.20.0.1/32  | psql             |
+----------+----------------+------------------+
```

This command returns the list of all active connections to the database.

To have `application_name` populate in connections output, you need to configure your Phoenix applications' Repo by adding the `parameters` and set `application_name`:

config :your\_app, YourApp.Repo,
  username: "postgres",
  password: "postgres",
  hostname: "localhost",
  database: "your\_app\_dev",
  stacktrace: true,
  show\_sensitive\_data\_on\_connection\_error: true,
  pool\_size: 10,
  parameters: \[
    {:application\_name, "your\_app"}
  \]

Query sources
-------------

-   https://github.com/heroku/heroku-pg-extras
-   https://hakibenita.com/postgresql-unused-index-size
-   https://sites.google.com/site/itmyshare/database-tips-and-examples/postgres/useful-sqls-to-check-contents-of-postgresql-shared\_buffer
-   https://wiki.postgresql.org/wiki/Index\_Maintenance

Development
-----------

cp docker-compose.yml.sample docker-compose.yml
docker compose up -d
PG\_VERSION=11 mix test --include distribution \\
  && PG\_VERSION=12 mix test --include distribution \\
  && PG\_VERSION=13 mix test --include distribution \\
  && PG\_VERSION=14 mix test --include distribution \\
  && PG\_VERSION=15 mix test --include distribution

By default tests will use the following database connection URL compatible with the default `docker-compose.yml`:

`ecto://postgres:postgres@localhost:5432/ecto_psql_extras`

Optionally, you can override the following variables:

`POSTGRES_USER` `POSTGRES_PASSWORD` `POSTGRES_HOST` `POSTGRES_DB`

or provide the full `DATABASE_URL` connection URL.
