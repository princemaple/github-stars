---
project: claude-code-router
stars: 35892
description: One local control plane for every AI agent: route across models, fuse new capabilities, orchestrate tools, and stay fully in control.
url: https://github.com/musistudio/claude-code-router
---

Claude Code Router
==================

  
**Kimi Code Subscription**  ·  **API Global**  ·  API China

**Thanks to Kimi for sponsoring this project!** Kimi K2.7 Code is an open-source, coding-focused agentic model developed by Moonshot AI, with substantial gains on real-world long-horizon coding tasks and higher end-to-end success across complex software engineering workflows. It also cuts thinking-token usage by approximately 30% compared with K2.6. Inside CCR, Kimi ships as built-in provider presets: import the pay-as-you-go API or the Kimi Code subscription in one click and route your coding agent's requests to Kimi, the subscription endpoint passes straight through natively with no protocol conversion, API endpoints are adapted automatically, and your balance and subscription usage show up right in the CCR dashboard.

CCR already supports Kimi. Visit the Kimi Open Platform (中文站 | Global) to try the API, or explore the cost-effective Coding Plan.

Claude Code Router Desktop is a local control plane for coding agents. It gives Claude Code, Codex, Grok CLI, ZCode, and compatible API clients one stable local endpoint, then lets you decide which provider, model, routing policy, tool stack, and account should handle each request.

Instead of wiring every agent to every model service by hand, CCR centralizes the model layer on your own machine: provider presets, custom endpoints, credential pools, fallback chains, Fusion-enhanced models, MCP tools, request logs, account usage, and desktop launch profiles all live in one app.

What CCR Helps You Do
---------------------

Goal

CCR gives you

Keep the same agent workflow while switching models

Local profiles for Claude Code, Codex, Grok CLI, and ZCode, with CLI/app launch entries and per-profile model selection

Try many providers without rebuilding config every time

Built-in provider presets, custom OpenAI/Anthropic/Gemini-compatible endpoints, protocol probing, model discovery, and connectivity checks

Make routing a runtime policy

Built-in agent routing, conditional rules, request rewrites, model-prefix routing, retries, and fallback model chains

Control cost and quota pressure

Credential pools, key rotation, local usage limits, account balance snapshots, token/cost dashboards, and tray status

Upgrade a model without replacing it

Fusion models that add vision, web search, or selected MCP tools to an existing base model

Keep large tool sets usable

ToolHub, a compact MCP entry point that lets agents resolve and invoke the tools needed for the current task

Debug what actually happened

Request logs, resolved provider/model fields, latency, token usage, estimated cost, network capture, and agent observability

Why Use CCR
-----------

-   **One gateway for your agent stack**: point clients at CCR once, then move routing, models, keys, and providers from scattered client configs into a single desktop UI.
-   **Provider freedom without workflow churn**: use OpenAI Chat/Responses, Anthropic Messages, Gemini Generate Content/Interactions, OpenRouter, DeepSeek, SiliconFlow, Moonshot, Kimi Code, Mistral, Z.AI, Bailian, and custom compatible providers.
-   **Reliability policies you can see and change**: define when a request should be rewritten, retried, or moved to another model, then verify the result in local logs.
-   **Operational visibility for AI work**: track requests, tokens, cost estimates, success rate, latency, model distribution, provider usage, and account balances from the dashboard or tray.
-   **Agent-native tools and extensions**: add Fusion capabilities, expose dynamic MCP tools through ToolHub, automate the built-in browser, relay agents through IM bots, or install local extensions.

Feature Highlights
------------------

-   **Agent profiles**: create profiles for Claude Code, Codex, Grok CLI, and ZCode with model overrides, scopes, CLI/app launch surfaces, environment settings, and multi-instance app workflows.
-   **Provider management**: add preset providers or custom endpoints; probe supported protocols; detect model lists; run real connectivity checks; manage single keys or credential pools; import local agent login state where supported.
-   **Model catalog**: search all configured models, edit model descriptions, and use those descriptions to guide Claude Code subagent, Task, and Workflow model selection.
-   **Routing engine**: combine built-in agent routing, request-header/body conditions, model-prefix routing, request rewrites, retry policy, and ordered fallback targets.
-   **Fusion models**: publish reusable virtual models that keep a base model's behavior while adding vision, hosted web search, or selected MCP tools.
-   **ToolHub**: merge multiple MCP servers into one dynamic MCP server so agents can resolve tools only when a task needs them; desktop builds can also expose built-in browser automation and Chrome login-state import.
-   **API keys and quotas**: create CCR client keys with expiration and local request/token/image limits, separate from upstream provider credentials.
-   **Logs and observability**: inspect request/response details, resolved provider and model, credential, status, latency, token usage, estimated cost, tool calls, and agent execution traces.
-   **Proxy and networking**: run CCR as a local HTTP/HTTPS proxy, optionally install the CA certificate, route supported API traffic through CCR, and capture network exchanges for debugging.
-   **Bot relay**: connect agent profiles to supported IM platforms including Weixin iLink, WeCom, Slack, Discord, Telegram, LINE, Feishu, and DingTalk.
-   **Extensions**: install wrapper plugins and core gateway plugins that can register local routes, proxy routes, provider account connectors, apps, and virtual models.

Documentation
-------------

Read the full documentation at ccrdesk.top, including the CLI reference and Docker deployment guide.

Download And Install
--------------------

1.  Open the GitHub Releases page.
2.  Download the package for your platform:
    -   macOS Apple Silicon: `Claude-Code-Router_<version>-mac-Apple-Silicon-arm64.dmg` or `.zip`
    -   macOS Intel: `Claude-Code-Router_<version>-mac-Intel-x64.dmg` or `.zip`
    -   Windows: `Claude Code Router_<version>.exe`
    -   Linux: `Claude Code Router_<version>.AppImage`
3.  Install and launch **Claude Code Router**.
4.  On first launch, CCR creates its local configuration database:
    -   macOS/Linux: `~/.claude-code-router/config.sqlite`
    -   Windows: `%APPDATA%\claude-code-router\config.sqlite`

CCR stores runtime configuration in SQLite. A legacy `config.json` is read only once for migration when no SQLite config exists.

After the service is started from the **Server** page, CCR listens on `http://127.0.0.1:3456` by default. The **Server** page controls the gateway `Host`, `Port`, proxy mode, system proxy, network capture, and CA certificate status.

CLI And Docker
--------------

The npm CLI requires Node.js 22 or newer and provides the browser management UI, gateway, and Agent Config launch commands without Electron:

npm install -g @musistudio/claude-code-router
ccr ui

The CLI management UI defaults to `http://127.0.0.1:3458`, while its model gateway defaults to `http://127.0.0.1:3456`. See the complete CLI reference for background/foreground service commands, options, profile launching, authentication, and data locations.

To run the browser UI and gateway behind one Nginx port with persistent Docker storage:

docker compose up -d --build

Docker exposes both management and gateway routes at `http://127.0.0.1:3458` by default. Read the Docker deployment guide before remote exposure; it covers the internal port topology, management and gateway authentication, `CCR_PUBLIC_BASE_URL`, volumes, backup/restore, upgrades, and health checks.

Quick Start
-----------

CCR can be configured entirely from the desktop UI. Use this setup order for a clean first run.

### 1\. Add a provider

Open **Providers**, click **Add Provider**, then choose a built-in preset, import a supported local agent login state, or select **Other / custom API endpoint**. Fill in the provider name, base URL, protocol, API key, and model list. Run protocol probing and model connectivity checks when available, then save the provider.

### 2\. Configure routing

Open **Routing** to enable built-in agent routes, add conditional rules, configure request rewrites, and set fallback behavior. Use **Add Routing Rule** for request conditions, model-prefix routing, or rule-level fallback targets.

### 3\. Start the gateway

Open **Server** and click **Start**. After the page shows Running, CCR listens on `http://127.0.0.1:3456` by default. Enable **Auto start** if you want CCR to start the local gateway whenever the desktop app opens.

### 4\. Connect your agent tool

Open **Agent Config** and choose the client you want to use. Configure Claude Code, Codex, Grok CLI, or ZCode, select the target model and effect scope, then apply the config. For app entries, use **Open Agent** to launch the target app through CCR.

### 5\. Monitor and adjust

Use **Settings → Logs & Observability** to enable request logs and agent observability. Use **Logs** to confirm `request model`, `resolved provider`, `resolved model`, status, tokens, latency, and errors. Use the dashboard and tray window for token, cost, model distribution, and account status.

Acknowledgements
----------------

Codex support is powered by musistudio/codexl.

Support & Sponsoring
--------------------

If you find this project helpful, please consider sponsoring its development. Your support is greatly appreciated.

  
One-time support via Ko-fi

  
International sponsorship

**Alipay**  

**WeChat Pay**  

### Our Sponsors

A huge thank you to all our sponsors for their generous support.

  
**Z智谱**

  
**AIHubmix**

  
**BurnCloud**

  
**302.AI**

  
**RunAPI**

  
**TeamoRouter**

  
**code0.ai**

  
**claudeapi**

  
**Qiniu Cloud AI**

  
**Fenno.ai**

  
**Unity2.Ai**

#### Community Sponsors

@Simon Leischnig

@duanshuaimin

@vrgitadmin

@\*o

@ceilwoo

@\*说

@\*更

@K\*g

@R\*R

@bobleer

@\*苗

@\*划

@Clarence-pan

@carter003

@S\*r

@\*晖

@\*敏

@Z\*z

@\*然

@cluic

@\*苗

@PromptExpert

@\*应

@yusnake

@\*飞

@董\*

@\*汀

@\*涯

@\*:-）

@\*\*磊

@\*琢

@\*成

@Z\*o

@\*琨

@congzhangzh

@\*\_

@Z\*m

@\*鑫

@c\*y

@\*昕

@witsice

@b\*g

@\*亿

@\*辉

@JACK

@\*光

@W\*l

@kesku

@biguncle

@二吉吉

@a\*g

@\*林

@\*咸

@\*明

@S\*y

@f\*o

@\*智

@F\*t

@r\*c

@qierkang

@\*军

@snrise-z

@\*王

@greatheart1000

@\*王

@zcutlip

@Peng-YM

@\*更

@\*.

@F\*t

@\*政

@\*铭

@\*叶

@七\*o

@\*青

@\*\*晨

@\*远

@\*霄

@\*\*吉

@\*\*飞

@\*\*驰

@x\*g

@\*\*东

@\*落

@哆\*k

@\*涛

@苗大

@\*呢

@d\*u

@crizcraig

s\*s

\*火

\*勤

\*\*锟

\*涛

\*\*明

\*知

\*语

\*瓜

If your name is masked, please contact me via my homepage email to update it with your GitHub username.

License
-------

This project is licensed under the MIT License.
