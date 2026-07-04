---
project: browser-use
stars: 102714
description: 🌐 Make websites accessible for AI agents. Automate tasks online with ease.
url: https://github.com/browser-use/browser-use
---

* * *

  

**Browser Use CLI 3.0 is here.** Give your coding agent a browser it can use reliably.

Paste this into Claude Code, Codex, etc:

```
Install or upgrade browser-use to the latest stable version with uv using Python 3.12, register the skill from `browser-use skill`, and connect it to my browser. Follow https://github.com/browser-use/browser-use if setup or connection fails.
```

🌤️ Want to skip the setup? Use our **cloud** for faster, scalable, stealth-enabled browser automation!

🤖 LLM Quickstart
=================

1.  Direct your favorite coding agent (Cursor, Claude Code, etc) to Agents.md
2.  Prompt away!

  

👋 Human Quickstart
===================

**1\. Install Browser Use (Python>=3.11):**

uv add browser-use
# or: pip install browser-use

**2\. \[Optional\] Get your API key from Browser Use Cloud:**

```
# .env
BROWSER_USE_API_KEY=your-key
# GOOGLE_API_KEY=your-key
# ANTHROPIC_API_KEY=your-key
```

**3\. Run your first agent:**

**Python Script:**

import asyncio

from browser\_use import Agent, BrowserProfile, ChatBrowserUse

async def main():
    agent \= Agent(
        task\="Find the number of stars of the browser-use repo",
        llm\=ChatBrowserUse(model\='openai/gpt-5.5'),
        \# llm=ChatBrowserUse(model='bu-2-0'),  # Browser Use's own optimized model
        \# llm=ChatOpenAI(model='gpt-5.5'),
        \# llm=ChatAnthropic(model='claude-opus-4-8'),  # Sonnet also works well.
        browser\_profile\=BrowserProfile(
            headless\=False,
            allowed\_domains\=\["\*.github.com"\],
        ),
    )
    history \= await agent.run()
    print(history.final\_result())

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

Check out the library docs and the cloud docs for more!

  

Open Source vs Cloud
====================

We benchmark Browser Use across 100 real-world browser tasks. Full benchmark is open source: **browser-use/benchmark**.

**Use the Open-Source Agent**

-   You need custom tools or deep code-level integration
-   We recommend pairing with our cloud browsers for leading stealth, proxy rotation, and scaling
-   Or self-host the open-source agent fully on your own machines

**Use the Fully-Hosted Cloud Agent (recommended)**

-   Much more powerful agent for complex tasks (see plot above)
-   Easiest way to start and scale
-   Best stealth with proxy rotation and captcha solving
-   1000+ integrations (Gmail, Slack, Notion, and more)
-   Persistent filesystem and memory

  

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

**Browser Use CLI 3.0** lets your agents do work for you online with our highest accuracy yet. It is powered by Browser Harness, and it applies what we learned about agent harnesses and agent frameworks: the latest models do best when you give them freedom, rather than abstracting away complexity. We provide your agents with a direct, dependable surface for acting in the browser.

browser-use <<'PY'
new\_tab("https://example.com")
print(page\_info())
PY

The CLI allows your agent to control the browser via Python, and it manages the browser in the background.

### Agent Skill

For Claude Code, Codex, and other agents, paste this prompt into your agent:

```
Install or upgrade browser-use to the latest stable version with uv using Python 3.12, register the skill from `browser-use skill`, and connect it to my browser. Follow https://github.com/browser-use/browser-use if setup or connection fails.
```

  

Integrations, hosting, custom tools, MCP, and more on our Docs ↗
----------------------------------------------------------------

  

FAQ
===

**What's the best model to use?**

We optimized **ChatBrowserUse()** specifically for browser automation tasks. On avg it completes tasks 3-5x faster than other models with SOTA accuracy.

For pricing and other LLM providers, see our supported models documentation.

**Can I use Claude / GPT / Gemini through ChatBrowserUse?**

Yes. `ChatBrowserUse` accepts provider-prefixed model ids, so a single `BROWSER_USE_API_KEY` reaches all of them — no separate OpenAI/Anthropic/Google keys required:

from browser\_use import Agent, ChatBrowserUse

llm \= ChatBrowserUse(model\='anthropic/claude-sonnet-4-6')  \# or 'openai/gpt-5.5', 'google/gemini-3-pro'
agent \= Agent(task\='...', llm\=llm)

For the best speed and cost we still recommend the default `bu-*` models.

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
