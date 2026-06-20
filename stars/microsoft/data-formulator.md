---
project: data-formulator
stars: 15836
description: 🪄 Create rich visualizations with AI 
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

News 🔥🔥🔥
-----------

\[05-28-2026\] **Data Formulator 0.7** — turn ANY data into insights in five easy steps:

1.  **Connect.** Governed, reusable connections to databases, warehouses, BI systems, object stores, and files (Superset, Kusto, Cosmos DB, MySQL, PostgreSQL, MSSQL, BigQuery, S3, Azure Blob, …). Need a custom source? Point your coding agent at the data loader plugin guide.
2.  **Load.** Ask the **data-loading agent** to find tables from connected databases, or extract data from Excel files, images, websites, and text.
3.  **Explore.** A unified **Data Agent** with thread memory inspects data, runs sandboxed code, and weaves explanation, exploration, and recommendation into one fluid conversation — grounded in your context. The **Data Thread** keeps questions, intermediate results, and charts navigable: revisit earlier steps, branch into alternatives, and compare side by side.
4.  **Refine.** 30+ chart types (area, streamgraph, candlestick, radar, maps, KPI, …) via a new semantic chart engine, plus a **style-refinement agent** that turns rough charts into presentation-ready visuals through natural language.
5.  **Share.** Build reports and export as image or PDF to tell the story.

➕ **Persistent sessions & workspaces** — identity-isolated, saved across restarts. Data Formulator is your de facto data analysis pane.

**Multilingual UI** — Data Formulator now speaks Chinese in addition to English (没错，DF现在会说中文了！). More languages on the way — contributions welcome.

> Install with `pip install data_formulator` or run instantly with `uvx data_formulator`.

Tip

**Are you a developer?** Join us to shape the future of AI-powered data exploration! We're looking for help with new agents, data connectors, chart templates, and more. Check out the Developers' Guide and our open issues.

Previous Updates
----------------

Here are milestones that lead to the current design:

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

Research Papers
---------------

-   Data Formulator 2: Iteratively Creating Rich Visualizations with AI

```
@article{wang2024dataformulator2iteratively,
      title={Data Formulator 2: Iteratively Creating Rich Visualizations with AI}, 
      author={Chenglong Wang and Bongshin Lee and Steven Drucker and Dan Marshall and Jianfeng Gao},
      year={2024},
      booktitle={ArXiv preprint arXiv:2408.16119},
}
```

-   Data Formulator: AI-powered Concept-driven Visualization Authoring

```
@article{wang2023data,
  title={Data Formulator: AI-powered Concept-driven Visualization Authoring},
  author={Wang, Chenglong and Thompson, John and Lee, Bongshin},
  journal={IEEE Transactions on Visualization and Computer Graphics},
  year={2023},
  publisher={IEEE}
}
```

Contributing
------------

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repositories using our CLA.

This project has adopted the Microsoft Open Source Code of Conduct. For more information see the Code of Conduct FAQ or contact opencode@microsoft.com with any additional questions or comments.

Trademarks
----------

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow Microsoft's Trademark & Brand Guidelines. Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos are subject to those third-party's policies.
