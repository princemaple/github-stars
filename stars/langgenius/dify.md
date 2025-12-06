---
project: dify
stars: 120711
description: Production-ready platform for agentic workflow development.
url: https://github.com/langgenius/dify
---

📌 Introducing Dify Workflow File Upload: Recreate Google NotebookLM Podcast

Dify Cloud · Self-hosting · Documentation · Dify edition overview

Dify is an open-source platform for developing LLM applications. Its intuitive interface combines agentic AI workflows, RAG pipelines, agent capabilities, model management, observability features, and more—allowing you to quickly move from prototype to production.

Quick start
-----------

> Before installing Dify, make sure your machine meets the following minimum system requirements:
> 
> -   CPU >= 2 Core
> -   RAM >= 4 GiB

  

The easiest way to start the Dify server is through Docker Compose. Before running Dify with the following commands, make sure that Docker and Docker Compose are installed on your machine:

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
    **We host a Dify Cloud service for anyone to try with zero setup. It provides all the capabilities of the self-deployed version, and includes 200 free GPT-4 calls in the sandbox plan.
    
-   **Self-hosting Dify Community Edition  
    **Quickly get Dify running in your environment with this starter guide. Use our documentation for further references and more in-depth instructions.
    
-   **Dify for enterprise / organizations  
    **We provide additional enterprise-centric features. Send us an email to discuss your enterprise needs.  
    
    > For startups and small businesses using AWS, check out Dify Premium on AWS Marketplace and deploy it to your own AWS VPC with one click. It's an affordable AMI offering with the option to create apps with custom logo and branding.
    

Staying ahead
-------------

Star Dify on GitHub and be instantly notified of new releases.

Advanced Setup
--------------

### Custom configurations

If you need to customize the configuration, please refer to the comments in our .env.example file and update the corresponding values in your `.env` file. Additionally, you might need to make adjustments to the `docker-compose.yaml` file itself, such as changing image versions, port mappings, or volume mounts, based on your specific deployment environment and requirements. After making any changes, please re-run `docker-compose up -d`. You can find the full list of available environment variables here.

### Metrics Monitoring with Grafana

Import the dashboard to Grafana, using Dify's PostgreSQL database as data source, to monitor metrics in granularity of apps, tenants, messages, and more.

-   Grafana Dashboard by @bowenliang123

### Deployment with Kubernetes

If you'd like to configure a highly-available setup, there are community-contributed Helm Charts and YAML files which allow Dify to be deployed on Kubernetes.

-   Helm Chart by @LeoQuote
-   Helm Chart by @BorisPolonsky
-   Helm Chart by @magicsong
-   YAML file by @Winson-030
-   YAML file by @wyy-holding
-   🚀 NEW! YAML files (Supports Dify v1.6.0) by @Zhoneym

#### Using Terraform for Deployment

Deploy Dify to Cloud Platform with a single click using terraform

##### Azure Global

-   Azure Terraform by @nikawang

##### Google Cloud

-   Google Cloud Terraform by @sotazum

#### Using AWS CDK for Deployment

Deploy Dify to AWS with CDK

##### AWS

-   AWS CDK by @KevinZhao (EKS based)
-   AWS CDK by @tmokmss (ECS based)

#### Using Alibaba Cloud Computing Nest

Quickly deploy Dify to Alibaba cloud with Alibaba Cloud Computing Nest

#### Using Alibaba Cloud Data Management

One-Click deploy Dify to Alibaba Cloud with Alibaba Cloud Data Management

#### Deploy to AKS with Azure Devops Pipeline

One-Click deploy Dify to AKS with Azure Devops Pipeline Helm Chart by @LeoZhang

Contributing
------------

For those who'd like to contribute code, see our Contribution Guide. At the same time, please consider supporting Dify by sharing it on social media and at events and conferences.

> We are looking for contributors to help translate Dify into languages other than Mandarin or English. If you are interested in helping, please see the i18n README for more information, and leave us a comment in the `global-users` channel of our Discord Community Server.

Community & contact
-------------------

-   GitHub Discussion. Best for: sharing feedback and asking questions.
-   GitHub Issues. Best for: bugs you encounter using Dify.AI, and feature proposals. See our Contribution Guide.
-   Discord. Best for: sharing your applications and hanging out with the community.
-   X(Twitter). Best for: sharing your applications and hanging out with the community.

**Contributors**

Star history
------------

Security disclosure
-------------------

To protect your privacy, please avoid posting security issues on GitHub. Instead, report issues to security@dify.ai, and our team will respond with detailed answer.

License
-------

This repository is licensed under the Dify Open Source License, based on Apache 2.0 with additional conditions.
