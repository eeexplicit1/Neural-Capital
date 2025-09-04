# Multi-Asset Portfolio Event Study  

## Goal
This framework provides a **reusable event-study pipeline** for portfolio analysis. With it, a data scientist can:  
- Backtest allocation strategies under stress scenarios.  
- Compare diversified portfolios vs. benchmarks during crises.  
- Quantify risk via drawdowns and recovery times.  
- Generate reproducible reports (tables + charts) for communication.  

The end result is a **historical stress test** of a balanced portfolio, answering the question:  

> *“How resilient is this portfolio compared to the S&P 500 during major financial shocks?”*  

## Overview  
This project downloads historical financial data for a diversified set of assets (stocks, bonds, gold, crypto) and evaluates portfolio performance during major market events. It automates data collection, return calculation, event slicing, metric computation, and visualization.  

## Workflow  

### 1. Data Setup  
- **Assets**: A dictionary (`TICKERS`) maps user-friendly names (e.g., `SPY`, `BTC`) to their Yahoo Finance tickers.  
- **Period**: Data is pulled from **1995-01-01** up to today.  
- **Source**: Prices are downloaded from Yahoo Finance using the [`yfinance`](https://pypi.org/project/yfinance/) package.  

### 2. Data Preparation  
- **Price Cleaning**: Missing values are forward-filled, indices are normalized to trading days, and symbols are renamed for readability.  
- **Return Series**: Daily percentage returns are computed with `pct_change()`.  
- **Portfolio Construction**: Assets are combined into a balanced 60/30/10 allocation (equity/bond/cash) for benchmarking against the S&P 500 (`SPY`).  

### 3. Event Windows  
Key crisis periods are defined, for example:  
- **Dotcom Bubble** (2000–2002)  
- **Global Financial Crisis** (2007–2009)  
- **COVID Crash** (2020)  
- **2022 Rate Hikes**  
- Optional: **Asian Crisis** (1997), **Debt Ceiling** (2011)  

Each event window is used to slice portfolio and benchmark data.  

### 4. Event Analysis  
For each event window:  
1. **Slicing**: Extract portfolio and SPY data only within event dates.  
2. **Normalization**: Start both series at **100** to compare relative performance.  
3. **Metrics Computed**:  
   - CAGR (annualized growth)  
   - Volatility  
   - Maximum Drawdown  
   - Crash Return (from peak to trough)  
   - Recovery Days (time to regain peak)  
   - Event start/end/trough dates  
4. **Visualization**:  
   - **Performance Chart** — portfolio vs. SPY indexed to 100.  
   - **Drawdown Chart** — depth and timing of drawdowns.  

### 5. Output  
- **Charts**: Saved under `outputs/figs/` as PNG files (one performance chart and one drawdown chart per event).  
- **Metrics Table**: Exported to both CSV and Excel (`outputs/per_event_metrics.csv` and `.xlsx`).  
- **Preview**: Prints the first rows of the metrics DataFrame for quick inspection.  

