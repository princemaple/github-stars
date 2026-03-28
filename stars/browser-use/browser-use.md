---
project: browser-use
stars: 84848
description: 🌐 Make websites accessible for AI agents. Automate tasks online with ease.
url: https://github.com/browser-use/browser-use
---

* * *

  

🌤️ Want to skip the setup? Use our **cloud** for faster, scalable, stealth-enabled browser automation!

🤖 LLM Quickstart
=================

1.  Direct your favorite coding agent (Cursor, Claude Code, etc) to Agents.md
2.  Prompt away!

  

👋 Human Quickstart
===================

**1\. Create environment and install Browser-Use with uv (Python>=3.11):**

uv init && uv add browser-use && uv sync
# uvx browser-use install  # Run if you don't have Chromium installed

**2\. \[Optional\] Get your API key from Browser Use Cloud:**

```
# .env
BROWSER_USE_API_KEY=your-key
# GOOGLE_API_KEY=your-key
# ANTHROPIC_API_KEY=your-key
```

**3\. Run your first agent:**

from browser\_use import Agent, Browser, ChatBrowserUse
\# from browser\_use import ChatGoogle  # ChatGoogle(model='gemini-3-flash-preview')
\# from browser\_use import ChatAnthropic  # ChatAnthropic(model='claude-sonnet-4-6')
import asyncio

async def main():
    browser \= Browser(
        \# use\_cloud=True,  # Use a stealth browser on Browser Use Cloud
    )

    agent \= Agent(
        task\="Find the number of stars of the browser-use repo",
        llm\=ChatBrowserUse(),
        \# llm=ChatGoogle(model='gemini-3-flash-preview'),
        \# llm=ChatAnthropic(model='claude-sonnet-4-6'),
        browser\=browser,
    )
    await agent.run()

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

Check out the library docs and the cloud docs for more!

  

Open Source vs Cloud
====================

We benchmark Browser Use across 100 real-world browser tasks. Full benchmark is open source: **browser-use/benchmark**.

**Use Open Source**

-   You need custom tools or deep code-level integration
-   You want to self-host and deploy browser agents on your own machines

**Use Cloud (recommended)**

-   Much better agent for complex tasks (see plot above)
-   Easiest way to start and scale
-   Best stealth with proxy rotation and captcha solving
-   1000+ integrations (Gmail, Slack, Notion, and more)
-   Persistent filesystem and memory

**Use Both**

-   Use the open-source library with your custom tools while running our cloud browsers and ChatBrowserUse model

  

Demos
=====

### 📋 Form-Filling

#### Task = "Fill in this job application with my resume and information."

Example code ↗

### 🍎 Grocery-Shopping

#### Task = "Put this list of items into my instacart."

grocery-use-large.mp4

Example code ↗

### 💻 Personal-Assistant.

#### Task = "Help me find parts for a custom PC."

pc-use-large.mp4

Example code ↗

### 💡See more examples here ↗ and give us a star!

  

🚀 Template Quickstart
======================

**Want to get started even faster?** Generate a ready-to-run template:

uvx browser-use init --template default

This creates a `browser_use_default.py` file with a working example. Available templates:

-   `default` - Minimal setup to get started quickly
-   `advanced` - All configuration options with detailed comments
-   `tools` - Examples of custom tools and extending the agent

You can also specify a custom output path:

uvx browser-use init --template default --output my\_agent.py

  

💻 CLI
======

Fast, persistent browser automation from the command line:

browser-use open https://example.com    # Navigate to URL
browser-use state                       # See clickable elements
browser-use click 5                     # Click element by index
browser-use type "Hello"                # Type text
browser-use screenshot page.png         # Take screenshot
browser-use close                       # Close browser

The CLI keeps the browser running between commands for fast iteration. See CLI docs for all commands.

### Claude Code Skill

For Claude Code, install the skill to enable AI-assisted browser automation:

mkdir -p ~/.claude/skills/browser-use
curl -o ~/.claude/skills/browser-use/SKILL.md \\
  https://raw.githubusercontent.com/browser-use/browser-use/main/skills/browser-use/SKILL.md

  

Integrations, hosting, custom tools, MCP, and more on our Docs ↗
----------------------------------------------------------------

  

FAQ
===

**What's the best model to use?**

We optimized **ChatBrowserUse()** specifically for browser automation tasks. On avg it completes tasks 3-5x faster than other models with SOTA accuracy.

**Pricing (per 1M tokens):**

-   Input tokens: $0.20
-   Cached input tokens: $0.02
-   Output tokens: $2.00

For other LLM providers, see our supported models documentation.

**Should I use the Browser Use system prompt with the open-source preview model?**

Yes. If you use `ChatBrowserUse(model='browser-use/bu-30b-a3b-preview')` with a normal `Agent(...)`, Browser Use still sends its default agent system prompt for you.

You do **not** need to add a separate custom "Browser Use system message" just because you switched to the open-source preview model. Only use `extend_system_message` or `override_system_message` when you intentionally want to customize the default behavior for your task.

If you want the best default speed/accuracy, we still recommend the newer hosted `bu-*` models. If you want the open-source preview model, the setup stays the same apart from the `model=` value.

**Can I use custom tools with the agent?**

Yes! You can add custom tools to extend the agent's capabilities:

from browser\_use import Tools

tools \= Tools()

@tools.action(description\='Description of what this tool does.')
def custom\_tool(param: str) \-> str:
    return f"Result: {param}"

agent \= Agent(
    task\="Your task",
    llm\=llm,
    browser\=browser,
    tools\=tools,
)

**Can I use this for free?**

Yes! Browser-Use is open source and free to use. You only need to choose an LLM provider (like OpenAI, Google, ChatBrowserUse, or run local models with Ollama).

**Terms of Service**

This open-source library is licensed under the MIT License. For Browser Use services & data policy, see our Terms of Service and Privacy Policy.

**How do I handle authentication?**

Check out our authentication examples:

-   Using real browser profiles - Reuse your existing Chrome profile with saved logins
-   If you want to use temporary accounts with inbox, choose AgentMail
-   To sync your auth profile with the remote browser, run `curl -fsSL https://browser-use.com/profile.sh | BROWSER_USE_API_KEY=XXXX sh` (replace XXXX with your API key)

These examples show how to maintain sessions and handle authentication seamlessly.

**How do I solve CAPTCHAs?**

For CAPTCHA handling, you need better browser fingerprinting and proxies. Use Browser Use Cloud which provides stealth browsers designed to avoid detection and CAPTCHA challenges.

**How do I go into production?**

Chrome can consume a lot of memory, and running many agents in parallel can be tricky to manage.

For production use cases, use our Browser Use Cloud API which handles:

-   Scalable browser infrastructure
-   Memory management
-   Proxy rotation
-   Stealth browser fingerprinting
-   High-performance parallel execution

  

**Tell your computer what to do, and it gets it done.**

   

Made with ❤️ in Zurich and San Francisco
