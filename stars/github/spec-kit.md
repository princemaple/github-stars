---
project: spec-kit
stars: 141678
description: 💫 Toolkit to help you get started with SDD or any other process!
url: https://github.com/github/spec-kit
---

🌱 Spec Kit
===========

### _Build with a spec, fix a bug, or assess an idea — with your coding agent._

**English** · 简体中文 · 日本語 · 한국어

Spec Kit is an open source toolkit that gives AI coding agents structured processes, reusable templates, and documented outcomes. Start with a ready-made process, customize it, or bring your own.

Choose your process
-------------------

What you need

Process

Outcome

Build a feature or application

Spec-Driven Development

A specification carried through planning, implementation, and convergence

Diagnose and repair broken behavior

Bug fixing

An assessed cause, scoped fix, and recorded verification

Decide whether an idea deserves investment

Idea assessment

An evidence-backed go, clarify, or stop decision

Adopt or create a different process

Your own process

A process adapted or assembled from reusable primitives

These are **independent entry points**, not mandatory phases. SDD ships in core; bug fixing and assessment are bundled extensions you install when needed, and the primitives below let you adopt or create other processes.

Capabilities
------------

Spec Kit combines ready-to-use processes with composable mechanisms:

Capability

Spec Kit mechanism

Connect to or switch between coding agents

Integration

Add a command, quality gate, or complete process

Extension

Connect a process to an external tool or service

Extension

React to coding-agent lifecycle events

Extension event hook

Adapt templates, commands, terminology, or methodology

Preset

Enforce organizational or regulatory standards

Preset

Override a template for one project

Project-local override

Automate prompts, commands, gates, and shell tasks

Workflow

Modify an installed workflow without forking it

Workflow overlay

Add reusable executable behavior to workflows

Workflow step

Install a curated setup for a role or team

Bundle

Discover community components

Catalog

Host a private catalog of approved components

Catalog

Access private catalogs and component downloads

Authentication

Work offline or behind a firewall

Local sources and self-hosted catalogs

Inspect which layer supplies a command, template, or script

Artifact inventory

Search the active catalogs with commands such as `specify extension search`, `specify preset search`, `specify workflow search`, and `specify bundle search`. Spec Kit includes community catalogs, and organizations can add their own curated sources. Catalog listings are not audits or endorsements, so review community source code before installing or running it.

Get started
-----------

You need **Python 3.11+**, **uv**, and a supported AI coding agent on Linux, macOS, or Windows. For **CLI setup only**, run this in your terminal to install Spec Kit and create a project:

uv tool install specify-cli
specify init my-project --integration copilot
cd my-project

The examples use **GitHub Copilot's default skills mode**. Replace `copilot` with your integration key to use another supported agent.

Already have code? Follow the existing-project guide. For pinned releases, other installers, CI, or troubleshooting, see Installation. To update an existing installation, see Upgrade.

Now **launch your coding agent in the project directory** and choose a process below. Invoke each `/speckit-*` **skill in your agent's chat**, one at a time, and review the result before continuing. These are agent skills, not terminal commands. Other agents and modes may use different invocation syntax.

Spec-Driven Development
-----------------------

Define **what and why** before deciding **how** to build it. SDD turns your requirements into a specification, a technical plan, and actionable tasks, then guides implementation against those artifacts.

**Constitution once per project; specify → plan → tasks → implement → converge per feature.**

Invoke these skills in your agent's chat:

```
/speckit-constitution Create principles focused on code quality, testing, and maintainability.
/speckit-specify Build a photo organizer with albums grouped by date and a tile preview of each album.
/speckit-plan Use Vite with vanilla JavaScript. Keep images local and store metadata in SQLite.
/speckit-tasks
/speckit-implement
/speckit-converge
```

Repeat **implement → converge** until convergence reports **Converged**. Add clarification, checklists, and consistency analysis when you need extra quality gates.

SDD walkthrough · Command reference

Bug fixing
----------

Keep diagnosis, repair, and verification separate so the agent fixes the assessed cause and checks the original symptom. No SDD feature workflow is required first.

**CLI setup (terminal):** install the opt-in extension from the project directory:

specify extension add bug

Then invoke the **assess → fix → test** skills in your agent's chat:

```
/speckit-bug-assess "Submitting an empty password crashes the login form." slug=login-crash
/speckit-bug-fix slug=login-crash
/speckit-bug-test slug=login-crash
```

The reports live in `.specify/bugs/login-crash/`. Review the final verdict: `verified`, `partial`, or `failed`. Missing verification is not a successful fix.

Bug-fixing walkthrough · Command reference

Idea assessment
---------------

Gather evidence before committing to an idea, whether or not it becomes software. This standalone process works even in a project with no source code.

**CLI setup (terminal):** install the opt-in extension from the project directory:

specify extension add assess

Then invoke the **intake → research → define → shape → decide** skills in your agent's chat:

```
/speckit-assess-intake "Let users work offline and sync when they reconnect." slug=offline-mode
/speckit-assess-research slug=offline-mode
/speckit-assess-define slug=offline-mode
/speckit-assess-shape slug=offline-mode
/speckit-assess-decide slug=offline-mode
```

The artifacts live in `.specify/assessments/offline-mode/`, ending in a **go / needs-clarification / kill** decision. Resolve unknowns by refining the existing Markdown artifacts directly or with the agent, rather than regenerating whole stages. A `go` decision can be handed to `/speckit-specify` if you choose to build it; stopping with a documented reason is also a useful result.

Assessment walkthrough · Command reference

Customize or bring your own process
-----------------------------------

**Extensions** add capabilities, **presets** adapt existing behavior, **workflows** automate steps, and **bundles** package a role-based setup. Use project-local overrides for one-off template changes.

Customization guide · Community extensions, presets, bundles, and walkthroughs

Documentation
-------------

-   CLI reference and process commands
-   SDD philosophy, full methodology, and evolving existing specs
-   Video overview and project history
-   How Spec Kit uses Spec Kit

Star history
------------

_Thanks to everyone who helps Spec Kit shine._

Support and contributing
------------------------

Report a bug or request a feature · Contributing guide · Code of conduct

Spec Kit is MIT licensed.
