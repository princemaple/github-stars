---
project: opensource.builders
stars: 1295
description: Find and build open-source alternatives
url: https://github.com/junaid33/opensource.builders
---

Opensource.Builders
===================

Find open-source alternatives to popular software, compare features side-by-side, and generate skills with code references that help AI build those features in your project.

Features
--------

-   **Browse Alternatives** - Discover open-source alternatives to proprietary applications
-   **Compare Applications** - See feature-by-feature comparisons between apps
-   **Skill Builder** - Generate AI coding agent skills from curated features with implementation details and code references
-   **Multi-Agent Support** - Install skills in Claude Code, Cursor, Droid, or Codex CLI

Skill Builder
-------------

The Skill Builder lets you select features from multiple open-source projects and generates a skill - a guide with specific code references that your AI coding agent can use to build those features in your project. Each skill includes:

-   Feature descriptions and implementation notes
-   Links to reference code in GitHub repositories
-   Documentation URLs for deeper context

### Installing Skills

After generating a skill, you can install it in your preferred AI coding agent:

**Claude Code**

# Save the skill file to your project
mkdir -p .claude/skills && cp ~/Downloads/SKILL.md .claude/skills/

**Cursor**

# Add the skill content to your rules file
cat ~/Downloads/SKILL.md \>> .cursor/rules/skill.mdc

**Droid**

# Save to your project's skills directory
mkdir -p .factory/skills && cp ~/Downloads/SKILL.md .factory/skills/

**Codex CLI**

# Add to your agents instructions
cat ~/Downloads/SKILL.md \>> codex.md

Getting Started
---------------

First, run the development server:

npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev

Open http://localhost:3000 with your browser to see the result.

Tech Stack
----------

-   Next.js - React framework
-   Keystone - Headless CMS
-   PostgreSQL - Database
-   Tailwind CSS - Styling

Contributing
------------

See CONTRIBUTING\_TO\_OSB.md for guidelines on adding applications, capabilities, and improving the platform.

Deploy
------

### Vercel

### Railway

License
-------

MIT
