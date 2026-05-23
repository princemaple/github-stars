---
project: data-formulator
stars: 15732
description: 🪄 Create rich visualizations with AI 
url: https://github.com/microsoft/data-formulator
---

  Data Formulator: AI-powered Data Visualization
================================================

🪄 Explore data with visualizations, powered by AI agents.

 

       

News 🔥🔥🔥
-----------

\[05-11-2026\] **Data Formulator 0.7 (alpha 2)** — A new chapter for AI-powered data exploration

-   🔌 **Data connectors** — first-class persistent connection to Superset, Kusto, Cosmos DB, MySQL, PostgreSQL, MSSQL, S3, Azure Blob, BigQuery, and more, with SSO, lazy catalog loading, search, and smart filters.
-   💬 **Conversational agent with thread memory** — a unified `DataAgent` that weaves explanation, exploration, visualization, and recommendation into one fluid conversation, carrying context across turns so the agent stays in sync with your train of thought.
-   🗂️ **Persistent session & workspace management** — identity-isolated workspaces with local and Azure Blob backends; sessions persist across restarts with timestamps and sort.
-   📊 **Expressive visualization** — 30+ chart types via a new semantic chart engine (area, streamgraph, candlestick, pie, radar, maps, …), plus a chart style-refinement agent that turns rough charts into presentation-ready visuals: restyle in one click, refine typography, color, layout, and annotations through natural language.
-   📚 **Knowledge distillation (experimental)** — agents distill reusable skills and experiences from your sessions into a shared knowledge library that informs future sessions.

> Install the pre-release with `pip install --pre data-formulator` or pin `==0.7.0a2`.

Tip

**Are you a developer?** Join us to shape the future of AI-powered data exploration! We're looking for help with new agents, data connectors, chart templates, and more. Check out the Developers' Guide and our open issues.

Previous Updates
----------------

Here are milestones that lead to the current design:

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

**Data Formulator** is a Microsoft Research prototype for data exploration with visualizations powered by AI agents.

Data Formulator enables analysts to explore data with visualizations. Started with data in any format (screenshot, text, csv, or database), you can work with AI agents with a novel blended interface that combines _user interface interactions (UI)_ and _natural language (NL) inputs_ to communicate their intents, control branching exploration directions, and create reports to share their insights.

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
