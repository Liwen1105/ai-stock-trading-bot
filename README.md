# AI-Driven Stock Trading

An end-to-end machine-learning framework for predicting next-day stock returns, generating trading signals, and evaluating strategy performance against Buy-and-Hold and random baselines.

## Project Overview

This project investigates whether machine-learning models can generate profitable, risk-aware trading signals for ten major technology stocks:

`AAPL` · `MSFT` · `GOOGL` · `AMZN` · `META` · `NVDA` · `TSLA` · `ORCL` · `IBM` · `CRM`

Daily market data from 2019 onward were enriched with technical indicators and company fundamentals. Several regression and tree-based models were trained to predict next-day log returns. Their predictions were converted into Buy, Sell, or Hold signals and evaluated through out-of-sample backtesting.

Financial-news sentiment was also explored using VADER and FinBERT. Because it showed weak predictive performance in this study, sentiment features were excluded from the final modeling stage.

## Objectives

- Build a reproducible financial-data and feature-engineering pipeline.
- Compare linear and non-linear machine-learning models.
- Convert return predictions into actionable trading signals.
- Backtest the AI strategy against meaningful benchmarks.
- Evaluate both returns and downside risk.
- Provide an interactive recommendation interface using Gradio.

## Project Workflow

1. **Data collection** – Gather daily price and volume data from Yahoo Finance and collect company fundamentals.
2. **Data preparation** – Standardize dates, validate the datasets, and calculate log returns.
3. **Feature engineering** – Create momentum, trend, and volatility indicators.
4. **Sentiment analysis** – Test VADER and FinBERT scores derived from financial-news headlines.
5. **Model training** – Predict next-day log returns with multiple machine-learning models.
6. **Signal generation** – Translate predictions into long, cash, or hold decisions.
7. **Backtesting** – Compare the AI strategy with Buy-and-Hold and random trading.
8. **Recommendation interface** – Display configurable Buy, Sell, and Hold recommendations with Gradio.

## Features

The modeling pipeline includes:

- Moving averages and exponential moving averages
- Relative Strength Index (RSI)
- Moving Average Convergence Divergence (MACD)
- Bollinger Bands
- Rolling volatility
- Lagged log returns
- Earnings per share (EPS)
- Price-to-earnings ratio (P/E)
- Revenue and operating cash flow
- Experimental VADER and FinBERT sentiment scores

All predictive features were lagged to reduce the risk of lookahead bias. The target variable was the next-day log return.

## Models

The following models were evaluated:

- Linear Regression
- Ridge Regression
- Lasso Regression
- Random Forest
- XGBoost

Model performance was assessed using mean squared error, R², and directional accuracy. Tree-based methods generally captured non-linear relationships more effectively, although results varied across stocks.

## Trading Strategy

Predicted returns were translated into trading decisions using a threshold-based rule:

| Prediction | Action |
|---|---|
| Greater than **+0.2%** | Enter or maintain a long position |
| Less than **−0.2%** | Exit to cash |
| Between the thresholds | Hold the current position |

The thresholds were designed to reduce unnecessary trading and focus on higher-confidence predictions.

## Evaluation

The AI strategy was compared against:

- **Buy-and-Hold:** continuous exposure to each stock.
- **Random strategy:** a probabilistic control that entered or exited with 50% probability each day.

Performance was measured using:

- **Total Return** – cumulative portfolio growth.
- **Sharpe Ratio** – risk-adjusted performance.
- **Maximum Drawdown** – the largest peak-to-trough decline.

## Key Findings

- Buy-and-Hold produced the strongest long-term absolute return for many of the technology stocks, but it was also exposed to substantial drawdowns.
- The AI strategy was most competitive on high-volatility, momentum-driven stocks such as **NVDA** and **TSLA**.
- In the reported backtest, the AI strategy achieved approximately **695% cumulative return for NVDA** and **1,356% for TSLA**, with Sharpe ratios close to or above 1.0.
- The AI strategy was less effective for several steadier or noisier stocks, including MSFT, META, and ORCL.
- The random baseline generally produced weaker and less consistent risk-adjusted performance.
- Sentiment features did not provide a meaningful predictive improvement and were removed from the final models.

These results suggest that the usefulness of an ML trading strategy depends strongly on the characteristics of the underlying asset. The project does not demonstrate universal outperformance over passive investing.

## Repository Structure

```text
.
├── notebooks/       # Weekly notebooks covering the complete workflow
├── data/            # Data documentation or reproducible data inputs
├── results/         # Charts, metrics, and backtesting outputs
├── app/             # Gradio recommendation application
├── reports/         # Final project report
├── requirements.txt # Python dependencies
└── README.md
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/ai-stock-trading-bot.git
cd ai-stock-trading-bot
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

Activate it on Windows:

```powershell
.venv\Scripts\activate
```

### 3. Install the dependencies

```bash
pip install -r requirements.txt
```

### 4. Explore the analysis

```bash
jupyter notebook
```

Open the notebooks in numerical order to follow the project from data collection through modeling and backtesting.

## Limitations

- Model performance varied substantially across stocks.
- Historical backtesting does not guarantee future performance.
- The reported results may not include every real-world cost, such as transaction fees, bid-ask spreads, slippage, market impact, and taxes.
- Fixed trading thresholds may not generalize across assets or market regimes.
- News sentiment was noisy and poorly aligned with next-day returns.
- Additional walk-forward validation and portfolio-level risk controls would strengthen the evaluation.

## Future Improvements

- Add transaction costs and slippage to the backtest.
- Tune decision thresholds separately for each stock.
- Expand walk-forward and market-regime testing.
- Introduce portfolio construction and position sizing.
- Evaluate sequence models and richer alternative datasets.
- Improve news filtering and sentiment alignment.
- Deploy the Gradio interface as an accessible web application.

## Author

**Liwen (Lydia) Chen**  
University of Toronto

## Disclaimer

This project is for educational and research purposes only. It does not constitute financial advice, and its results should not be interpreted as a recommendation to buy or sell any security.
