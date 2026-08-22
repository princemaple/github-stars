---
project: data-formulator
stars: 16888
description: 🪄 Data Formulator is an interactive AI-powered data analysis system makes it easy to connect, explore and visualize data.
url: https://github.com/microsoft/data-formulator
---

  Data Formulator: AI-powered Data Visualization
================================================

🪄 Explore data with visualizations, powered by AI agents.

 

       

Why Data Formulator?
--------------------

Working with data is hard for two simple reasons:

1.  **Data lives everywhere.** Connecting agents to files, databases, warehouses, and BI tools takes time. It is even harder when agents start answering before the relationships between data sources are clear.
2.  **Questions evolve as you explore.** Each answer can lead to follow-up questions, comparisons, and new directions. A long chat history makes it hard to see where you are and how you got there.

Data Formulator provides one visual workspace for exploring and analyzing data:

1.  **Data connectors** give agents a common way to connect to different data sources and maintains a data memory to remember the relationships between them.
2.  **Data Threads** let you branch into different questions, compare paths, and use visualizations to discover deeper insights without losing context.

Data.Formulator-0.7-1080p.mp4

Tip

**Love the charts?** They're built on **Flint**. It's an open-source visualization language that compiles compact chart specs into polished visualizations.

News 🔥🔥🔥
-----------

\[08-15-2026\] **Data Formulator 0.8 beta 1** (`0.8.0b1`) introduces:

-   **One unified flow:** load data, ask questions, review results, and branch in the Data Thread.
-   **More data sources:** use files, local folders, databases, and platforms such as Databricks.
-   **Better charts:** explore more Flint-powered charts, recommendations, themes, and styling tools.

> Preview with `pip install --pre data_formulator==0.8.0b1` or `uvx data_formulator@0.8.0b1`. Install the latest stable release (0.7) with `pip install data_formulator` or run instantly with `uvx data_formulator`.

See the changelog for release details.

Previous Updates
----------------

Here are milestones that lead to the current design:

-   **v0.7** (05-28-2026): Turn ANY data into insights in five steps — connect governed data sources, load via agents, explore with the unified `DataAgent` + Data Thread, refine 30+ chart types (semantic chart engine powered by Flint) with a style-refinement agent, and share as reports. Plus persistent sessions & workspaces and a multilingual (English/Chinese) UI.
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

### Desktop downloads

CI builds self-contained Windows and macOS applications for pull requests and every update to `main`. Download the latest archives from the **Artifacts** section of the most recent desktop builds workflow. Workflow artifacts are retained for 30 days. Tagged builds are also attached as permanent downloads to the corresponding GitHub Release.

Extract the archive, then launch Data Formulator using the instructions for your operating system:

-   **Windows:** Run `Data Formulator.exe`. If Microsoft Defender SmartScreen appears, select **More info**, verify that you downloaded the archive from this repository, and then select **Run anyway**.
-   **macOS:** Move `Data Formulator.app` to **Applications**. The first time you open it, macOS may report that Apple could not verify the app. Open **System Settings → Privacy & Security**, scroll to **Security**, and select **Open Anyway** for Data Formulator. Confirm by selecting **Open** when prompted.

Warning

These are automated preview builds and are not currently code-signed or notarized. Only bypass the operating-system warning when the archive was downloaded directly from this repository's workflow artifacts or releases.

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
    
-   **Option 4: Working as developer**
    
    You can build Data Formulator locally and develop your own version. Check out details in DEVELOPMENT.md.
    

Using Data Formulator
---------------------

Start with the data you already have: upload CSV, TSV, Excel, JSON, screenshots, or text; connect to databases and data platforms; or ask the analyst to find and load the data you need. The analyst can discover sources, clarify your request, propose a loading plan, and let you review the data before adding it to the workspace.

Continue the conversation in the **Data Thread**. Ask questions in natural language and follow the reasoning through explanations, tables, and editable charts in one history. Refine a result directly, branch from any earlier step to explore an alternative, or delegate the next investigation to the analyst. When the analysis is ready, compose the results into a report to share.

data-formulator-tutorial.mp4

Contributing
------------

This project welcomes contributions and suggestions. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repositories using our CLA.

This project has adopted the Microsoft Open Source Code of Conduct. For more information see the Code of Conduct FAQ or contact opencode@microsoft.com with any additional questions or comments.

Trademarks
----------

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow Microsoft's Trademark & Brand Guidelines. Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos are subject to those third-party's policies.
