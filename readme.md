# Neural Capital — Crash Analysis POC

## Purpose
Reproduce how a Balanced portfolio (60% equities, 30% bonds, 10% cash) performed versus the S&P 500 across major market breakdowns. Produce slide-ready charts and a metrics table for each event.

## What’s included
- `Neural_Capital_Crash_Analysis.ipynb` — Jupyter notebook (main analysis).
- `outputs/per_event_metrics.xlsx` — Excel table with metrics per event and portfolio.
- `outputs/figs/` — PNGs: `{Event}_balanced_vs_spy.png`, `{Event}_drawdown.png`.
- `outputs/*.csv` — timeseries used in the analysis.

## How to run (quick)
1. Create and activate Python virtual env.
2. `pip install -r requirements.txt` (or install the listed packages).
3. `jupyter lab` → open `Neural_Capital_Crash_Analysis.ipynb` → Run All.
4. Find charts and metrics in `outputs/`.

## Key assumptions
- Using **price-only** Close prices (no dividends) for the POC.
- Monthly rebalancing.
- Portfolio mapping: equities = SPY/QQQ/VXUS; bonds = BND/IEF/TIP; cash = SHY; gold = GLD.
- Transaction costs are ignored.

## Notes / Limitations
- Some ETFs don’t have data for older events (e.g., Dot-com era). Notebook will skip events that cannot be simulated with the full portfolio.
- Dividend/total-return adjustment and transaction costs are not included and can change numerical results.

## Next steps
- Add total-return (Adj Close) version.
- Add a simple rule-based “AI-proxy” to demonstrate dynamic protection (e.g., shift out of equities on macro signals).
- Optionally backfill proxies for very old events to cover Dot-com fully.
