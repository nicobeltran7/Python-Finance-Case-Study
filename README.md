# Finance Case Study — Multi-Ticker Exploratory

**Objective**  
Turn raw daily prices into **decision-ready views**: price trends, return correlations, and a quick diversification read for a mixed basket vs **S&P 500**.

**Business case (why this exists)**  
A PM/CFO asks, “How are our names moving vs the market, and what actually diversifies us?”  
This repo shows a **fast, reproducible path** from data → returns → correlations → takeaways you can drop into a slide the same day.

---

## Universe & Horizon

- **Tickers shown in the analysis**
  - Trend/returns: `XOM`, `AAPL`, `JPM`, `KO`, `^GSPC`
  - Correlations: `AAPL`, `AMZN`, `GOOGL`, `JPM`, `^GSPC`
- **Dates:** `2021-01-01` → `2024-01-31`
- **Source:** Yahoo Finance via `yfinance` (Stooq fallback optional)

---

## Repository Structure

finance-case-study/
├─ README.md
├─ requirements.txt
├─ .gitignore
├─ notebooks/
│ └─ Finance_case_study.ipynb
├─ data/ # (optional) cached prices
│ └─ .gitkeep
└─ results/ # export screenshots here
├─ 1_share_price_trend.png 
├─ 2_correlation_heatmap.png 
└─ 3_rolling_returns_smooth.png 

## Approach

- **Data sourcing**
  - Pull daily OHLCV with `yfinance`; align calendars and de-duplicate dates.
- **Cleaning & prep**
  - Use **Adj Close** (preferred) or Close → build a wide prices matrix.
  - Sanity checks for missing/duplicate dates (no forward-fill for returns).
- **Returns & risk**
  - Daily % returns, cumulative returns; rolling 20-day volatility (optional).
- **Correlation & diversification**
  - Correlation on daily returns to understand co-movement and diversification.
- **Visualization**
  - Price trend line chart; correlation heatmap; optional smoothed (100-day) returns.
- **Reproducibility**
  - Single notebook; figures saved to `/results`; env pinned via `requirements.txt`.

---

## Results (highlights)

**(1) Share price trend (2021–2024)**  



**(2) Correlation heatmap (daily returns)**  


**What the plots show (from your outputs):**
- **Diversification:** Financials/Staples (e.g., `JPM`, `KO`) move **less** with mega-cap Tech than Tech names move with each other.  
- **Correlations vs S&P 500:** `AAPL` ≈ **0.80**, `AMZN` ≈ **0.71**, `GOOGL` ≈ **0.75**, `JPM` ≈ **0.63**.  
- **Within-Tech:** `AAPL–AMZN` ≈ **0.61**, `AAPL–GOOGL` ≈ **0.66**, `AMZN–GOOGL` ≈ **0.66** (high co-movement).  
- **Lower pairwise with JPM:** `AAPL–JPM` ≈ **0.36**, `AMZN–JPM` ≈ **0.31**, `GOOGL–JPM` ≈ **0.34** → helpful for reducing basket variance.

<details>




---

## Reproduce

### Environment
```bash
pip install -r requirements.txt
# or
pip install pandas matplotlib seaborn yfinance pandas-datareader

## Next Steps

- **Performance table**
  - Compute and export `results/perf_summary.csv` with: CAGR, annualized stdev, max drawdown, and simple Sharpe (rf≈0).
  - Add a small summary snippet to the README once populated.

- **Portfolio view**
  - Compare **equal-weight vs cap-weight** baskets; support monthly/quarterly rebalancing and a transaction-cost toggle.
  - Plot rolling **beta** and **correlation** vs `^GSPC` (36/60-day windows).

- **Productize**
  - Ship a tiny **Streamlit** app to pick tickers/dates and auto-generate the two charts + metrics table.
  - Optional: GitHub Actions job to **refresh figures weekly** and cache raw prices to `/data`.

- **Analysis extensions**
  - Add drawdown curve and recovery times.
  - Include moving-average signals (50/200d), rolling volatility bands, and a simple regime flag.
  - Sector/factor tilt quick view (Tech/Financials/Staples weight and contribution to risk).

---

## Notes

- Prefer **Adj Close** for total-return proxy (split/dividend adjusted).  
- Do **not** forward-fill price gaps before computing returns—this inflates correlation and distorts drawdowns.  
- Correlations are **sample- and frequency-dependent** (daily ≠ weekly/monthly); interpret in context.  
- Yahoo/third-party data can change or be delayed; if a call fails, use the **Stooq fallback** (`pandas-datareader`).  
- Reproducibility: pin dependencies in `requirements.txt` and save figures into `/results` so the README renders consistently.

---

## Disclaimer

This project is for **educational purposes only**.  
Nothing here is investment, legal, or tax advice. Markets involve risk, including loss of principal. Always verify data and methods before making decisions.
