---
project: oban
stars: 3798
description: 💎 Robust job processing in Elixir, backed by modern PostgreSQL, SQLite3, and MySQL
url: https://github.com/oban-bg/oban
---

Robust job processing in Elixir, backed by modern PostgreSQL, MySQL, and SQLite3. Reliable,  
observable, and loaded with enterprise grade features.

Table of Contents
-----------------

-   Features
-   Oban Pro
-   Engines
-   Requirements
-   Installation
-   Quick Getting Started
-   Learning
-   Community
-   Contributing

* * *

Note

This README is for the unreleased main branch, please reference the official documentation on hexdocs for the latest stable release.

* * *

Features
--------

Oban's primary goals are **reliability**, **consistency** and **observability**.

Oban is a powerful and flexible library that can handle a wide range of background job use cases, and it is well-suited for systems of any size. It provides a simple and consistent API for scheduling and performing jobs, and it is built to be fault-tolerant and easy to monitor.

Oban is fundamentally different from other background job processing tools because _it retains job data for historic metrics and inspection_. You can leave your application running indefinitely without worrying about jobs being lost or orphaned due to crashes.

#### Advantages Over Other Tools

-   **Fewer Dependencies** — If you are running a web app there is a _very good_ chance that you're running on top of a SQL database. Running your job queue within a SQL database minimizes system dependencies and simplifies data backups.
    
-   **Transactional Control** — Enqueue a job along with other database changes, ensuring that everything is committed or rolled back atomically.
    
-   **Database Backups** — Jobs are stored inside of your primary database, which means they are backed up together with the data that they relate to.
    

#### Advanced Features

-   **Isolated Queues** — Jobs are stored in a single table but are executed in distinct queues. Each queue runs in isolation, with its own concurrency limits, ensuring that a job in a single slow queue can't back up other faster queues.
    
-   **Isolated Jobs** — Every job runs in a dedicated process to provide fully concurrent execution, a clean environment between jobs, and efficient cleanup after the job runs.
    
-   **Queue Control** — Queues can be started, stopped, paused, resumed and scaled independently at runtime locally or across _all_ running nodes (even in environments like Heroku, without distributed Erlang).
    
-   **Resilient Queues** — Failing queries won't crash the entire supervision tree, instead a backoff mechanism will safely retry them again in the future.
    
-   **Job Canceling** — Jobs can be canceled in the middle of execution regardless of which node they are running on. This stops the job at once and flags it as `cancelled`.
    
-   **Triggered Execution** — Insert triggers ensure that jobs are dispatched on all connected nodes as soon as they are inserted into the database.
    
-   **Unique Jobs** — Duplicate work can be avoided through unique job controls. Uniqueness can be enforced at the argument, queue, worker and even sub-argument level for any period of time.
    
-   **Scheduled Jobs** — Jobs can be scheduled at any time in the future, down to the second.
    
-   **Periodic (CRON) Jobs** — Automatically enqueue jobs on a cron-like schedule. Duplicate jobs are never enqueued, no matter how many nodes you're running.
    
-   **Job Priority** — Prioritize jobs within a queue to run ahead of others with ten levels of granularity.
    
-   **Historic Metrics** — After a job is processed the row isn't deleted. Instead, the job is retained in the database to provide metrics. This allows users to inspect historic jobs and to see aggregate data at the job, queue or argument level.
    
-   **Node Metrics** — Every queue records metrics to the database during runtime. These are used to monitor queue health across nodes and may be used for analytics.
    
-   **Graceful Shutdown** — Queue shutdown is delayed so that slow jobs can finish executing before shutdown. When shutdown starts queues are paused and stop executing new jobs. Any jobs left running after the shutdown grace period may be rescued later.
    
-   **Telemetry Integration** — Job life-cycle events are emitted via Telemetry integration. This enables simple logging, error reporting and health checkups without plug-ins.
    

🌟 Oban Pro
-----------

An official set of extensions, plugins, and workers that expand what Oban is capable of is available as a licensed package. It includes features like:

-   **Smart Engine** — Enables global concurrency, global rate limiting, queue partitioning, and auto insert batching for truly distributed job processing.
    
-   **Pro Worker** — Extends workers with execution hooks, structured args, output recording, encrypted args at rest, and chained execution.
    
-   **Workflows** — Compose jobs with arbitrary dependencies for sequential, fan-out, and fan-in execution patterns.
    
-   **Batches** — Process related jobs while tracking overall progress across all nodes and executing optional callbacks.
    
-   **Dynamic Plugins** — Runtime configuration of cron schedules, queues, job priorities, and automatic scaling—ideal for applications that manage jobs dynamically.
    
-   **Decorator** — Build and insert jobs directly from regular functions without defining worker modules.
    

Learn more about Oban Pro →

Engines
-------

Oban ships with engines for PostgreSQL, MySQL, and SQLite3. Each engine supports the same core functionality, though they have differing levels of maturity and suitability for production.

Requirements
------------

Oban requires:

-   Elixir 1.15+
-   Erlang 24+
-   PostgreSQL 12.0+, MySQL 8.4+, or SQLite3 3.37.0+

Installation
------------

See the installation guide for details on installing and configuring Oban in your application.

Quick Getting Started
---------------------

1.  Configure queues and an Ecto repo for Oban to use:
    
    \# In config/config.exs
    config :my\_app, Oban,
      repo: MyApp.Repo,
      queues: \[mailers: 20\]
    
2.  Define a worker to process jobs in the `mailers` queue (see `Oban.Worker`):
    
    defmodule MyApp.MailerWorker do
      use Oban.Worker, queue: :mailers
    
      @impl Oban.Worker
      def perform(%Oban.Job{args: %{"email" \=> email} \= \_args}) do
        \_ \= Email.deliver(email)
        :ok
      end
    end
    
3.  Enqueue a job (see the documentation):
    
    %{email: %{to: "foo@example.com", body: "Hello from Oban!"}}
    |> MyApp.MailerWorker.new()
    |> Oban.insert()
    
4.  The magic happens! Oban executes the job when there is available bandwidth in the `mailer` queue.
    

Learning
--------

Learn the fundamentals of Oban, all the way through to preparing for production with our LiveBook powered Oban Training curriculum.

Community
---------

There are a few places to connect and communicate with other Oban users:

-   Ask questions and discuss _#oban_ on the Elixir Forum
-   Request an invitation and join the _#oban_ channel on Slack
-   Learn about bug reports and upcoming features in the issue tracker

Contributing
------------

To run the Oban test suite you must have PostgreSQL 12+ and MySQL 8+ running. Follow these steps to create the database, create the database and run all migrations:

mix test.setup

To ensure a commit passes CI you should run `mix test.ci` locally, which executes the following commands:

-   Check formatting (`mix format --check-formatted`)
-   Check deps (`mix deps.unlock --check-unused`)
-   Lint with Credo (`mix credo --strict`)
-   Run all tests (`mix test --raise`)
-   Run Dialyzer (`mix dialyzer`)
