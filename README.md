# COMM-486-Assignment-3# BTC–FX Gap & Triangular Arbitrage Analysis

Course project for **COMM 486T** at UBC (Commerce).

This project checks whether Bitcoin prices on Coinbase (USD) and NDAX (CAD) imply a tradable USD/CAD discrepancy around Bank of Canada and Federal Reserve announcement windows — and whether that gap survives real trading costs.

## Findings (short)

| Result | Value |
|--------|--------|
| Mean BTC-implied FX gap | **9.8 bps** |
| Max gap | **51.8 bps** |
| BoC window mean gap | **20.6 bps** (42/120 minutes above 25 bps) |
| Fed window mean gap | **−4.7 bps** (8/120 minutes above 25 bps) |
| Naive rule (≥25 bps, CAD 10,000) | **85 trades**, **+$4,438** gross |
| After bid/ask + 50 bps fees + 1-min lag | **−$3,051**, **0** winning trades |
| Cost-aware rule | **0 trades** (best net edge **−8.3 bps**) |

**Conclusion:** Do not trade these gaps. They look like thin-market / stale-quote artifacts on NDAX, not a tradeable edge.

## What’s in this repo

| File | Purpose |
|------|---------|
| `aligned.csv` | 1-minute aligned panel: BTC/USD, BTC/CAD, USD/CAD (Oct 28, 2026, 12:00–20:00 UTC) |
| `supporting_analysis.ipynb` | Step-by-step analysis, backtest, and charts |
| `findings_slides.pdf` | 2-slide summary of conclusions |

## How to run

```bash
pip install pandas matplotlib jupyter
jupyter notebook supporting_analysis.ipynb
```

The notebook loads `aligned.csv` from this repo’s `main` branch.

## Method (high level)

1. Build an implied USD/CAD rate from BTC/CAD ÷ BTC/USD  
2. Compare to observed USD/CAD; express the gap in basis points  
3. Focus on BoC (13:00–15:00 UTC) and Fed (17:30–19:30 UTC) windows  
4. Backtest a ±25 bps trigger with CAD 10,000 notional  
5. Apply no-look-ahead execution (signal at \(t\), fill at \(t+1\)), spreads, and 50 bps fees  

## Data sources

- BTC/USD: Coinbase 1-minute candles  
- BTC/CAD: NDAX midpoint  
- USD/CAD: Dukascopy 1-minute mid  

## Stack

Python · pandas · matplotlib · Jupyter

## Notes

Built with AI assistance (Muse / Cursor). I directed the analysis, verified the results, and wrote the explanations in my own words.

## Suggested GitHub About blurb

> BTC-implied USD/CAD gaps around BoC/Fed windows — cost-aware triangular arbitrage backtest (Python)

**Topics:** `python` `pandas` `finance` `arbitrage` `data-science` `jupyter` `ubc`
