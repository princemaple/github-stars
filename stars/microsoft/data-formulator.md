---
project: data-formulator
stars: 14510
description: 🪄 Create rich visualizations with AI 
url: https://github.com/microsoft/data-formulator
---

  Data Formulator: AI-powered Data Visualization
================================================

🪄 Explore data with visualizations, powered by AI agents.

 

       

News 🔥🔥🔥
-----------

\[12-08-2025\] **Data Formulator 0.5.1** — Connect more, visualize more, move faster

-   🔌 **Community data loaders**: Google BigQuery, MySQL, Postgres, MongoDB
-   📊 **New chart types**: US Map & Pie Chart (more to be added soon)
-   ✏️ **Editable reports**: Refine generated reports with Chartifact in markdown style. demo
-   ⚡ **Snappier UI**: Noticeably faster interactions across the board

\[11-07-2025\] Data Formulator 0.5: Vibe with your data, in control

-   📊 **Load (almost) any data**: load structured data, extract data from screenshots, from messy text blocks, or connect to databases.
-   🤖 **Explore data with AI agents**:
    -   In agent mode, provide a high-level goal and ask agents to explore data for you.
    -   To stay in control, directly interact with agents: ask for recommendations or specify chart designs with UI + NL inputs, and AI agents will formulate data to realize your design.
    -   Use data threads to control branching exploration paths: backtrack, branch, or follow up.
-   ✅ **Verify AI generated results**: interact with charts and inspect data, formulas, explanations, and code.
-   📝 **Create reports to share insights**: choose charts you want to share, and ask agents to create reports grounded in data formulated throughout exploration.

Previous Updates
----------------

Here are milestones that lead to the current design:

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

**View detailed update history**

-   \[07-10-2025\] Data Formulator 0.2.2: Start with an analysis goal
    
    -   Some key frontend performance updates.
    -   You can start your exploration with a goal, or, tab and see if the agent can recommend some good exploration ideas for you. Demo
-   \[05-13-2025\] Data Formulator 0.2.1.3/4: External Data Loader
    
    -   We introduced external data loader class to make import data easier. Readme and Demo
        -   Current data loaders: MySQL, Azure Data Explorer (Kusto), Azure Blob and Amazon S3 (json, parquet, csv).
        -   \[07-01-2025\] Updated with: Postgresql, mssql.
    -   Call for action link:
        -   Users: let us know which data source you'd like to load data from.
        -   Developers: let's build more data loaders.
-   \[04-23-2025\] Data Formulator 0.2: working with _large_ data 📦📦📦
    
    -   Explore large data by:
        1.  Upload large data file to the local database (powered by DuckDB).
        2.  Use drag-and-drop to specify charts, and Data Formulator dynamically fetches data from the database to create visualizations (with ⚡️⚡️⚡️ speeds).
        3.  Work with AI agents: they generate SQL queries to transform the data to create rich visualizations!
        4.  Anchor the result / follow up / create a new branch / join tables; let's dive deeper.
    -   Checkout the demos at \[https://github.com/microsoft/data-formulator/releases/tag/0.2\]
    -   Improved overall system performance, and enjoy the updated derive concept functionality.
-   \[03-20-2025\] Data Formulator 0.1.7: Anchoring ⚓︎
    
    -   Anchor an intermediate dataset, so that followup data analysis are built on top of the anchored data, not the original one.
    -   Clean a data and work with only the cleaned data; create a subset from the original data or join multiple data, and then go from there. AI agents will be less likely to get confused and work faster. ⚡️⚡️
    -   Check out the demos at \[https://github.com/microsoft/data-formulator/releases/tag/0.1.7\]
    -   Don't forget to update Data Formulator to test it out!
-   \[02-20-2025\] Data Formulator 0.1.6 released!
    
    -   Now supports working with multiple datasets at once! Tell Data Formulator which data tables you would like to use in the encoding shelf, and it will figure out how to join the tables to create a visualization to answer your question. 🪄
    -   Checkout the demo at \[https://github.com/microsoft/data-formulator/releases/tag/0.1.6\].
    -   Update your Data Formulator to the latest version to play with the new features.
-   \[02-12-2025\] More models supported now!
    
    -   Now supports OpenAI, Azure, Ollama, and Anthropic models (and more powered by LiteLLM);
    -   Models with strong code generation and instruction following capabilities are recommended (gpt-4o, claude-3-5-sonnet etc.);
    -   You can store API keys in `api-keys.env` to avoid typing them every time (see template `api-keys.env.template`).
    -   Let us know which models you have good/bad experiences with, and what models you would like to see supported! \[comment here\]
-   \[11-07-2024\] Minor fun update: data visualization challenges!
    
    -   We added a few visualization challenges with the sample datasets. Can you complete them all? \[try them out!\]
    -   Comment in the issue when you did, or share your results/questions with others! \[comment here\]
-   \[10-11-2024\] Data Formulator python package released!
    
    -   You can now install Data Formulator using Python and run it locally, easily. \[check it out\].
    -   Our Codespaces configuration is also updated for fast start up ⚡️. \[try it now!\]
    -   New experimental feature: load an image or a messy text, and ask AI to parse and clean it for you(!). \[demo\]
-   \[10-01-2024\] Initial release of Data Formulator, check out our \[blog\] and \[video\]!
    

Overview
--------

**Data Formulator** is a Microsoft Research prototype for data exploration with visualizations powered by AI agents.

Data Formulator enables analysts to iteratively explore and visualize data. Started with data in any format (screenshot, text, csv, or database), users can work with AI agents with a novel blended interface that combines _user interface interactions (UI)_ and _natural language (NL) inputs_ to communicate their intents, control branching exploration directions, and create reports to share their insights.

Get Started
-----------

Play with Data Formulator with one of the following options:

-   **Option 1: Install via Python PIP**
    
    Use Python PIP for an easy setup experience, running locally (recommend: install it in a virtual environment).
    
    # install data\_formulator
    pip install data\_formulator
    
    # Run data formulator with this command
    python -m data\_formulator
    
    Data Formulator will be automatically opened in the browser at http://localhost:5000.
    
    _you can specify the port number (e.g., 8080) by `python -m data_formulator --port 8080` if the default port is occupied._
    
-   **Option 2: Codespaces (5 minutes)**
    
    You can also run Data Formulator in Codespaces; we have everything pre-configured. For more details, see CODESPACES.md.
    
-   **Option 3: Working in the developer mode**
    
    You can build Data Formulator locally if you prefer full control over your development environment and develop your own version on top. For detailed instructions, refer to DEVELOPMENT.md.
    

Using Data Formulator
---------------------

### Load Data

Besides uploading csv, tsv or xlsx files that contain structured data, you can ask Data Formulator to extract data from screenshots, text blocks or websites, or load data from databases use connectors. Then you are ready to explore.

### Explore Data

There are four levels to explore data based depending on whether you want more vibe or more control:

-   Level 1 (most control): Create charts with UI via drag-and-drop, if all fields to be visualized are already in the data.
-   Level 2: Specify chart designs with natural language + NL. Describe how new fields should be visualized in your chart, AI will automatically transform data to realize the design.
-   Level 3: Get recommendations: Ask AI agents to recommend charts directly from NL descriptions, or even directly ask for exploration ideas.
-   Level 4 (most vibe): In agent mode, provide a high-level goal and let AI agents automatically plan and explore data in multiple turns. Exploration threads will be created automatically.

data-formulator-tutorial.mp4

-   Level 5: In practice, leverage all of them to keep up with both vibe and control!

### Create Reports

Use the report builder to compose a report of the style you like, based on selected charts. Then share the reports to others!

Developers' Guide
-----------------

Follow the developers' instructions to build your new data analysis tools on top of Data Formulator.

Help wanted:

-   Add more database connectors (#156)
-   Scaling up messy data extractor: more document types and larger files.
-   Adding more chart templates (e.g., maps).
-   other ideas?

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
