---
project: browser-use
stars: 114383
description: Agents that use the browser.
url: https://github.com/browser-use/browser-use
---

* * *

  

  

Navigate the web like a human does.
===================================

Find an available slot, pick a date and time, handle the CAPTCHA, and book a driving test.

Explore more demos and prompts ↗

  

Which Browser Use do I need?
============================

-   **Path 1: Fully Hosted Cloud:** Scale up with a fully hosted agent and browser.
-   **Path 2: CLI:** Automate your own browser tasks.
-   **Path 3: Python Library:** Run the open source Browser Use agent locally from your own code.

Quickstart
==========

Path 1: Fully Hosted Cloud
--------------------------

Scale browser automation with our hosted agent, stealth browsers, and infrastructure for profiles, recordings, and data policies.

Get started with the API ↗

New Google, GitHub, or Microsoft signups get **$15 cloud credit**.

  

Path 2: CLI
-----------

Paste this prompt into Claude Code, Codex, Hermes, OpenClaw, or your favorite agent.

```
Install or upgrade browser-use to the latest stable version with uv using Python 3.12, run `browser-use skill install` to register the skill, and connect it to my browser. If setup or connection fails, follow https://github.com/browser-use/browser-harness/blob/main/install.md.
```

  

Path 3: Python Library
----------------------

Run the Browser Use agent locally from Python, with your choice of model and a local or cloud browser:

**1\. Install Browser Use (Python >= 3.11):**

With uv installed, run `uv init --python 3.12` first if you're starting a new project.

uv add browser-use

**2\. Add your OpenAI API key to `.env`:**

# .env
OPENAI\_API\_KEY=your-key
# BROWSER\_USE\_API\_KEY=your-key  # Optional: BU2 model or cloud browser

For either optional Browser Use service, get a Browser Use API key.

**3\. Save this as `agent.py`:**

import asyncio

from browser\_use import Agent, Browser, ChatBrowserUse, ChatOpenAI
from dotenv import load\_dotenv

load\_dotenv()

async def main():
    llm \= ChatOpenAI(model\='gpt-5.6-luna', reasoning\_effort\='xhigh')
    \# llm = ChatBrowserUse(model='bu-2-0')  # Use BU2 instead; requires BROWSER\_USE\_API\_KEY
    agent \= Agent(
        task\="Find the number of stars of the browser-use repo",
        llm\=llm,
        \# browser=Browser(use\_cloud=True),  # Use a cloud browser; requires BROWSER\_USE\_API\_KEY
    )
    history \= await agent.run()
    print(history.final\_result())

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

To use BU2, replace the `ChatOpenAI` line with the commented `ChatBrowserUse` line. The cloud-browser option works with either model.

**4\. Run it:**

uv run agent.py

The agent opens a browser, looks up the repository, and prints its answer.

Python library docs ↗

  

Browser Use Benchmark v2
========================

This very hard benchmark targets the hardest browser tasks. On easier tasks, even smaller models can achieve very high success rates. Results shown are from a 60-task subset of BU Bench V2.

Integrations, hosting, custom tools, MCP, and more on our Docs ↗
----------------------------------------------------------------

  

FAQ
===

**Should I use the fully hosted cloud, CLI, or Python library?**

-   **Fully Hosted Cloud:** Send tasks through the API and let Browser Use run the agent, browser, and infrastructure.
-   **CLI:** Give an existing agent (Claude Code, Codex, Hermes, OpenClaw, Pi, Cursor, etc.) browser access. You can use it interactively or in scripts.
-   **Python Library:** Run the open source agent in your own application, with custom tools, structured output, and your choice of model.

The CLI and Python library can each connect to a local or cloud browser. A cloud browser hosts the browser; the fully hosted API runs the agent as well.

**What's the best model to use?**

We recommend **BU2**, our model optimized for browser automation: `ChatBrowserUse(model='bu-2-0')`. It uses `BROWSER_USE_API_KEY`; `ChatBrowserUse()` currently selects the same model.

The best choice depends on your tasks, latency, and budget. See the BU2 model card, benchmark, and supported models and pricing to compare options.

**Can I use Claude / GPT / Gemini through ChatBrowserUse?**

Yes. `ChatBrowserUse` accepts provider-prefixed model IDs through the Browser Use gateway, using `BROWSER_USE_API_KEY`:

from browser\_use import Agent, ChatBrowserUse

llm \= ChatBrowserUse(model\='anthropic/claude-sonnet-4-6')  \# or 'google/gemini-3-pro'
agent \= Agent(task\='...', llm\=llm)

You can also use providers directly through wrappers such as `ChatOpenAI`, `ChatAnthropic`, and `ChatGoogle`, with each provider's own API key. See supported models.

**Do I need to provide a system prompt?**

No. `Agent(...)` supplies the Browser Use system prompt automatically, including when you change models. Put your task in `task=`. Use `extend_system_message` to add instructions or `override_system_message` to replace the default prompt when you need custom behavior.

See the custom system prompt example.

**Can I use custom tools with the agent?**

Yes. Register a function with `Tools` and pass it to the agent. This example adds a tool for the current UTC time and uses `BROWSER_USE_API_KEY` from `.env`:

import asyncio
from datetime import datetime, timezone

from browser\_use import ActionResult, Agent, ChatBrowserUse, Tools
from dotenv import load\_dotenv

load\_dotenv()
tools \= Tools()

@tools.action(description\='Get the current date and time in UTC.')
def get\_current\_time() \-> ActionResult:
    return ActionResult(extracted\_content\=datetime.now(timezone.utc).isoformat())

async def main():
    agent \= Agent(
        task\="What is the current UTC time?",
        llm\=ChatBrowserUse(model\='bu-2-0'),
        tools\=tools,
    )
    history \= await agent.run()
    print(history.final\_result())

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

**Can I use this for free?**

The Python library is free and MIT-licensed. Model inference and hosted browsers are separate: API providers, including `ChatBrowserUse`, and Browser Use Cloud charge for usage. You can also use a local browser and a local model through Ollama, subject to your hardware and model requirements.

**Terms of Service**

This open-source library is licensed under the MIT License. For Browser Use services & data policy, see our Terms of Service and Privacy Policy.

**How do I handle authentication?**

-   **Local browser:** Use `Browser.from_system_chrome()` to reuse a Chrome profile. See the real-browser guide and example.
-   **Cloud browser:** Follow the profile sync guide, then use `Browser(use_cloud=True, cloud_profile_id='your-profile-id')`.

Profile sync transfers cookies, not local storage, IndexedDB, or extensions. Some sites may require you to sign in again.

**How do I solve CAPTCHAs?**

Browser Use Cloud provides stealth browsers and proxies designed to reduce bot detection and CAPTCHA challenges. With the Python library, enable a cloud browser with `Browser(use_cloud=True)` and set `BROWSER_USE_API_KEY`.

Results depend on the site and challenge; no browser configuration guarantees that every CAPTCHA can be avoided or solved.

**How do I go into production?**

Choose how much you want to manage:

-   **Keep your agent code:** Connect the CLI or Python library to cloud browsers for managed browser infrastructure, stealth, profiles, and recordings.
-   **Have us run the agent too:** Use the fully hosted Cloud API to submit tasks and retrieve results.

You can also host the Python library and browsers on your own infrastructure.

  

Related Repositories
--------------------

Repository

What it's for

Browser Harness

Our CLI for giving AI agents control of your browser.

Browser Harness JS

Give your JavaScript agent control of a real browser.

Browser Use Pi

Run a TypeScript browser agent built on Pi.

Cloud SDK

Integrate Browser Use Cloud into your application.

Video Use

Edit videos with your coding agent.

macOS Harness

Give your agent control of Mac apps, browsers, and files.

Benchmark

Explore browser tasks and compare agent performance.

  

Citation
--------

If you use Browser Use in your research or project, please cite:

@software{browser\_use2024,
  author = {Müller, Magnus and Žunič, Gregor},
  title = {Browser Use: Enable AI to control your browser},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/browser-use/browser-use}
}

  

**Tell your computer what to do, and it gets it done.**

   

Made with ❤️ in Zurich and San Francisco
