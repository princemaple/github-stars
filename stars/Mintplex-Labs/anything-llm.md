---
project: anything-llm
stars: 28183
description: The all-in-one Desktop & Docker AI application with built-in RAG, AI agents, and more.
url: https://github.com/Mintplex-Labs/anything-llm
---

**AnythingLLM:** The all-in-one AI app you were looking for.  
Chat with your docs, use AI Agents, hyper-configurable, multi-user, & no frustrating set up required.

| | Docs | Hosted Instance

**English** · 简体中文 · 日本語

👉 AnythingLLM for desktop (Mac, Windows, & Linux)! Download Now

A full-stack application that enables you to turn any document, resource, or piece of content into context that any LLM can use as references during chatting. This application allows you to pick and choose which LLM or Vector Database you want to use as well as supporting multi-user management and permissions.

Watch the demo!

### Product Overview

AnythingLLM is a full-stack application where you can use commercial off-the-shelf LLMs or popular open source LLMs and vectorDB solutions to build a private ChatGPT with no compromises that you can run locally as well as host remotely and be able to chat intelligently with any documents you provide it.

AnythingLLM divides your documents into objects called `workspaces`. A Workspace functions a lot like a thread, but with the addition of containerization of your documents. Workspaces can share documents, but they do not talk to each other so you can keep your context for each workspace clean.

Cool features of AnythingLLM
----------------------------

-   🆕 **Custom AI Agents**
-   🖼️ **Multi-modal support (both closed and open-source LLMs!)**
-   👤 Multi-user instance support and permissioning _Docker version only_
-   🦾 Agents inside your workspace (browse the web, run code, etc)
-   💬 Custom Embeddable Chat widget for your website _Docker version only_
-   📖 Multiple document type support (PDF, TXT, DOCX, etc)
-   Simple chat UI with Drag-n-Drop funcitonality and clear citations.
-   100% Cloud deployment ready.
-   Works with all popular closed and open-source LLM providers.
-   Built-in cost & time-saving measures for managing very large documents compared to any other chat UI.
-   Full Developer API for custom integrations!
-   Much more...install and find out!

### Supported LLMs, Embedder Models, Speech models, and Vector Databases

**Large Language Models (LLMs):**

-   Any open-source llama.cpp compatible model
-   OpenAI
-   OpenAI (Generic)
-   Azure OpenAI
-   AWS Bedrock
-   Anthropic
-   NVIDIA NIM (chat models)
-   Google Gemini Pro
-   Hugging Face (chat models)
-   Ollama (chat models)
-   LM Studio (all models)
-   LocalAi (all models)
-   Together AI (chat models)
-   Fireworks AI (chat models)
-   Perplexity (chat models)
-   OpenRouter (chat models)
-   DeepSeek (chat models)
-   Mistral
-   Groq
-   Cohere
-   KoboldCPP
-   LiteLLM
-   Text Generation Web UI
-   Apipie
-   xAI
-   Novita AI (chat models)

**Embedder models:**

-   AnythingLLM Native Embedder (default)
-   OpenAI
-   Azure OpenAI
-   LocalAi (all)
-   Ollama (all)
-   LM Studio (all)
-   Cohere

**Audio Transcription models:**

-   AnythingLLM Built-in (default)
-   OpenAI

**TTS (text-to-speech) support:**

-   Native Browser Built-in (default)
-   PiperTTSLocal - runs in browser
-   OpenAI TTS
-   ElevenLabs
-   Any OpenAI Compatible TTS service.

**STT (speech-to-text) support:**

-   Native Browser Built-in (default)

**Vector Databases:**

-   LanceDB (default)
-   Astra DB
-   Pinecone
-   Chroma
-   Weaviate
-   Qdrant
-   Milvus
-   Zilliz

### Technical Overview

This monorepo consists of three main sections:

-   `frontend`: A viteJS + React frontend that you can run to easily create and manage all your content the LLM can use.
-   `server`: A NodeJS express server to handle all the interactions and do all the vectorDB management and LLM interactions.
-   `collector`: NodeJS express server that process and parses documents from the UI.
-   `docker`: Docker instructions and build process + information for building from source.
-   `embed`: Submodule for generation & creation of the web embed widget.
-   `browser-extension`: Submodule for the chrome browser extension.

🛳 Self Hosting
---------------

Mintplex Labs & the community maintain a number of deployment methods, scripts, and templates that you can use to run AnythingLLM locally. Refer to the table below to read how to deploy on your preferred environment or to automatically deploy.

Docker

AWS

GCP

Digital Ocean

Render.com

Railway

RepoCloud

Elestio

or set up a production AnythingLLM instance without Docker →

How to setup for development
----------------------------

-   `yarn setup` To fill in the required `.env` files you'll need in each of the application sections (from root of repo).
    -   Go fill those out before proceeding. Ensure `server/.env.development` is filled or else things won't work right.
-   `yarn dev:server` To boot the server locally (from root of repo).
-   `yarn dev:frontend` To boot the frontend locally (from root of repo).
-   `yarn dev:collector` To then run the document collector (from root of repo).

Learn about documents

Learn about vector caching

External Apps & Integrations
----------------------------

_These are apps that are not maintained by Mintplex Labs, but are compatible with AnythingLLM. A listing here is not an endorsement._

-   Midori AI Subsystem Manager - A streamlined and efficient way to deploy AI systems using Docker container technology.
-   Coolify - Deploy AnythingLLM with a single click.
-   GPTLocalhost for Microsoft Word - A local Word Add-in for you to use AnythingLLM in Microsoft Word.

Telemetry & Privacy
-------------------

AnythingLLM by Mintplex Labs Inc contains a telemetry feature that collects anonymous usage information.

More about Telemetry & Privacy for AnythingLLM

### Why?

We use this information to help us understand how AnythingLLM is used, to help us prioritize work on new features and bug fixes, and to help us improve AnythingLLM's performance and stability.

### Opting out

Set `DISABLE_TELEMETRY` in your server or docker .env settings to "true" to opt out of telemetry. You can also do this in-app by going to the sidebar > `Privacy` and disabling telemetry.

### What do you explicitly track?

We will only track usage details that help us make product and roadmap decisions, specifically:

-   Typ of your installation (Docker or Desktop)
-   When a document is added or removed. No information _about_ the document. Just that the event occurred. This gives us an idea of use.
-   Type of vector database in use. Let's us know which vector database provider is the most used to prioritize changes when updates arrive for that provider.
-   Type of LLM in use. Let's us know the most popular choice and prioritize changes when updates arrive for that provider.
-   Chat is sent. This is the most regular "event" and gives us an idea of the daily-activity of this project across all installations. Again, only the event is sent - we have no information on the nature or content of the chat itself.

You can verify these claims by finding all locations `Telemetry.sendTelemetry` is called. Additionally these events are written to the output log so you can also see the specific data which was sent - if enabled. No IP or other identifying information is collected. The Telemetry provider is PostHog - an open-source telemetry collection service.

View all telemetry events in source code

👋 Contributing
---------------

-   create issue
-   create PR with branch name format of `<issue number>-<short name>`
-   LGTM from core-team

🌟 Contributors
---------------

🔗 More Products
----------------

-   **VectorAdmin:** An all-in-one GUI & tool-suite for managing vector databases.
-   **OpenAI Assistant Swarm:** Turn your entire library of OpenAI assistants into one single army commanded from a single agent.

* * *

Copyright © 2024 Mintplex Labs.  
This project is MIT licensed.