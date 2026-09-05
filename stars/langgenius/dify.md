---
project: dify
stars: 154535
description: Build Agentic workflows, RAG pipelines, with rich AI model and tool support on one collaborative workspace. Deploy on cloud, VPC, or self-hosted, so teams move from prototype to production without rebuilding the stack.
url: https://github.com/langgenius/dify
---

Dify Cloud · Self-hosting · Documentation · Dify edition overview

Dify is an open-source LLM app development platform. Its intuitive interface combines AI workflow, RAG pipeline, agent capabilities, model management, observability features (including Opik, Langfuse, and Arize Phoenix) and more, letting you quickly go from prototype to production. Here's a list of the core features:

Quick start
-----------

> Before installing Dify, make sure your machine meets the following minimum system requirements:
> 
> -   CPU >= 2 Core
> -   RAM >= 4 GiB

  

The easiest way to start the Dify server is through Docker Compose. Before running Dify with the following commands, make sure that Docker and Docker Compose v2.24.0 or later are installed on your machine:

cd dify
cd docker
cp .env.example .env
docker compose up -d

After running, you can access the Dify dashboard in your browser at http://localhost/install and start the initialization process.

#### Seeking help

Please refer to our FAQ if you encounter problems setting up Dify. Reach out to the community and us if you are still having issues.

> If you'd like to contribute to Dify or do additional development, refer to our guide to deploying from source code

Key features
------------

**1\. Workflow**: Build and test powerful AI workflows on a visual canvas, leveraging all the following features and beyond.

**2\. Comprehensive model support**: Seamless integration with hundreds of proprietary / open-source LLMs from dozens of inference providers and self-hosted solutions, covering GPT, Mistral, Llama3, and any OpenAI API-compatible models. A full list of supported model providers can be found here.

**3\. Prompt IDE**: Intuitive interface for crafting prompts, comparing model performance, and adding additional features such as text-to-speech to a chat-based app.

**4\. RAG Pipeline**: Extensive RAG capabilities that cover everything from document ingestion to retrieval, with out-of-box support for text extraction from PDFs, PPTs, and other common document formats.

**5\. Agent capabilities**: You can define agents based on LLM Function Calling or ReAct, and add pre-built or custom tools for the agent. Dify provides 50+ built-in tools for AI agents, such as Google Search, DALL·E, Stable Diffusion and WolframAlpha.

**6\. LLMOps**: Monitor and analyze application logs and performance over time. You could continuously improve prompts, datasets, and models based on production data and annotations.

**7\. Backend-as-a-Service**: All of Dify's offerings come with corresponding APIs, so you could effortlessly integrate Dify into your own business logic.

Using Dify
----------

-   **Cloud  
    **We host a Dify Cloud service for anyone to try with zero setup. It provides all the capabilities of the self-deployed version, and includes 200 free GPT-4 calls in the sandbox plan. If you run into issues with Dify Cloud, contact our Cloud support team.
    
-   **Self-hosting Dify Community Edition  
    **Quickly get Dify running in your environment with this starter guide. Use our documentation for further references and more in-depth instructions.
    
-   **Dify for enterprise / organizations  
    **We provide additional enterprise-centric features. Send us an email to discuss your enterprise needs.  
    

Staying ahead
-------------

Star Dify on GitHub and be instantly notified of new releases.

Advanced Setup
--------------

For custom configuration, observability, and deployment options, see Advanced Setup.

Contributing
------------

Dify welcomes contributions of all kinds:

-   **Code**: Read the Contribution Guide, then browse good first issues.
-   **Ideas and feedback**: Start or join a GitHub Discussion.
-   **Translations**: Follow the internationalization guide to add or update a locale.
-   **Community**: Share the apps you build, help other users, and spread the word about Dify.

### Contributors

Community & contact
-------------------

Choose the channel that best fits your question:

-   GitHub Discussions: Get help, share feedback, and propose ideas.
-   GitHub Issues: Report reproducible bugs and track engineering work. Read the Contribution Guide before opening one.
-   Discord: Chat in real time, share your apps, and connect with other Dify users.
-   X: Follow Dify for release news and project updates.

Star History
------------

Security disclosure
-------------------

To protect your privacy, please avoid posting security issues on GitHub. Instead, report issues to security@dify.ai, and our team will respond with detailed answer.

License
-------

This repository is licensed under the Dify Open Source License, based on Apache 2.0 with additional conditions.
