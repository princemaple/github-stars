---
project: AutoGPT
stars: 180777
description: AutoGPT is the vision of accessible AI for everyone, to use and to build on. Our mission is to provide the tools, so that you can focus on what matters.
url: https://github.com/Significant-Gravitas/AutoGPT
---

AutoGPT: Build, Deploy, and Run AI Agents
=========================================

   

Deutsch | Español | français | 日本語 | 한국어 | Português | Русский | 中文

**AutoGPT** is a powerful platform that allows you to create, deploy, and manage continuous AI agents that automate complex workflows.

Hosting Options
---------------

-   Download to self-host (Free!)
-   Join the Waitlist for the cloud-hosted beta (Closed Beta - Public release Coming Soon!)

How to Self-Host the AutoGPT Platform
-------------------------------------

Note

Setting up and hosting the AutoGPT Platform yourself is a technical process. If you'd rather something that just works, we recommend joining the waitlist for the cloud-hosted beta.

### System Requirements

Before proceeding with the installation, ensure your system meets the following requirements:

#### Hardware Requirements

-   CPU: 4+ cores recommended
-   RAM: Minimum 8GB, 16GB recommended
-   Storage: At least 10GB of free space

#### Software Requirements

-   Operating Systems:
    -   Linux (Ubuntu 20.04 or newer recommended)
    -   macOS (10.15 or newer)
    -   Windows 10/11 with WSL2
-   Required Software (with minimum versions):
    -   Docker Engine (20.10.0 or newer)
    -   Docker Compose (2.0.0 or newer)
    -   Git (2.30 or newer)
    -   Node.js (16.x or newer)
    -   npm (8.x or newer)
    -   VSCode (1.60 or newer) or any modern code editor

#### Network Requirements

-   Stable internet connection
-   Access to required ports (will be configured in Docker)
-   Ability to make outbound HTTPS connections

### Updated Setup Instructions:

We've moved to a fully maintained and regularly updated documentation site.

👉 Follow the official self-hosting guide here

This tutorial assumes you have Docker, VSCode, git and npm installed.

* * *

#### ⚡ Quick Setup with One-Line Script (Recommended for Local Hosting)

Skip the manual steps and get started in minutes using our automatic setup script.

For macOS/Linux:

```
curl -fsSL https://setup.agpt.co/install.sh -o install.sh && bash install.sh
```

For Windows (PowerShell):

```
powershell -c "iwr https://setup.agpt.co/install.bat -o install.bat; ./install.bat"
```

This will install dependencies, configure Docker, and launch your local instance — all in one go.

### 🧱 AutoGPT Frontend

The AutoGPT frontend is where users interact with our powerful AI automation platform. It offers multiple ways to engage with and leverage our AI agents. This is the interface where you'll bring your AI automation ideas to life:

**Agent Builder:** For those who want to customize, our intuitive, low-code interface allows you to design and configure your own AI agents.

**Workflow Management:** Build, modify, and optimize your automation workflows with ease. You build your agent by connecting blocks, where each block performs a single action.

**Deployment Controls:** Manage the lifecycle of your agents, from testing to production.

**Ready-to-Use Agents:** Don't want to build? Simply select from our library of pre-configured agents and put them to work immediately.

**Agent Interaction:** Whether you've built your own or are using pre-configured agents, easily run and interact with them through our user-friendly interface.

**Monitoring and Analytics:** Keep track of your agents' performance and gain insights to continually improve your automation processes.

Read this guide to learn how to build your own custom blocks.

### 💽 AutoGPT Server

The AutoGPT Server is the powerhouse of our platform This is where your agents run. Once deployed, agents can be triggered by external sources and can operate continuously. It contains all the essential components that make AutoGPT run smoothly.

**Source Code:** The core logic that drives our agents and automation processes.

**Infrastructure:** Robust systems that ensure reliable and scalable performance.

**Marketplace:** A comprehensive marketplace where you can find and deploy a wide range of pre-built agents.

### 🐙 Example Agents

Here are two examples of what you can do with AutoGPT:

1.  **Generate Viral Videos from Trending Topics**
    
    -   This agent reads topics on Reddit.
    -   It identifies trending topics.
    -   It then automatically creates a short-form video based on the content.
2.  **Identify Top Quotes from Videos for Social Media**
    
    -   This agent subscribes to your YouTube channel.
    -   When you post a new video, it transcribes it.
    -   It uses AI to identify the most impactful quotes to generate a summary.
    -   Then, it writes a post to automatically publish to your social media.

These examples show just a glimpse of what you can achieve with AutoGPT! You can create customized workflows to build agents for any use case.

* * *

### **License Overview:**

🛡️ **Polyform Shield License:** All code and content within the `autogpt_platform` folder is licensed under the Polyform Shield License. This new project is our in-developlemt platform for building, deploying and managing agents.  
_Read more about this effort_

🦉 **MIT License:** All other portions of the AutoGPT repository (i.e., everything outside the `autogpt_platform` folder) are licensed under the MIT License. This includes the original stand-alone AutoGPT Agent, along with projects such as Forge, agbenchmark and the AutoGPT Classic GUI.  
We also publish additional work under the MIT Licence in other repositories, such as GravitasML which is developed for and used in the AutoGPT Platform. See also our MIT Licenced Code Ability project.

* * *

### Mission

Our mission is to provide the tools, so that you can focus on what matters:

-   🏗️ **Building** - Lay the foundation for something amazing.
-   🧪 **Testing** - Fine-tune your agent to perfection.
-   🤝 **Delegating** - Let AI work for you, and have your ideas come to life.

Be part of the revolution! **AutoGPT** is here to stay, at the forefront of AI innovation.

**📖 Documentation**  |  **🚀 Contributing**

* * *

🤖 AutoGPT Classic
------------------

> Below is information about the classic version of AutoGPT.

**🛠️ Build your own Agent - Quickstart**

### 🏗️ Forge

**Forge your own agent!** – Forge is a ready-to-go toolkit to build your own agent application. It handles most of the boilerplate code, letting you channel all your creativity into the things that set _your_ agent apart. All tutorials are located here. Components from `forge` can also be used individually to speed up development and reduce boilerplate in your agent project.

🚀 **Getting Started with Forge** – This guide will walk you through the process of creating your own agent and using the benchmark and user interface.

📘 Learn More about Forge

### 🎯 Benchmark

**Measure your agent's performance!** The `agbenchmark` can be used with any agent that supports the agent protocol, and the integration with the project's CLI makes it even easier to use with AutoGPT and forge-based agents. The benchmark offers a stringent testing environment. Our framework allows for autonomous, objective performance evaluations, ensuring your agents are primed for real-world action.

📦 `agbenchmark` on Pypi  |  📘 Learn More about the Benchmark

### 💻 UI

**Makes agents easy to use!** The `frontend` gives you a user-friendly interface to control and monitor your agents. It connects to agents through the agent protocol, ensuring compatibility with many agents from both inside and outside of our ecosystem.

The frontend works out-of-the-box with all agents in the repo. Just use the CLI to run your agent of choice!

📘 Learn More about the Frontend

### ⌨️ CLI

To make it as easy as possible to use all of the tools offered by the repository, a CLI is included at the root of the repo:

$ ./run
Usage: cli.py \[OPTIONS\] COMMAND \[ARGS\]...

Options:
  --help  Show this message and exit.

Commands:
  agent      Commands to create, start and stop agents
  benchmark  Commands to start the benchmark and list tests and categories
  setup      Installs dependencies needed for your system.

Just clone the repo, install dependencies with `./run setup`, and you should be good to go!

🤔 Questions? Problems? Suggestions?
------------------------------------

### Get help - Discord 💬

To report a bug or request a feature, create a GitHub Issue. Please ensure someone else hasn't created an issue for the same topic.

🤝 Sister projects
------------------

### 🔄 Agent Protocol

To maintain a uniform standard and ensure seamless compatibility with many current and future applications, AutoGPT employs the agent protocol standard by the AI Engineer Foundation. This standardizes the communication pathways from your agent to the frontend and benchmark.

* * *

Stars stats
-----------

⚡ Contributors
--------------
