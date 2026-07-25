---
project: data-formulator
stars: 15980
description: 🪄 Data Formulator is an interactive AI-powered data analysis system makes it easy to connect, explore and visualize data.
url: https://github.com/microsoft/data-formulator
---

  Data Formulator: AI-powered Data Visualization
================================================

🪄 Explore data with visualizations, powered by AI agents.

 

       

Why Data Formulator?
--------------------

Your data lives everywhere — databases, warehouses, BI tools, files. Coding agents can help, but only after someone wires them up, and answers come back as walls of code or text that are hard to follow, refine, or share.

Data Formulator makes it simple: **connect any data, ask anything, get charts you can edit, branch, and share** — all on one interactive, visual canvas.

-   **Data & platform teams**: wire up your databases, warehouses, and BI sources once, and give the whole org an AI-powered data exploration layer.
-   **Analysts & users**: ask, edit, branch, share. It's so easy to get insights from good-looking charts.

Data.Formulator-0.7-1080p.mp4

Tip

**Love the charts?** They're built on **Flint** — our open-source visualization language that compiles compact, semantic chart specs into polished Vega-Lite, ECharts, and Chart.js. Explore the project site or drop it into your own app.

News 🔥🔥🔥
-----------

\[07-23-2026\] **Data Formulator 0.8 alpha** (a1–a4, latest: 0.8.0a4) includes:

-   **Conversational database loading.** Agents can discover relevant tables, propose filters, preview results, and revise a loading plan through conversation before importing data.
-   **Unified Data Thread.** Questions, clarifications, explanations, tables, and charts share one conversation history, with branching from earlier steps into new questions, calculated columns, or visualizations.
-   **Expanded chart gallery, powered by Flint.** New bullet, connected scatter, ECDF, Gantt, range area, slope, sparkline, and violin charts, along with improved chart recommendations. Try the open-source Flint chart language in your own applications.
-   **Persistent analyst attachments.** CSV, JSON, Excel, and other attached files remain available to the analyst throughout an exploration instead of being embedded once in a prompt.
-   **Databricks connector.** Browse Unity Catalog catalogs, schemas, and tables, then load Databricks data into the exploration workflow.
-   **Microsoft authentication for enterprise connectors.** SQL Server supports passwordless Microsoft Entra ID authentication through `az login`, including an in-app flow for local deployments. Kusto supports delegated Microsoft sign-in alongside Azure default identity and service principal authentication.
-   **Connector setup and diagnostics.** Connection forms separate connection, scope, and source-specific authentication options. Persistent server logs and an in-app log viewer help diagnose failures.

> Preview with `pip install --pre data_formulator==0.8.0a4` or `uvx data_formulator@0.8.0a4`.

> Install the latest stable release (0.7) with `pip install data_formulator` or run instantly with `uvx data_formulator`.

Previous Updates
----------------

Here are milestones that lead to the current design:

-   **v0.7** (05-28-2026): Turn ANY data into insights in five steps — connect governed data sources, load via agents, explore with the unified `DataAgent` + Data Thread, refine 30+ chart types (semantic chart engine powered by Flint) with a style-refinement agent, and share as reports. Plus persistent sessions & workspaces and a multilingual (English/Chinese) UI.
-   **v0.7 alpha 2** (05-11-2026): Early preview of data connectors, the unified `DataAgent` with thread memory, persistent workspaces, the semantic chart engine, and experimental knowledge distillation.
-   **v0.6** (Demo): Real-time insights from live data — connect to URLs and databases with automatic refresh
-   **uv support**: Faster installation with uv — `uvx data_formulator` or `uv pip install data_formulator`
-   **v0.5.1** (Demo): Community data loaders, US Map & Pie Chart, editable reports, snappier UI
-   **v0.5**: Vibe with your data, in control — agent mode, data extraction, reports
-   **v0.2.2** (Demo): Goal-driven exploration with agent recommendations and performance improvements
-   **v0.2.1.3/4** (Readme | Demo): External data loaders (MySQL, PostgreSQL, MSSQL, Azure Data Explorer, S3, Azure Blob)
-   **v0.2** (Demos): Large data support with DuckDB integration
-   **v0.1.7** (Demos): Dataset anchoring for cleaner workflows
-   **v0.1.6** (Demo): Multi-table support with automatic joins
-   **Model Support**: OpenAI, Azure, Ollama, Anthropic via LiteLLM (feedback)
-   **Python Package**: Easy local installation (try it)
-   **Visualization Challenges**: Test your skills (challenges)
-   **Data Extraction**: Parse data from images and text (demo)
-   **Initial Release**: Blog | Video

Overview
--------

**Data Formulator** is a Microsoft Research project for data exploration with visualizations powered by AI agents. It combines _UI interactions_ with _natural language_ so analysts can communicate intent, branch into alternative analyses, and share results — starting from any data format (screenshot, text, CSV, or database).

Get Started
-----------

Play with Data Formulator with one of the following options.

-   **Option 1: Install via uv (recommended)**
    
    uv is an extremely fast Python package manager. If you have uv installed, you can run Data Formulator directly without any setup:
    
    uvx data\_formulator
    
    Run `uvx data_formulator --help` to see all available options, such as custom port, sandboxing mode, and data storage location.
    
-   **Option 2: Install via pip**
    
    Use pip for installation (recommend: install it in a virtual environment).
    
    pip install data\_formulator # install
    python -m data\_formulator # run
    
    Data Formulator will be automatically opened in the browser at http://localhost:5567.
    
-   **Option 3: Run with Docker**
    
    docker compose up --build
    
    Open http://localhost:5567 in your browser. To stop, press `Ctrl+C` or run `docker compose down`.
    
-   **Option 4: Codespaces**
    
    You can run Data Formulator in Codespaces; we have everything pre-configured. For more details, see CODESPACES.md.
    
-   **Option 5: Working as developer**
    
    You can build Data Formulator locally and develop your own version. Check out details in DEVELOPMENT.md.
    

Using Data Formulator
---------------------

Besides uploading csv, tsv or xlsx files that contain structured data, you can ask Data Formulator to extract data from screenshots, text blocks or websites, or load data from databases use connectors. Then you are ready to explore. Ask visualizaiton questions, edit charts, or delegate some exploration tasks to agents. Then, create reports to share your insights.

data-formulator-tutorial.mp4

Contributing
------------

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repositories using our CLA.

This project has adopted the Microsoft Open Source Code of Conduct. For more information see the Code of Conduct FAQ or contact opencode@microsoft.com with any additional questions or comments.

Trademarks
----------

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow Microsoft's Trademark & Brand Guidelines. Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos are subject to those third-party's policies.
