---
project: spec-kit
stars: 122115
description: 💫 Toolkit to help you get started with Spec-Driven Development
url: https://github.com/github/spec-kit
---

🌱 Spec Kit
===========

### _Define what to build before building it — with any AI coding agent._

**An open source toolkit for building high-quality software with any AI coding agent — a ready-to-use spec-driven process (or bring your own), endlessly extensible, community-driven, and built for your whole organization.**

* * *

Table of Contents
-----------------

-   🤔 What is Spec-Driven Development?
-   ⚡ Get Started
-   📽️ Video Overview
-   🌍 Community
-   🤖 Supported AI Coding Agent Integrations
-   🔧 Specify CLI Reference
-   🧩 Making Spec Kit Your Own: Extensions & Presets
-   📦 Bundles: Role-Based Setups
-   📚 Core Philosophy
-   🌟 Development Phases
-   🎯 Experimental Goals
-   🔧 Prerequisites
-   📖 Learn More
-   💬 Support
-   🙏 Acknowledgements
-   📄 License

🤔 What is Spec-Driven Development?
-----------------------------------

Spec-Driven Development **flips the script** on traditional software development. For decades, code has been king — specifications were just scaffolding we built and discarded once the "real work" of coding began. Spec-Driven Development changes this: **specifications become executable**, directly generating working implementations rather than just guiding them.

⚡ Get Started
-------------

### 1\. Install Specify CLI

Requires **uv** (install uv). Replace `vX.Y.Z` with the latest release tag from Releases — keep the leading `v` (for example, `v0.12.11`, not `0.12.11`):

uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z

Prefer installing from PyPI? The `specify-cli` package is also published there:

uv tool install specify-cli

See the Installation Guide for alternative methods, verification, upgrade, and troubleshooting.

### 2\. Initialize a project

specify init my-project --integration copilot
cd my-project

To check for updates or upgrade the installed CLI, use the self-management commands. See the Upgrade Guide for detailed scenarios and customization options.

# Check whether a newer release is available (read-only — does not modify anything)
specify self check

# Preview what would run, without actually upgrading
specify self upgrade --dry-run

# Upgrade in place to the latest stable release (auto-detects uv tool vs pipx install)
specify self upgrade

# Or pin a specific release tag (replace vX.Y.Z\[suffix\] with your desired release tag)
specify self upgrade --tag vX.Y.Z\[suffix\]

Bare `specify self upgrade` executes immediately, matching the no-prompt behavior of commands like `pip install -U` and `npm update`. For `uv tool` installs, it runs `uv tool install specify-cli --force --from <git ref>` under the hood so pinned release tags work, including dev, alpha/beta/rc, or build metadata suffixes. `uvx` (ephemeral) runs and source checkouts are detected and produce path-specific guidance instead of running an installer. Set `SPECIFY_UPGRADE_TIMEOUT_SECS` to cap how long the installer subprocess may run (default: no timeout — interrupt with `Ctrl+C` if needed).

### 3\. Establish project principles

Launch your coding agent in the project directory. Most agents expose spec-kit as `/speckit.*` slash commands; Codex CLI in skills mode uses `$speckit-*` instead; GitHub Copilot CLI uses `/agents` to select the agent or address it directly in a prompt.

Use the **`/speckit.constitution`** command to create your project's governing principles and development guidelines that will guide all subsequent development.

/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements

### 4\. Create the spec

Use the **`/speckit.specify`** command to describe what you want to build. Focus on the **what** and **why**, not the tech stack.

/speckit.specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.

### 5\. Create a technical implementation plan

Use the **`/speckit.plan`** command to provide your tech stack and architecture choices.

/speckit.plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.

### 6\. Break down into tasks

Use **`/speckit.tasks`** to create an actionable task list from your implementation plan.

/speckit.tasks

### 7\. Execute implementation

Use **`/speckit.implement`** to execute all tasks and build your feature according to the plan.

/speckit.implement

For detailed step-by-step instructions, see our comprehensive guide.

📽️ Video Overview
------------------

Want to see Spec Kit in action? Watch our video overview!

🌍 Community
------------

Explore community-contributed resources on the Spec Kit docs site:

-   Extensions — commands, hooks, and capabilities
-   Presets — template and terminology overrides
-   Bundles — role and team stacks composed from existing components
-   Walkthroughs — end-to-end SDD scenarios
-   Friends — projects that extend or build on Spec Kit

Note

Community contributions are independently created and maintained by their respective authors. Review source code before installation and use at your own discretion.

Want to contribute? See the Extension Publishing Guide, the Presets Publishing Guide, or the Community Bundles guide.

🤖 Supported AI Coding Agent Integrations
-----------------------------------------

Spec Kit works with 30+ AI coding agents — both CLI tools and IDE-based assistants. See the full list with notes and usage details in the Supported AI Coding Agent Integrations guide.

Run `specify integration list` to see all available integrations in your installed version.

Available Slash Commands
------------------------

After running `specify init`, your AI coding agent will have access to these slash commands for structured development. For integrations that support skills mode, passing `--integration <agent> --integration-options="--skills"` installs agent skills instead of slash-command prompt files.

### Core Commands

Essential commands for the Spec-Driven Development workflow:

Command

Agent Skill

Description

`/speckit.constitution`

`speckit-constitution`

Create or update project governing principles and development guidelines

`/speckit.specify`

`speckit-specify`

Define what you want to build (requirements and user stories)

`/speckit.plan`

`speckit-plan`

Create technical implementation plans with your chosen tech stack

`/speckit.tasks`

`speckit-tasks`

Generate actionable task lists for implementation

`/speckit.taskstoissues`

`speckit-taskstoissues`

Convert generated task lists into GitHub issues for tracking and execution

`/speckit.implement`

`speckit-implement`

Execute all tasks to build the feature according to the plan

`/speckit.converge`

`speckit-converge`

Assess the codebase against spec/plan/tasks and append remaining work as new tasks

### Optional Commands

Additional commands for enhanced quality and validation:

Command

Agent Skill

Description

`/speckit.clarify`

`speckit-clarify`

Clarify underspecified areas (recommended before `/speckit.plan`; formerly `/quizme`)

`/speckit.analyze`

`speckit-analyze`

Cross-artifact consistency & coverage analysis (run after `/speckit.tasks`, before `/speckit.implement`)

`/speckit.checklist`

`speckit-checklist`

Generate custom quality checklists that validate requirements completeness, clarity, and consistency (like "unit tests for English")

🔧 Specify CLI Reference
------------------------

For full command details, options, and examples, see the CLI Reference.

🧩 Making Spec Kit Your Own: Extensions & Presets
-------------------------------------------------

Spec Kit can be tailored to your needs through two complementary systems — **extensions** and **presets** — plus project-local overrides for one-off adjustments:

Priority

Component Type

Location

⬆ 1

Project-Local Overrides

`.specify/templates/overrides/`

2

Presets — Customize core & extensions

`.specify/presets/templates/`

3

Extensions — Add new capabilities

`.specify/extensions/templates/`

⬇ 4

Spec Kit Core — Built-in SDD commands & templates

`.specify/templates/`

-   **Templates** are resolved at **runtime** — Spec Kit walks the stack top-down and uses the first match.
-   Project-local overrides (`.specify/templates/overrides/`) let you make one-off adjustments for a single project without creating a full preset.
-   **Extension/preset commands** are applied at **install time** — when you run `specify extension add` or `specify preset add`, command files are written into agent directories (e.g., `.claude/commands/`).
-   If multiple presets or extensions provide the same command, the highest-priority version wins. On removal, the next-highest-priority version is restored automatically.
-   If no overrides or customizations exist, Spec Kit uses its core defaults.

### Extensions — Add New Capabilities

Use **extensions** when you need functionality that goes beyond Spec Kit's core. Extensions introduce new commands and templates — for example, adding domain-specific workflows that are not covered by the built-in SDD commands, integrating with external tools, or adding entirely new development phases. They expand _what Spec Kit can do_.

# Search available extensions
specify extension search

# Install an extension
specify extension add <extension-name\>

For example, extensions could add Jira integration, post-implementation code review, V-Model test traceability, or project health diagnostics.

See the Extensions reference for the full command guide. Browse the community extensions for what's available.

### Presets — Customize Existing Workflows

Use **presets** when you want to change _how_ Spec Kit works without adding new capabilities. Presets override the templates and commands that ship with the core _and_ with installed extensions — for example, enforcing a compliance-oriented spec format, using domain-specific terminology, or applying organizational standards to plans and tasks. They customize the artifacts and instructions that Spec Kit and its extensions produce.

# Search available presets
specify preset search

# Install a preset
specify preset add <preset-name\>

For example, presets could restructure spec templates to require regulatory traceability, adapt the workflow to fit the methodology you use (e.g., Agile, Kanban, Waterfall, jobs-to-be-done, or domain-driven design), add mandatory security review gates to plans, enforce test-first task ordering, or localize the entire workflow to a different language. The pirate-speak demo shows just how deep the customization can go. Multiple presets can be stacked with priority ordering.

See the Presets reference for the full command guide, including resolution order and priority stacking.

📦 Bundles: Role-Based Setups
-----------------------------

Extensions and presets are individual building blocks. A **bundle** packages a curated set of them — extensions, presets, steps, and workflows — into a single, versioned, role-oriented setup so a whole team persona (product manager, business analyst, security researcher, developer, …) can be provisioned with one command.

A bundle is described by a hand-written `bundle.yml` manifest. It pins each component to a version and, optionally, targets a specific integration; a bundle with no `integration` is **agnostic** and inherits whatever integration the project already uses.

# Discover bundles in the active catalog stack
specify bundle search \[<query\>\]

# Inspect the exact component set a bundle will add (equals what install does)
specify bundle info <bundle-id\>

# Install a bundle's full component set in one operation
specify bundle install <bundle-id\>

# See what's installed, then update or remove non-destructively
specify bundle list
specify bundle update <bundle-id\>     # or --all
specify bundle remove <bundle-id\>     # removes only this bundle's components

Bundles resolve from a **priority-ordered catalog stack** (project > user > built-in). Each source carries an install policy: `install-allowed` sources can be installed from, while `discovery-only` sources are visible in `search`/`info` but refuse installation. Manage the stack with `specify bundle catalog list|add|remove`.

Authors validate and package bundles locally. Distribution is hosting the built artifact and adding a catalog source; community bundle submissions use the Bundle Submission issue template so required component catalogs and install evidence can be reviewed:

specify bundle validate --path ./my-bundle      # structural + reference checks
specify bundle build --path ./my-bundle         # produce a versioned .zip artifact

Four ready-to-read example manifests live under `examples/bundles/` (product manager, business analyst, security researcher, developer).

Key guarantees: `info` shows exactly what `install` adds (transparency); installs are idempotent and confined to the project root; `remove` never touches components another installed bundle still needs; and all consume/author commands work **offline** against local or pinned sources.

### When to Use Which

Goal

Use

Add a brand-new command or workflow

Extension

Customize the format of specs, plans, or tasks

Preset

Integrate an external tool or service

Extension

Enforce organizational or regulatory standards

Preset

Ship reusable domain-specific templates

Either — presets for template overrides, extensions for templates bundled with new commands

Provision a complete role-based setup in one command

Bundle

📚 Core Philosophy
------------------

Spec-Driven Development is a structured process that emphasizes:

-   **Intent-driven development** where specifications define the "_what_" before the "_how_"
-   **Rich specification creation** using guardrails and organizational principles
-   **Multi-step refinement** rather than one-shot code generation from prompts
-   **Heavy reliance** on advanced AI model capabilities for specification interpretation

🌟 Development Phases
---------------------

Phase

Focus

Key Activities

**0-to-1 Development** ("Greenfield")

Generate from scratch

-   Start with high-level requirements
-   Generate specifications
-   Plan implementation steps
-   Build production-ready applications

**Creative Exploration**

Parallel implementations

-   Explore diverse solutions
-   Support multiple technology stacks & architectures
-   Experiment with UX patterns

**Iterative Enhancement** ("Brownfield")

Brownfield modernization

-   Add features iteratively
-   Modernize legacy systems
-   Adapt processes

For existing projects, keep Spec Kit tooling updates separate from feature artifact evolution: refresh managed project files when upgrading, and update `specs/` artifacts when intended behavior changes. The Evolving Specs guide describes the recommended brownfield loop.

🎯 Experimental Goals
---------------------

Our research and experimentation focus on:

### Technology independence

-   Create applications using diverse technology stacks
-   Validate the hypothesis that Spec-Driven Development is a process not tied to specific technologies, programming languages, or frameworks

### Enterprise constraints

-   Demonstrate mission-critical application development
-   Incorporate organizational constraints (cloud providers, tech stacks, engineering practices)
-   Support enterprise design systems and compliance requirements

### User-centric development

-   Build applications for different user cohorts and preferences
-   Support various development approaches (from vibe-coding to AI-native development)

### Creative & iterative processes

-   Validate the concept of parallel implementation exploration
-   Provide robust iterative feature development workflows
-   Extend processes to handle upgrades and modernization tasks

🔧 Prerequisites
----------------

-   **Linux/macOS/Windows**
-   Supported AI coding agent.
-   uv for package management (recommended) or pipx for persistent installation
-   Python 3.11+
-   Git

If you encounter issues with an agent, please open an issue so we can refine the integration.

📖 Learn More
-------------

-   **Complete Spec-Driven Development Methodology** - Deep dive into the full process
-   **Quick Start Guide** - Step-by-step implementation walkthrough

* * *

💬 Support
----------

For support, please open a GitHub issue. We welcome bug reports, feature requests, and questions about using Spec-Driven Development.

🙏 Acknowledgements
-------------------

This project is heavily influenced by and based on the work and research of John Lam.

📄 License
----------

This project is licensed under the terms of the MIT open source license. Please refer to the LICENSE file for the full terms.
