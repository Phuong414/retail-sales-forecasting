# retail-sales-forecasting-aus

Forecasting Australian online retail sales using Winters' Exponential Smoothing (WES) — built as a consultant project for the Australian Retailers Association.

**Grade: 90+/100** | Macquarie University — BUSA3015 Business Forecasting (S1 2025)

---

## Project Overview

Developed a time series forecasting model to predict 12 months of Australian online retail turnover (February 2025 – January 2026) using ABS retail trade data. The project compares pre-optimised and post-optimised WES models, and benchmarks WES against Holt's Exponential Smoothing (HES).

**Key result:** Post-optimised WES achieved a MAPE of 2.54% and reduced MSE by 22% (21,389 → 16,707) over the pre-optimised baseline. WES outperformed HES by 94% on MSE (16,707 vs 276,174).

---

## Dataset

- **Source:** [ABS Retail Trade, Australia — February 2025](https://www.abs.gov.au/statistics/industry/retail-and-wholesale-trade/retail-trade-australia/latest-release)
- **Series:** Total online retail — Original & Seasonally Adjusted figures
- **Period used for training:** February 2022 – January 2025 (36 months)
- **Forecast horizon:** February 2025 – January 2026 (12 months out-of-sample)
- **Unit:** AUD millions (monthly estimates)

---

## Methods

### Exercise 1 — Holt's Exponential Smoothing (HES)
Applied to seasonally-adjusted data to capture level and trend.

| Parameter | Pre-optimised | Post-optimised |
|-----------|--------------|----------------|
| Alpha (α) | 0.5 | Solver-optimised |
| Beta (β) | 0.2 | Solver-optimised |

### Exercise 2 — Winters' Exponential Smoothing (WES)
Applied to original (non-adjusted) data to capture level, trend, and seasonality.

| Parameter | Pre-optimised | Post-optimised |
|-----------|--------------|----------------|
| Alpha (α) | 0.5 | Solver-optimised |
| Beta (β) | 0.2 | Solver-optimised |
| Gamma (γ) | 0.1 | Solver-optimised |

**Model type:** Multiplicative WES — chosen because seasonal fluctuations scale proportionally with sales level.

**WES component formulas:**

| Component | Formula |
|-----------|---------|
| Level (Lₜ) | `α × (Yₜ ÷ Sₜ₋ₛ) + (1 – α) × (Lₜ₋₁ + Tₜ₋₁)` |
| Trend (Tₜ) | `β × (Lₜ – Lₜ₋₁) + (1 – β) × Tₜ₋₁` |
| Seasonality (Sₜ) | `γ × (Yₜ ÷ Lₜ) + (1 – γ) × Sₜ₋ₛ` |
| Forecast (Ŷₜ₊ₘ) | `(Lₜ + m × Tₜ) × Sₜ₊ₘ₋ₛ` |

Parameter optimisation was performed using Excel Solver, minimising MSE.

---

## Results

### WES Model Performance

| Model | MAE | MSE | MAPE |
|-------|-----|-----|------|
| Pre-optimised | 112.94 | 21,388.84 | 2.90% |
| Post-optimised | 99.85 | 16,706.77 | 2.54% |

### WES vs HES Benchmark (Post-optimised)

| Model | MAE | MSE |
|-------|-----|-----|
| WES | 99.85 | 16,706.77 |
| HES | 372.05 | 276,173.59 |

WES outperformed HES substantially — confirming that seasonality is the dominant driver of Australian online retail turnover patterns. The December holiday spike is the most critical seasonal effect captured by the model.

---

## Files

```
retail-sales-forecasting-aus/
│
├── README.md
├── Assignment_1.xlsx          # Full Excel workbook with all calculations, Solver setup, and charts
└── report_section_b.pdf       # Written report submitted for Section B (850 words)
```

---

## Tools

- **Excel** — WES/HES model implementation, Solver optimisation, charting
- **Minitab** — Residual diagnostics and ACF analysis
- **ABS Open Data** — Source data

---

## Key Insights

- Australian online retail sales show a clear **upward trend** with a **strong December seasonal peak** driven by holiday shopping.
- The multiplicative WES model is more appropriate than additive because seasonal amplitude grows with the sales level over time.
- Residual analysis (ACF) revealed some remaining autocorrelation at multiple lags, suggesting minor model limitations — likely driven by structural breaks or one-off demand shocks.
- Both WES and HES assume stable historical patterns. Forecasts should be supplemented with **judgmental adjustments** for macroeconomic disruptions (e.g. inflation, consumer sentiment shifts).

---

## Context

This was a university assessment for BUSA3015 — Business Forecasting at Macquarie University Business School (S1 2025). The brief simulated a consulting engagement for the Australian Retailers Association, requiring both quantitative rigour and stakeholder-facing communication of forecasting results.
