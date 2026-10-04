---
project: TradingAgents
stars: 109628
description: TradingAgents: Multi-Agents LLM Financial Trading Framework
url: https://github.com/TauricResearch/TradingAgents
---

  

  

Deutsch | Español | français | 日本語 | 한국어 | Português | Русский | 中文

* * *

TradingAgents: Multi-Agents LLM Financial Trading Framework
===========================================================

News
----

-   \[2026-10\] **TradingAgents v0.6.0** released with reports saved as one HTML page, a provider per model tier so the managers and analysts can run on different models, past decisions settled for every ticker while the analysts work, and company news read from Yahoo search while Yahoo's news feed is down.
-   \[2026-09\] **TradingAgents v0.5.2** released with parallel analysts for a faster analysis, a CLI that runs without prompts from flags such as `--ticker` and `--date`, the run's settings recorded in every report, and backtests that see only data published by each analysis date.
-   \[2026-09\] **TradingAgents v0.5.1** released with a package layout organised by what each module holds (import paths moved), optional Jev screening of social posts, GPT-6 Sol and Luna as the default models, and fixes to run isolation and SEC EDGAR statements.

Full release notes are in CHANGELOG.md.

Earlier news

-   \[2026-09\] **TradingAgents v0.5.0** released with point-in-time integrity across every dated path, SEC EDGAR fundamentals served as filed, backtesting over a ticker and date grid, portfolio-aware runs, and current model lineups across every provider.
-   \[2026-08\] **TradingAgents v0.4.0** released with look-ahead / point-in-time fixes across FRED macro, social sentiment, and the decision-log memory; clearer decision signals; working CLI checkpoint resume; Trader price grounding; and the GPT-5.6 and GLM-5.3 models.
-   \[2026-07\] **TradingAgents v0.3.1** released with correctness and stability fixes: Alpha Vantage look-ahead filtering, graph-router crash-safety, graph-shape-aware checkpoint resume, working crypto sentiment sources, a configurable LLM retry budget, Bedrock API-key auth, and Claude Sonnet 5 / Fable 5 support.
-   \[2026-06\] **TradingAgents v0.3.0** released with a verified data-access contract, an expanded provider registry (NVIDIA, Kimi, Groq, Mistral, Bedrock, and any OpenAI-compatible endpoint), FRED and Polymarket data vendors, a current-generation model catalog, and a CI gate.
-   \[2026-05\] **TradingAgents v0.2.5** released with the grounded Sentiment Analyst, GPT-5.5 etc. model coverage, Qwen/GLM/MiniMax dual-region support, `TRADINGAGENTS_*` env-var configurability with API-key auto-detection, remote Ollama support, non-US alpha benchmarks, and ticker path-traversal hardening.
-   \[2026-04\] **TradingAgents v0.2.4** released with structured-output agents (Research Manager, Trader, Portfolio Manager), LangGraph checkpoint resume, persistent decision log, DeepSeek/Qwen/GLM/Azure provider support, Docker, and a Windows UTF-8 encoding fix.
-   \[2026-03\] **TradingAgents v0.2.3** released with multi-language support, GPT-5.4 family models, unified model catalog, backtesting date fidelity, and proxy support.
-   \[2026-03\] **TradingAgents v0.2.2** released with GPT-5.4/Gemini 3.1/Claude 4.6 model coverage, five-tier rating scale, OpenAI Responses API, Anthropic effort control, and cross-platform stability.
-   \[2026-02\] **TradingAgents v0.2.0** released with multi-provider LLM support (GPT-5.x, Gemini 3.x, Claude 4.x, Grok 4.x) and improved system architecture.
-   \[2026-01\] **Trading-R1** Technical Report released, with Terminal expected to land soon.

🚀 TradingAgents | ⚡ Installation & CLI | 🎬 Demo | 📦 Package Usage | 🤝 Contributing | 📄 Citation

> 🎉 **TradingAgents** officially released! We have received numerous inquiries about the work, and we would like to express our thanks for the enthusiasm in our community.
> 
> So we decided to fully open-source the framework. Looking forward to building impactful projects with you!

TradingAgents Framework
-----------------------

TradingAgents is a multi-agent trading framework that mirrors the dynamics of real-world trading firms. By deploying specialized LLM-powered agents: from fundamental analysts, sentiment experts, and technical analysts, to trader, risk management team, the platform collaboratively evaluates market conditions and informs trading decisions. Moreover, these agents engage in dynamic discussions to pinpoint the optimal strategy.

> TradingAgents framework is designed for research purposes. Trading performance may vary based on many factors, including the chosen backbone language models, model temperature, trading periods, the quality of data, and other non-deterministic factors. It is not intended as financial, investment, or trading advice.

Our framework decomposes complex trading tasks into specialized roles.

### Analyst Team

-   Fundamentals Analyst: Evaluates company financials and performance metrics, identifying intrinsic values and potential red flags.
-   Sentiment Analyst: Aggregates news headlines, StockTwits, and Reddit chatter into a single sentiment read to gauge short-term market mood.
-   News Analyst: Monitors global news and macroeconomic indicators, interpreting the impact of events on market conditions.
-   Technical Analyst: Utilizes technical indicators (like MACD and RSI) to detect trading patterns and forecast price movements.

The selected analysts work at the same time, each on its own tools, and the research debate starts once all of their reports are in.

### Researcher Team

-   Comprises both bullish and bearish researchers who critically assess the insights provided by the Analyst Team. Through structured debates, they balance potential gains against inherent risks.

### Trader Agent

-   Composes reports from the analysts and researchers to make informed trading decisions, determining the timing and magnitude of trades.

### Risk Management and Portfolio Manager

-   Continuously evaluates portfolio risk by assessing market volatility, liquidity, and other risk factors. The risk management team evaluates and adjusts trading strategies, providing assessment reports to the Portfolio Manager for final decision.
-   The Portfolio Manager approves/rejects the transaction proposal. If approved, the order will be sent to the simulated exchange and executed.

Installation and CLI
--------------------

### Installation

Clone TradingAgents:

git clone https://github.com/TauricResearch/TradingAgents.git
cd TradingAgents

TradingAgents needs Python 3.11 or later. Create a virtual environment in any of your favorite environment managers:

conda create -n tradingagents python=3.13
conda activate tradingagents

Or with uv:

uv venv --python 3.13
source .venv/bin/activate

Install the package and its dependencies (`uv pip install .` with uv):

pip install .

### Docker

Alternatively, run with Docker:

cp .env.example .env  # add your API keys
docker compose run --rm tradingagents

After updating the repository, rebuild the image with `docker compose build`.

Results, reports, the memory log and the cache live in the `tradingagents_data` volume. To keep them in a folder on the host instead, create the folder and point `TRADINGAGENTS_DATA_DIR` at it, in `.env` or the shell: `mkdir -p data && TRADINGAGENTS_DATA_DIR=./data docker compose run --rm tradingagents`.

For local models with Ollama:

docker compose --profile ollama run --rm tradingagents-ollama

### Required APIs

TradingAgents supports multiple LLM providers. Set the API key for your chosen provider:

export OPENAI\_API\_KEY=...          # OpenAI (GPT)
export GOOGLE\_API\_KEY=...          # Google (Gemini)
export ANTHROPIC\_API\_KEY=...       # Anthropic (Claude)
export XAI\_API\_KEY=...             # xAI (Grok)
export DEEPSEEK\_API\_KEY=...        # DeepSeek
export DASHSCOPE\_API\_KEY=...       # Qwen (international, dashscope-intl.aliyuncs.com)
export DASHSCOPE\_CN\_API\_KEY=...    # Qwen (China, dashscope.aliyuncs.com)
export ZHIPU\_API\_KEY=...           # GLM via Z.AI (international)
export ZHIPU\_CN\_API\_KEY=...        # GLM via BigModel (China, open.bigmodel.cn)
export MINIMAX\_API\_KEY=...         # MiniMax (global, api.minimax.io)
export MINIMAX\_CN\_API\_KEY=...      # MiniMax (China, api.minimaxi.com)
export OPENROUTER\_API\_KEY=...      # OpenRouter
export MISTRAL\_API\_KEY=...         # Mistral
export MOONSHOT\_API\_KEY=...        # Kimi (Moonshot)
export GROQ\_API\_KEY=...            # Groq
export NVIDIA\_API\_KEY=...          # NVIDIA NIM
export FRED\_API\_KEY=...            # FRED macro data (free, optional)
export ALPHA\_VANTAGE\_API\_KEY=...   # Alpha Vantage
export TYPESAFE\_API\_KEY=...        # Jev social-post screening (optional)

For Azure OpenAI, copy `.env.enterprise.example` to `.env.enterprise` and fill in your credentials.

For AWS Bedrock, install the extra with `pip install ".[bedrock]"`, set `llm_provider: "bedrock"`, configure AWS credentials (environment variables, `~/.aws/credentials`, or an IAM role) and `AWS_DEFAULT_REGION`, and use a Bedrock model ID, e.g. `us.anthropic.claude-opus-5-5`.

For local models, configure Ollama with `llm_provider: "ollama"`. The default endpoint is `http://localhost:11434/v1`; set `OLLAMA_BASE_URL` to point at a remote `ollama-serve`. Pull models with `ollama pull <name>`, and pick "Custom model ID" in the CLI for any model not listed by default.

For any other OpenAI-compatible server (vLLM, LM Studio, llama.cpp, or a custom relay), use `llm_provider: "openai_compatible"` and set the endpoint via `backend_url` (or `TRADINGAGENTS_LLM_BACKEND_URL`), e.g. `http://localhost:8000/v1` for vLLM or `http://localhost:1234/v1` for LM Studio. The model is whatever your server serves. No key is needed for local servers; set `OPENAI_COMPATIBLE_API_KEY` when the endpoint requires one.

With `TYPESAFE_API_KEY` set, the Sentiment Analyst screens StockTwits and Reddit posts with TypeSafe's Jev before reading them. Posts that are not about the company are dropped, and each source opens with a count of the remaining posts by stance: bullish, bearish, neutral, or unclear. Without the key, posts pass through unscreened. `jev-latest` moves with new releases; set `TYPESAFE_DEFAULT_MODEL` to a versioned ID such as `jev-1.13.0` to hold it fixed across runs. To reach Jev through OpenRouter, put an OpenRouter key in `TYPESAFE_API_KEY` and set `TYPESAFE_BASE_URL=https://openrouter.ai/api`.

Alternatively, copy `.env.example` to `.env` and fill in your keys:

cp .env.example .env

### CLI Usage

Launch the interactive CLI:

tradingagents          # installed command
python -m cli.main     # alternative: run directly from source

You will see a screen where you can select your desired tickers, analysis date, LLM provider, research depth, and more. Your previous run's answers come back as the defaults, so pressing Enter accepts them. The `TRADINGAGENTS_*` variables in `.env` still skip their step entirely.

To run without questions, for a scheduled job or a script, answer the per-run steps with flags and the rest with `TRADINGAGENTS_*` variables:

export TRADINGAGENTS\_LLM\_PROVIDER=openai TRADINGAGENTS\_QUICK\_THINK\_LLM=gpt-6-luna TRADINGAGENTS\_DEEP\_THINK\_LLM=gpt-6-sol
export TRADINGAGENTS\_OUTPUT\_LANGUAGE=English TRADINGAGENTS\_MAX\_DEBATE\_ROUNDS=1 TRADINGAGENTS\_MAX\_RISK\_ROUNDS=1
tradingagents --ticker NVDA --date 2026-09-23 --analysts market,news,fundamentals --save --no-show

Each flag skips only its own question. Run without a terminal, a missing answer stops the run before it starts and names the flag or variable to set.

A saved report also includes `complete_report.html`, the report as one page with its sections listed beside the text, for reading in a browser, on a phone or in print. Answering the save question at the prompt also asks about the page and can open it in your browser; `--no-html` skips it, and so does `ta.save_reports(state, "NVDA", html=False)` from Python.

### Markets and tickers

TradingAgents works with any market Yahoo Finance covers, using the exchange-suffixed ticker. Company identity and the alpha benchmark resolve automatically per market.

-   US: `AAPL`, `SPY`
-   Hong Kong: `0700.HK` · Tokyo: `7203.T` · London: `AZN.L`
-   India: `RELIANCE.NS`, `.BO` · Canada: `.TO` · Australia: `.AX`
-   China A-shares: Shanghai `.SS`, Shenzhen `.SZ` (e.g. `600519.SS` for Kweichow Moutai)
-   Crypto: `BTC-USD`, `ETH-USD`

An interface will appear showing results as they load, letting you track the agent's progress as it runs.

TradingAgents Package
---------------------

### Implementation Details

We built TradingAgents with LangGraph to ensure flexibility and modularity. The framework supports multiple LLM providers: OpenAI, Google, Anthropic, xAI, DeepSeek, Qwen (Alibaba DashScope, international and China endpoints), GLM (Zhipu), MiniMax (global + China), OpenRouter, Ollama for local models, and Azure OpenAI for enterprise.

### Python Usage

To use TradingAgents inside your code, you can import the `tradingagents` module and initialize a `TradingAgentsGraph()` object. The `.propagate()` function will return a decision. You can run `main.py`, here's also a quick example:

from tradingagents.graph.trading\_graph import TradingAgentsGraph
from tradingagents.default\_config import DEFAULT\_CONFIG

ta \= TradingAgentsGraph(debug\=True, config\=DEFAULT\_CONFIG.copy())

\# forward propagate
state, decision \= ta.propagate("NVDA", "2026-09-01")
print(decision)

\# the same report tree the CLI saves, under results\_dir/reports
ta.save\_reports(state, "NVDA")

You can also adjust the default configuration to set your own choice of LLMs, debate rounds, etc.

from tradingagents.graph.trading\_graph import TradingAgentsGraph
from tradingagents.default\_config import DEFAULT\_CONFIG

config \= DEFAULT\_CONFIG.copy()
config\["llm\_provider"\] \= "openai"        \# e.g. openai, google, anthropic, deepseek, groq, ollama; openai\_compatible covers any OpenAI-compatible endpoint (vLLM, LM Studio, llama.cpp, ...)
config\["deep\_think\_llm"\] \= "gpt-6-sol"    \# Model for complex reasoning
config\["quick\_think\_llm"\] \= "gpt-6-luna"   \# Model for quick tasks
config\["max\_debate\_rounds"\] \= 2

ta \= TradingAgentsGraph(debug\=True, config\=config)
\_, decision \= ta.propagate("NVDA", "2026-09-01")
print(decision)

The quick model serves the analysts, researchers, debaters and trader; the deep model serves the research and portfolio managers. Each can run on its own provider, for example the managers on Claude while the rest run on OpenAI:

config\["deep\_think\_provider"\] \= "anthropic"
config\["deep\_think\_llm"\] \= "claude-opus-5-5"

A tier on its own provider uses that provider's key and default endpoint; set `quick_think_backend_url` or `deep_think_backend_url` for a local or relay endpoint. The `TRADINGAGENTS_DEEP_THINK_PROVIDER` and `TRADINGAGENTS_QUICK_THINK_PROVIDER` variables set them for the CLI, together with the tier's model variable.

See `tradingagents/default_config.py` for all configuration options.

### Fundamentals as filed

US company statements come from SEC EDGAR, which records the date every figure was filed. A run dated in the past reads the statements exactly as they stood that day: a fiscal year that has ended but has not been filed yet is not served, and a figure restated later still reads as first reported. Apple's 2008 total assets were filed as $39.6B and restated to $36.2B in 2010, so a run dated in between reads $39.6B. EDGAR needs no account or API key.

Other companies' statements come from Yahoo Finance, which dates a statement by the period it covers rather than by when it was published. A run dated today reads them; a run dated in the past is told they are withheld, since Yahoo cannot say which figures were public by then.

Insider trades are dated by when they happened, not when they were filed, so a run dated in the past is told they are withheld as well.

SEC asks callers to identify themselves and refuses requests that carry no contact address, so a default one is sent. Set your own so SEC can reach you rather than the project:

SEC\_EDGAR\_USER\_AGENT="Your Name your@email.com"

It covers companies that file with the SEC, including foreign companies listed in the US. Anything else, such as Hong Kong or A-share listings, falls through to the next vendor in the chain. EDGAR's machine-readable filings begin in 2009, and a fourth quarter is reported as unavailable rather than derived, because filers publish it only inside the annual figure.

### Current holdings

By default the agents do not know what you hold, so their guidance is written for a reader who applies it to their own position. Pass a portfolio to have the trader, the risk analysts and the portfolio manager work against your actual book.

from tradingagents.portfolio import PortfolioContext

portfolio \= PortfolioContext.model\_validate({
    "cash": 25000.0,
    "currency": "USD",
    "positions": \[{"ticker": "NVDA", "quantity": 120, "average\_price": 150.0}\],
})
\_, decision \= ta.propagate("NVDA", "2026-09-01", portfolio\=portfolio)

The CLI takes the same content as a JSON file: `tradingagents --portfolio my_book.json`.

An empty `positions` list means a flat book, which is different from passing nothing. A run without a portfolio is never treated as flat.

Persistence and Recovery
------------------------

TradingAgents persists two kinds of state across runs.

### Memory log

The memory log is always on. Each completed run appends its decision to `~/.tradingagents/memory/trading_memory.md`. While the analysts of a later run work, TradingAgents settles every logged decision whose holding period has passed: it fetches the realised return (raw, and alpha against the instrument's regional benchmark) and generates a one-paragraph reflection. The Portfolio Manager then reads the most recent decisions for the same ticker plus recent lessons from other tickers, so each analysis carries forward what worked and what didn't. If settling fails, the run goes on and its report says so.

Override the path with `TRADINGAGENTS_MEMORY_LOG_PATH`.

To settle decisions without running an analysis, for a scheduled job, call `ta.settle_all_pending()`; it returns the decisions it settled and any it could not.

### Checkpoint resume

Checkpoint resume is opt-in via `--checkpoint`. When enabled, LangGraph saves state after each node so a crashed or interrupted run resumes from the last successful step instead of starting over. The run view says whether it resumed a saved run or started fresh. Checkpoints are cleared automatically on successful completion.

Per-ticker SQLite databases live at `~/.tradingagents/cache/checkpoints/<TICKER>.db` (override the base with `TRADINGAGENTS_CACHE_DIR`). Use `--clear-checkpoints` to reset all of them before a run.

tradingagents --checkpoint           # enable for this run
tradingagents --clear-checkpoints    # reset before running

config \= DEFAULT\_CONFIG.copy()
config\["checkpoint\_enabled"\] \= True
ta \= TradingAgentsGraph(config\=config)
\_, decision \= ta.propagate("NVDA", "2026-09-01")

Evaluating decisions over time
------------------------------

One run gives one decision, which cannot tell you whether the system decides well. `run_backtest` runs the same pipeline over a grid of tickers and dates, writes to a memory log of its own, and scores the decisions whose holding window has since traded.

from tradingagents.backtest import iter\_grid, run\_backtest, summarize

dates \= iter\_grid("2026-06-01", "2026-08-01", every\_n\_days\=7)
result \= run\_backtest(\["NVDA", "AAPL"\], dates, config, selected\_analysts\=\["market", "news"\])
print(summarize(result).render())

From the CLI:

tradingagents backtest NVDA,AAPL --start 2026-06-01 --end 2026-08-01 --every 7

Each cell is scored on realized alpha against the instrument's regional benchmark, grouped by rating. Your own memory log is never written to, and re-running the same grid with `run_id=result.run_id` skips the cells that already ran, so an interrupted sweep continues where it stopped.

Reproducibility
---------------

TradingAgents is LLM-driven, so two runs of the same ticker and date can differ. This is expected for a research tool built on language models, not a defect. The variation comes from a few distinct sources, and it helps to separate them.

Language model sampling is non-deterministic. Even at a fixed temperature, providers do not guarantee byte-identical output across calls, and reasoning models (the default GPT-6 family, and any thinking-mode model) vary the most because their internal reasoning is itself sampled.

Live data moves. News, StockTwits, and Reddit return different content as time passes, so a run today sees different inputs than a run last week even for the same historical trade date. Pin the analysis date to hold the price and indicator window fixed, but the social and news sources still reflect "now".

To reduce variation you can lower the sampling temperature. Set `temperature` in your config (or `TRADINGAGENTS_TEMPERATURE` in `.env`); lower values make models that honor it more repeatable. The current curated models are reasoning-first and largely ignore temperature, so for tighter reproducibility name a non-reasoning model in your config, or in `TRADINGAGENTS_DEEP_THINK_LLM` and `TRADINGAGENTS_QUICK_THINK_LLM`. Any model ID your provider serves is accepted, whether or not the picker lists it.

config \= DEFAULT\_CONFIG.copy()
config\["llm\_provider"\] \= "openai"
config\["temperature"\] \= 0.0
\# Reasoning models ignore temperature. For tighter reproducibility, name a
\# non-reasoning model in deep\_think\_llm / quick\_think\_llm.

What does not vary anymore: the analyzed company identity is resolved deterministically from the ticker before any agent runs, and the market analyst grounds exact price and indicator claims in a verified data snapshot. Earlier reports of "different companies" or fabricated price levels across runs are addressed by these two mechanisms.

Backtest results are not guaranteed to match any published figure. Returns depend on the model, the temperature, the date range, data quality, and the sampling above. Treat the framework as a research scaffold for studying multi-agent analysis, not as a strategy with a fixed, replicable return.

Contributing
------------

Contributions are welcome: bug fixes, documentation, and feature ideas; past contributions are credited per release in `CHANGELOG.md`.

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
