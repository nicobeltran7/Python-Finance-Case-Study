# Finance Case Study — Multi-Ticker Exploratory

**Objective**  
Turn raw daily prices into a small set of **decision-ready views**: price trends, return correlations, and a lightweight portfolio check for a mixed basket (Tech, Financials, Staples) vs **S&P 500**.

**Business case (why this exists)**  
A PM or CFO asks, “How are our names moving vs the market, and what actually diversifies us?”  
This repo shows the **fastest reproducible path** from data → returns → correlations → takeaways that can drop into a slide or dashboard the same day.

---

## Repository Structure

finance-case-study/
├─ README.md
├─ requirements.txt
├─ .gitignore
├─ notebooks/
│ └─ Finance_case_study.ipynb
├─ data/ # (optional) cached price CSVs
│ └─ .gitkeep
└─ results/ # export your screenshots here
├─ 1_share_price_trend.png # ← paste Screenshot (1)
└─ 2_correlation_heatmap.png # ← paste Screenshot (2)

## Universe & Horizon

- **Tickers:** `AAPL`, `AMZN`, `GOOGL`, `JPM`, `KO`, `^GSPC`  
- **Dates:** `2021-01-01` → `2024-01-31`  
- **Source:** Yahoo Finance (`yfinance`) with a Stooq fallback (for blocked/ratelimited calls)

---

## What the notebook does

1. **Ingest**: download OHLCV, align trading days.  
2. **Prep**: build a clean **Close/Adj Close** matrix; handle NAs; sanity checks.  
3. **Returns & Risk**: daily returns, cumulative returns, rolling volatility.  
4. **Correlation**: cross-asset correlation matrix to reason about diversification.  
5. **(Optional) Portfolio**: equal-weight basket vs **^GSPC**.

---

## Results (short highlights)

**(1) Share price trend (2021–2024)**  
![Share price trend](results/1_share_price_trend.png)

**(2) Correlation heatmap (daily returns)**  
![Correlation heatmap](results/2_correlation_heatmap.png)

**Example takeaways (replace with your own after running):**
- Tech names (**AAPL/AMZN/GOOGL**) move together; **KO** and **JPM** reduce basket correlation.  
- Over this window, **AAPL** outran **JPM**; **^GSPC** sits near the basket median risk/return.  
- Highest rolling volatility: **AMZN/GOOGL**; lowest: **KO**.

---

## Reproduce

### Environment
```bash
pip install -r requirements.txt
# or
pip install pandas matplotlib seaborn yfinance pandas-datareader
