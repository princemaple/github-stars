---
project: claude-code-router
stars: 35567
description: Use Claude Code as the foundation for coding infrastructure, allowing you to decide how to interact with the model while enjoying updates from Anthropic.
url: https://github.com/musistudio/claude-code-router
---

Claude Code Router Desktop
==========================

Claude Code Router Desktop is a local gateway and desktop control panel for routing agent requests from Claude Code, Codex, ZCode, and compatible clients to the model provider you actually want to use.

Why Use CCR
-----------

-   Use one local endpoint for multiple agent tools instead of configuring every client separately.
-   Route requests with default routing, conditional rules, fallback targets, and request rewrites instead of editing client configuration by hand.
-   Mix providers without changing your workflow. CCR supports OpenAI-compatible APIs, Anthropic Messages, Gemini Generate Content, OpenRouter, DeepSeek, SiliconFlow, Moonshot, Kimi Code, Mistral, Z.AI, Bailian, and custom providers.
-   Control cost and reliability with fallback routing, API key rotation, usage statistics, and request logs.

Features
--------

-   **Overview dashboard**: inspect system status, usage widgets, account balances, model distribution, and share cards.
-   **Provider management**: add provider presets or custom endpoints, probe protocol support, test model connectivity, manage credentials, and monitor supported account balances where available.
-   **Routing rules**: configure default routing, conditional and model-prefix rules, fallback handling, and request rewrites.
-   **Agent Config**: configure Claude Code, Codex, and ZCode launch entries, models, scopes, and multi-instance app profiles.
-   **Gateway compatibility**: translate supported client requests through the local CCR model gateway.
-   **Proxy mode**: capture supported API traffic through a local proxy with optional system proxy integration and network capture.
-   **Fusion models**: combine a base model with vision, web search, or MCP tools into a reusable selectable model.

Documentation
-------------

Read the full documentation at ccrdesk.top.

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
    -   Windows: `%APPDATA%\Claude Code Router\config.sqlite`

CCR stores runtime configuration in SQLite. A legacy `config.json` is read only once for migration when no SQLite config exists.

After the service is started from the **Server** page, CCR listens on `http://localhost:8080` by default. The **Server** page controls the gateway `Host`, `Port`, proxy mode, system proxy, network capture, and CA certificate status.

Quick Start
-----------

CCR can be configured entirely from the desktop UI. Use this setup order for a clean first run.

### 1\. Add a provider

Open **Providers**, click **Add Provider**, then choose a built-in preset or **Other / custom API endpoint**. Fill in the provider name, base URL, protocol, API key, and model list. Run protocol probing and model connectivity checks when available, then save the provider.

### 2\. Configure routing

Open **Routing** to add conditional rules, configure request rewrites, and set fallback behavior.

Use **Add Routing Rule** for request conditions, model-prefix routing, or rule-level fallback targets.

### 3\. Start the gateway

Open **Server** and click **Start**. After the page shows Running, CCR listens on `http://localhost:8080`. Enable **Auto start** if you want CCR to start the local gateway whenever the desktop app opens.

### 4\. Connect your agent tool

Open **Agent Config** and choose the client you want to use. Configure Claude Code, Codex, or ZCode, select the target model and effect scope, then apply the config. For app entries, use the **Open Agent** action to open the target app through CCR.

### 5\. Monitor and adjust

Use **Settings → Logs & Observability** to enable request logs and agent observability. Use **Logs** to confirm `request model`, `resolved provider`, `resolved model`, status, tokens, latency, and errors; use the tray window for quick token and account status.

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
