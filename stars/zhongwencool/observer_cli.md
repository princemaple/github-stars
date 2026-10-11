---
project: observer_cli
stars: 1536
description: Visualize Erlang/Elixir Nodes On The Command Line
url: https://github.com/zhongwencool/observer_cli
---

observer\_cli
=============

**Bounded BEAM investigations for people and agents.** Start with a question, inspect the evidence, and choose the next smallest observation. Text is concise; JSON preserves measurements and coverage.

> This checkout implements unreleased **2.1.0**, a breaking redesign. Keep a versioned 2.0 binary until you migrate.

Start here
----------

Prepare a distributed target with the matching **2.1.0 bundle, protocol 2**. Have its cookie injected by a protected secret source; never paste the value into command arguments.

export OBSERVER\_CLI\_NODE='app@host'
# OBSERVER\_CLI\_COOKIE is supplied by your secret source.
observer\_cli check
observer\_cli check cpu --window 5s
observer\_cli inspect process --sort reductions-rate --window 5s
observer\_cli inspect process --pid '<0.123.0>'

A bare check observes for **15 seconds**, evaluates VM-limit and scheduler-pressure rules, and shows evidence and next steps. No findings does not prove node health. Reductions/s measures activity, not process CPU time. There is no saved connection or `connect`/`disconnect` step.

Entry

Purpose

`check [cpu|memory|mailbox|connections]`

Bounded overview or focused investigation.

`inspect RESOURCE`

Runtime facts, rankings, or process/port detail.

`trace call` / `trace stop`

Explicitly authorized node-global tracing.

`tui`

Continuous interaction with existing pages and plugins.

`describe [COMMAND PATH]`

Offline command discovery.

Use `observer_cli --help` for an overview or `describe inspect process --json` for precise machine-readable constraints. See the CLI reference for resources, target options, metric meanings and limits.

Build this checkout
-------------------

Controllers are escripts and require Erlang/OTP **26–29**. JSON requires controller OTP **27+**; OTP 26 supports text/term and rejects JSON before connecting.

rebar3 escriptize
./\_build/default/bin/observer\_cli --version

Alternatively, with OTP 29 / Elixir 1.20:

mix deps.get
mix escript.build
./observer\_cli --version

Include `observer_cli` and `recon` in the target release. Command diagnostics never upload missing code. These commands build locally; they do not publish a release.

Automation and safety
---------------------

Agents bind the target explicitly on **every** call:

observer\_cli check cpu --window 5s \\
  --node 'app@host' --cookie-env OBSERVER\_CLI\_COOKIE --json

Complete checks exit `0` even with findings; `--fail-on` opts into severity-based failure. Partial execution and cleanup failures take precedence. Follow typed selectors, not display text; suggestions never execute automatically.

An Erlang cookie grants trusted-peer execution authority, and distribution is not encrypted by default. Use trusted nodes and transport. Default checks do not read business contents, state, logs or traces. State and trace require specific consent; TUI code loading requires `--load-code` and the same OTP major.

Identifiers are included for follow-up. Use `--redact` for sharing metadata, but review the destination: counts and topology remain sensitive, and arbitrary logs cannot be reliably redacted. Use one active observation per target; per-request budgets do not limit aggregate concurrent load.

Further reading
---------------

-   Agent workflows: JSON-only investigation and sharing.
-   Core concepts: evidence, uncertainty and trust.
-   TUI reference and plugins.
-   Public JSON Schema.
