# 📈 AI Finance Assistant – Agentic AI Stock Trading System

An AI-powered stock trading assistant built using **LangChain, Google Gemini, and multiple financial APIs**. The system analyzes stock market data, evaluates technical indicators, retrieves financial news, and makes trading decisions using an autonomous AI agent.

It also integrates **Alpaca Paper Trading** to execute simulated buy and sell orders based on the agent's analysis.

## 🚀 Key Features

### 1. AI-Powered Stock Analysis
- Retrieves current stock prices using Twelve Data.
- Fetches historical stock prices for trend analysis.
- Analyzes market conditions using Google Gemini 2.5 Flash.
- Generates BUY, SELL, or HOLD decisions.
- Provides confidence levels and reasoning.

### 2. Technical Indicator Analysis

**Relative Strength Index (RSI)**
- Calculates 14-period RSI.
- RSI above 70 indicates overbought conditions.
- RSI below 30 indicates oversold conditions.
- RSI between 30 and 70 is treated as the normal range.

**Simple Moving Average (SMA)**
- Calculates 50-day SMA and 200-day SMA.
- Identifies bullish and bearish market trends.
- 50-day SMA above 200-day SMA indicates a bullish signal (Golden Cross).
- 50-day SMA below 200-day SMA indicates a bearish signal (Death Cross).

### 3. Financial News Analysis
- Retrieves the latest five company news headlines.
- Uses Finnhub API to collect news from the previous seven days.
- Evaluates headlines as Positive, Neutral, or Negative through the AI agent.
- Combines news information with technical indicators before making trading decisions.

### 4. Agentic AI Trading
- Built using LangChain's `create_agent`.
- Uses Google Gemini 2.5 Flash as the reasoning model.
- Dynamically invokes tools based on the system instructions.
- Coordinates stock analysis, news retrieval, and trading operations.
- Makes trading decisions based on multiple signals.

### 5. Paper Trading with Alpaca
- Executes simulated market buy and sell orders.
- Checks available buying power and account equity.
- Retrieves existing stock positions.
- Tracks average entry price and unrealized profit or loss.
- Uses Alpaca's paper-trading environment instead of real-money trading.

### 6. Observability with LangSmith
- Integrates LangSmith tracing.
- Tracks AI agent execution.
- Helps inspect tool calls and model interactions.
- Supports debugging and monitoring of the agent workflow.

---

## 🏗️ System Architecture

```text
                USER QUERY
                    |
                    v
           LANGCHAIN AI AGENT
                    |
                    v
           GOOGLE GEMINI 2.5 FLASH
                    |
          +---------+----------+
          |         |          |
          v         v          v
       STOCK     TECHNICAL   FINANCIAL
       DATA      ANALYSIS     NEWS
          |         |          |
          v         v          v
      TwelveData  RSI / SMA  Finnhub
          |         |          |
          +---------+----------+
                    |
                    v
             TRADING ANALYSIS
                    |
                    v
              BUY / SELL / HOLD
                    |
                    v
             TRADING EXECUTION
                    |
                    v
              ALPACA API
                    |
          +---------+----------+
          |                    |
          v                    v
       BUY / SELL         ACCOUNT STATUS
       ORDERS             POSITIONS
          |                    |
          +---------+----------+
                    |
                    v
             LANGSMITH TRACING
```

## 🧠 Agent Tools

The LangChain agent has access to eight custom tools.

| Tool | Description |
|---|---|
| `get_stock_price` | Retrieves the current stock price. |
| `get_price_history` | Fetches the last 10 days of closing prices. |
| `calculate_rsi` | Calculates RSI(14) and identifies market conditions. |
| `get_sma` | Compares 50-day and 200-day moving averages. |
| `get_company_news` | Retrieves the latest five company headlines. |
| `place_order` | Places simulated market buy or sell orders. |
| `get_stocks_owned` | Retrieves existing stock positions and unrealized P/L. |
| `get_balance` | Checks account equity and available buying power. |

## 🔄 Decision-Making Workflow

The agent follows a structured analysis process.

**Step 1: Market Data Collection**

Retrieves current stock prices and recent historical closing prices.

**Step 2: Technical Analysis**

Calculates RSI and compares 50-day and 200-day SMA values.

**Step 3: News Analysis**

Retrieves recent company headlines and evaluates their potential market impact.

**Step 4: Decision Generation**

Combines price movements, technical indicators, and news to generate a trading decision.

**Step 5: Trade Execution**

- BUY with Medium or High confidence: Buy one share.
- SELL with High confidence: Sell one share if the stock is already held.
- HOLD: Do not execute an order.

**Step 6: Portfolio Monitoring**

Checks available buying power, account equity, current positions, and unrealized profit or loss.

## 📊 Sample Analysis Output

```text
STOCK ANALYSIS REPORT: AAPL

DECISION: BUY
CONFIDENCE: Medium

Current Price: $XXX.XX
Recent Trend: Upward

RSI(14): XX.X → Neutral
SMA: Golden Cross → Bullish

News: Positive

Key Headlines:
- Company reports revenue growth.
- Positive business performance update.

Rationale:
Technical indicators suggest a bullish trend,
supported by positive company news.

Risk Note:
Paper trading simulation for educational purposes only.
```

*Illustrative output only; not a live stock recommendation.*

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| LLM | Google Gemini 2.5 Flash |
| Agent Framework | LangChain |
| Agent Creation | LangChain `create_agent` |
| Stock Market Data | Twelve Data API |
| Financial News | Finnhub API |
| Paper Trading | Alpaca API |
| Observability | LangSmith |
| Development Environment | Google Colab |

## 📂 Project Structure

```text
AI-FINANCE-ASSISTANCE/
│
├── AI_FINANCE_ASSISTANCE.ipynb
│
└── README.md
```

## ⚙️ Installation and Setup

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd AI-FINANCE-ASSISTANCE
```

### 2. Install dependencies

```bash
pip install -U langchain langchain-google-genai langsmith requests finnhub-python
```

### 3. Configure API Keys

The notebook uses Google Colab Secrets to securely access API credentials.

Configure the following secrets in Google Colab:

```text
API_KEY
TWELVE_DATA
FINN_HUB_API
ALPACA_KEY
ALPACA_SECRET
LANGSMITH_API
```

### 4. Configure Alpaca Paper Trading

1. Create an Alpaca account.
2. Enable paper trading.
3. Generate paper-trading API credentials.
4. Add the credentials to Google Colab Secrets.
5. Use the paper-trading endpoint:

```python
ALPACA_BASE_URL = "https://paper-api.alpaca.markets"
```

### 5. Configure LangSmith

Set the tracing environment variables:

```python
os.environ["LANGSMITH_TRACING"] = "true"
os.environ["LANGSMITH_API_KEY"] = userdata.get("LANGSMITH_API")
os.environ["LANGSMITH_PROJECT"] = "AI_TRADING_AGENT"
```

### 6. Run the notebook

Open `AI_FINANCE_ASSISTANCE.ipynb` in Google Colab, configure your secrets, and execute the notebook cells in order.

---

## 🔍 Observability with LangSmith

LangSmith is integrated to trace and inspect the AI application.

It helps with:
- Tracking agent execution.
- Inspecting model interactions.
- Monitoring tool calls.
- Debugging agent workflows.
- Understanding execution behavior.

---

## ⚠️ Limitations and Future Improvements

- Implement advanced financial news sentiment analysis using an NLP model.
- Add historical backtesting to evaluate trading strategies.
- Introduce risk management and position-sizing mechanisms.
- Add stop-loss and take-profit strategies.
- Build a Streamlit or React dashboard for portfolio visualization.
- Add explicit trade confirmation before order execution.
- Evaluate trading performance using historical data.

## 🔐 Security

- Store API credentials in Google Colab Secrets.
- Never hardcode or upload API keys.
- Use Alpaca paper-trading credentials.
- Validate order parameters before execution.

## 👨‍💻 Author

**Kondapalli Aakash**

[GitHub Profile](https://github.com/DEVIAAKASH007)

---

⭐ If you find this project interesting, consider giving the repository a star!

**Disclaimer:** This project is developed for educational purposes. Trading decisions are generated by an AI model and are not financial advice. All order execution in this implementation uses Alpaca's paper-trading environment.
