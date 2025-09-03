## Goal
*    Backtest portfolio strategies.

*    Study asset correlations and diversification.

*    Analyze market shocks (e.g., dotcom crash, GFC, COVID-19).

*    Explore risk-adjusted performance (Sharpe ratio, drawdowns, etc.).

## What the code does

<p>Define universe of assets </p>

* A dictionary maps “friendly” names (e.g., SPY, BTC) to their Yahoo Finance symbols.

* This makes it easy to work with both traditional and crypto assets in one dataset.

<p>Download historical prices </p>

* Using yfinance, the script retrieves adjusted daily close prices for all tickers in one request.

* Dates are set from 1995 to today, ensuring coverage across major financial crises.

<p>Clean and organize data</p>

* Converts Yahoo’s symbols back to the friendly names for readability.

* Ensures a consistent time index, fills forward missing data, and drops rows with all missing values.

<p>Compute daily returns</p>

* Prices are transformed into percentage daily returns, which are the standard input for most portfolio and risk analyses.

