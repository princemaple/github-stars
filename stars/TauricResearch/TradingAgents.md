---
project: TradingAgents
stars: 28136
description: TradingAgents: Multi-Agents LLM Financial Trading Framework
url: https://github.com/TauricResearch/TradingAgents
---

  

Deutsch | Español | français | 日本語 | 한국어 | Português | Русский | 中文

* * *

TradingAgents: Multi-Agents LLM Financial Trading Framework
===========================================================

> 🎉 **TradingAgents** officially released! We have received numerous inquiries about the work, and we would like to express our thanks for the enthusiasm in our community.
> 
> So we decided to fully open-source the framework. Looking forward to building impactful projects with you!

🚀 TradingAgents | ⚡ Installation & CLI | 🎬 Demo | 📦 Package Usage | 🤝 Contributing | 📄 Citation

TradingAgents Framework
-----------------------

TradingAgents is a multi-agent trading framework that mirrors the dynamics of real-world trading firms. By deploying specialized LLM-powered agents: from fundamental analysts, sentiment experts, and technical analysts, to trader, risk management team, the platform collaboratively evaluates market conditions and informs trading decisions. Moreover, these agents engage in dynamic discussions to pinpoint the optimal strategy.

> TradingAgents framework is designed for research purposes. Trading performance may vary based on many factors, including the chosen backbone language models, model temperature, trading periods, the quality of data, and other non-deterministic factors. It is not intended as financial, investment, or trading advice.

Our framework decomposes complex trading tasks into specialized roles. This ensures the system achieves a robust, scalable approach to market analysis and decision-making.

### Analyst Team

-   Fundamentals Analyst: Evaluates company financials and performance metrics, identifying intrinsic values and potential red flags.
-   Sentiment Analyst: Analyzes social media and public sentiment using sentiment scoring algorithms to gauge short-term market mood.
-   News Analyst: Monitors global news and macroeconomic indicators, interpreting the impact of events on market conditions.
-   Technical Analyst: Utilizes technical indicators (like MACD and RSI) to detect trading patterns and forecast price movements.

### Researcher Team

-   Comprises both bullish and bearish researchers who critically assess the insights provided by the Analyst Team. Through structured debates, they balance potential gains against inherent risks.

### Trader Agent

-   Composes reports from the analysts and researchers to make informed trading decisions. It determines the timing and magnitude of trades based on comprehensive market insights.

### Risk Management and Portfolio Manager

-   Continuously evaluates portfolio risk by assessing market volatility, liquidity, and other risk factors. The risk management team evaluates and adjusts trading strategies, providing assessment reports to the Portfolio Manager for final decision.
-   The Portfolio Manager approves/rejects the transaction proposal. If approved, the order will be sent to the simulated exchange and executed.

Installation and CLI
--------------------

### Installation

Clone TradingAgents:

git clone https://github.com/TauricResearch/TradingAgents.git
cd TradingAgents

Create a virtual environment in any of your favorite environment managers:

conda create -n tradingagents python=3.13
conda activate tradingagents

Install dependencies:

pip install -r requirements.txt

### Required APIs

You will need the OpenAI API for all the agents, and Alpha Vantage API for fundamental and news data (default configuration).

export OPENAI\_API\_KEY=$YOUR\_OPENAI\_API\_KEY
export ALPHA\_VANTAGE\_API\_KEY=$YOUR\_ALPHA\_VANTAGE\_API\_KEY

Alternatively, you can create a `.env` file in the project root with your API keys (see `.env.example` for reference):

cp .env.example .env
# Edit .env with your actual API keys

**Note:** We are happy to partner with Alpha Vantage to provide robust API support for TradingAgents. You can get a free AlphaVantage API here, TradingAgents-sourced requests also have increased rate limits to 60 requests per minute with no daily limits. Typically the quota is sufficient for performing complex tasks with TradingAgents thanks to Alpha Vantage’s open-source support program. If you prefer to use OpenAI for these data sources instead, you can modify the data vendor settings in `tradingagents/default_config.py`.

### CLI Usage

You can also try out the CLI directly by running:

python -m cli.main

You will see a screen where you can select your desired tickers, date, LLMs, research depth, etc.

An interface will appear showing results as they load, letting you track the agent's progress as it runs.

TradingAgents Package
---------------------

### Implementation Details

We built TradingAgents with LangGraph to ensure flexibility and modularity. We utilize `o1-preview` and `gpt-4o` as our deep thinking and fast thinking LLMs for our experiments. However, for testing purposes, we recommend you use `o4-mini` and `gpt-4.1-mini` to save on costs as our framework makes **lots of** API calls.

### Python Usage

To use TradingAgents inside your code, you can import the `tradingagents` module and initialize a `TradingAgentsGraph()` object. The `.propagate()` function will return a decision. You can run `main.py`, here's also a quick example:

from tradingagents.graph.trading\_graph import TradingAgentsGraph
from tradingagents.default\_config import DEFAULT\_CONFIG

ta \= TradingAgentsGraph(debug\=True, config\=DEFAULT\_CONFIG.copy())

\# forward propagate
\_, decision \= ta.propagate("NVDA", "2024-05-10")
print(decision)

You can also adjust the default configuration to set your own choice of LLMs, debate rounds, etc.

from tradingagents.graph.trading\_graph import TradingAgentsGraph
from tradingagents.default\_config import DEFAULT\_CONFIG

\# Create a custom config
config \= DEFAULT\_CONFIG.copy()
config\["deep\_think\_llm"\] \= "gpt-4.1-nano"  \# Use a different model
config\["quick\_think\_llm"\] \= "gpt-4.1-nano"  \# Use a different model
config\["max\_debate\_rounds"\] \= 1  \# Increase debate rounds

\# Configure data vendors (default uses yfinance and Alpha Vantage)
config\["data\_vendors"\] \= {
    "core\_stock\_apis": "yfinance",           \# Options: yfinance, alpha\_vantage, local
    "technical\_indicators": "yfinance",      \# Options: yfinance, alpha\_vantage, local
    "fundamental\_data": "alpha\_vantage",     \# Options: openai, alpha\_vantage, local
    "news\_data": "alpha\_vantage",            \# Options: openai, alpha\_vantage, google, local
}

\# Initialize with custom config
ta \= TradingAgentsGraph(debug\=True, config\=config)

\# forward propagate
\_, decision \= ta.propagate("NVDA", "2024-05-10")
print(decision)

> The default configuration uses yfinance for stock price and technical data, and Alpha Vantage for fundamental and news data. For production use or if you encounter rate limits, consider upgrading to Alpha Vantage Premium for more stable and reliable data access. For offline experimentation, there's a local data vendor option that uses our **Tauric TradingDB**, a curated dataset for backtesting, though this is still in development. We're currently refining this dataset and plan to release it soon alongside our upcoming projects. Stay tuned!

You can view the full list of configurations in `tradingagents/default_config.py`.

Contributing
------------

We welcome contributions from the community! Whether it's fixing a bug, improving documentation, or suggesting a new feature, your input helps make this project better. If you are interested in this line of research, please consider joining our open-source financial AI research community Tauric Research.

Citation
--------

Please reference our work if you find _TradingAgents_ provides you with some help :)

```
@misc{xiao2025tradingagentsmultiagentsllmfinancial,
      title={TradingAgents: Multi-Agents LLM Financial Trading Framework}, 
      author={Yijia Xiao and Edward Sun and Di Luo and Wei Wang},
      year={2025},
      eprint={2412.20138},
      archivePrefix={arXiv},
      primaryClass={q-fin.TR},
      url={https://arxiv.org/abs/2412.20138}, 
}
```
