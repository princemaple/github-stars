---
project: rasa
stars: 21012
description: 💬   Open source machine learning framework to automate text- and voice-based conversations: NLU, dialogue management, connect to Slack, Facebook, and more - Create chatbots and voice assistants
url: https://github.com/RasaHQ/rasa
---

Rasa Open Source
================

  

### 🚧 **Note: Maintenance Mode** 🚧

Rasa Open Source is currently in maintenance mode.  
The future of building AI agents with Rasa is **Hello Rasa** and **CALM**.

* * *

🚀 The Future of Rasa: Hello Rasa
---------------------------------

**Building reliable AI agents just got easier.**

**Hello Rasa** is our new interactive playground for prototyping AI agents. It combines LLM fluency with the reliability of business logic using our **CALM** (Conversational AI with Language Models) engine.

### Why switch to Hello Rasa?

-   **No setup required:** Open the playground, pick a template (Banking, Telecom, Support), and start building in your browser.
-   **No NLU training:** We have moved beyond intents. The LLM handles dialogue understanding while you define the business flows.
-   **Built-in copilot:** A specialized AI assistant helps you generate code, debug flows, and expand your agent instantly.
-   **Production ready:** Hello Rasa is not just a toy. Export your agent to the Rasa Platform when you are ready to scale.

### Core concepts

-   **CALM:** Combines LLM flexibility with strict business logic. The LLM understands the user; the code enforces the rules.
-   **Flows:** Describe logical steps (e.g., collect money, transfer funds) rather than rigid dialogue trees.
-   **Inspector:** See real-time decision-making. No black boxes.

👉 **Start building for free at Hello Rasa**

* * *

🧠 Join the Agent Engineering Community
---------------------------------------

We are building a home for people shipping real-world AI agents.

Agent Engineering is evolving faster than any single framework. This is a vendor-neutral space to discuss architectures, memory, orchestration, and safety with builders across the industry.

### What you get:

-   **Network:** Meet engineers building production agents
-   **Learn:** Discuss practical patterns, not just theory
-   **Access:** Direct influence on the Hello Rasa roadmap and early access to features

Channel

Purpose

**#agent-design**

Architectures, reasoning, memory, testing

**#showcase**

Show your builds, demos, and repos

**#ask-anything**

Debugging and workflow questions

👉 **Join the Community**

* * *

  
  

Rasa Open Source (Legacy)
=========================

> **Note:** The documentation and installation instructions below apply to the classic Rasa Open Source framework. For the latest CALM-based experience, see the Hello Rasa section above.

Rasa is an open source machine learning framework for automating text and voice-based conversations. With Rasa, you can build contextual assistants on:

-   Facebook Messenger
-   Slack
-   Google Hangouts
-   Webex Teams
-   Microsoft Bot Framework
-   Rocket.Chat
-   Mattermost
-   Telegram
-   Twilio
-   Your own custom conversational channels

Rasa helps you build contextual assistants that can handle layered conversations with lots of back-and-forth.

### 📚 Resources

-   🤓 Read the docs
-   😁 Install Rasa
-   🚀 Learn all about Conversational AI
-   🏢 Explore the enterprise platform

Development Internals & Contributing
------------------------------------

We are happy to receive contributions. Please review our Contribution Guidelines before getting started.

### Installation for Development

Rasa uses **Poetry** for packaging and dependency management.

1.  **Install Poetry**: Follow the official guide.
2.  **Build from source**:
    
    make install
    
    _Note for macOS users_: If you run into compiler issues, try `export SYSTEM_VERSION_COMPAT=1` before installation.

### Running Tests

Make sure you have development requirements installed:

make prepare-tests-ubuntu # Ubuntu/Debian
make prepare-tests-macos  # macOS
make test                 # Run tests

### Releases

Rasa follows Semantic Versioning.

-   **Major**: Incompatible API changes
-   **Minor**: Backward-compatible functionality
-   **Patch**: Backward-compatible bug fixes

For full details on our release cadence and maintenance policy, visit our Product Release and Maintenance Policy.

License
-------

Licensed under the Apache License, Version 2.0. Copyright 2022 Rasa Technologies GmbH. Copy of the license.
