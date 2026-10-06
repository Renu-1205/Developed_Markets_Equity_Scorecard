# Developed Markets Equity Scorecard

A systematic framework for ranking five developed equity markets - **US, Eurozone, UK, Switzerland, Japan** - on relative 3–6 month performance, built around four independently-tested signal pillars.

Methodology informed by published S&P Global and MSCI scorecard/factor-index research.

---

## Overview

- **Universe:** US, Eurozone, UK, Switzerland, Japan
- **Sample:** 245 synchronized monthly observations, Dec-2005 to Apr-2026
- **Objective:** Rank the five markets each month to identify likely relative outperformers/underperformers over the next 3–6 months
- **Approach:** Four economically distinct signals → cross-sectional standardization → equal-weighted composite score → monthly ranking → historical backtest

---

## Signal Framework

| Pillar | Signal | Construction | Rationale |
|---|---|---|---|
| **Macro** | PMI Level | Current PMI reading, cross-sectional z-score | Captures the pace of business-cycle expansion |
| **Micro** | EPS Momentum | 6-month EPS growth, cross-sectional z-score | Captures the direction of corporate earnings |
| **Valuation** | P/E Reversal | −(6-month P/E change), cross-sectional z-score | Captures whether a market's multiple is cheapening or richening |
| **Technical** | Risk-Adjusted Momentum | 6-month price momentum ÷ 12-month realized volatility | Captures trailing price trend, adjusted for volatility |

Each signal is standardized **cross-sectionally** — every month, a country's raw value is converted to a z-score relative to the other four markets that same month - so all four pillars are directly comparable before combining.

---

## Predictive Power Testing

Each signal was tested independently against forward 3-month and 6-month returns using:

1. **Monthly cross-sectional Information Coefficient** (Spearman rank correlation, computed separately each month)
2. **HAC (Newey-West) significance test** on the mean IC
3. **Top-minus-bottom country spread** (return of the highest-scoring market minus the lowest-scoring market)
4. **HAC significance test** on the spread

### Results (6-month horizon)

| Pillar | Mean IC | p-value | Verdict |
|---|---|---|---|
| Micro (EPS Momentum) | 0.145 | 0.033 | **Significant — strongest signal** |
| Macro (PMI) | 0.076 | 0.233 | Directionally positive, not significant |
| Technical (Risk-Adj. Momentum) | 0.065 | 0.293 | Near-zero at 3M, inconclusive at 6M |
| Valuation (P/E Reversal) | 0.041 | 0.459 | Weakest, least consistent |

Only earnings momentum individually clears conventional significance. The other three pillars are retained for economic completeness and because the **composite score outperforms any single weaker pillar in isolation** (6M composite IC = 0.117, p = 0.058).

---

## Scorecard Construction

```
Composite Score = 0.25 × Macro + 0.25 × Micro + 0.25 × Valuation + 0.25 × Technical
```

Countries are ranked 1 (highest score) to 5 (lowest score) every month. Equal weighting was chosen deliberately over evidence-optimized weighting, given the small cross-section (5 markets) — a data-mined weighting scheme risks overfitting a sample this size.

---

## Backtest

A long-only portfolio (equal-weight base, tilted by composite score via a bounded sigmoid function, one-month execution lag) was simulated from Dec-2006 to Apr-2026 and compared against a naive equal-weight benchmark.

| Metric | Composite-Weighted | Equal-Weight |
|---|---|---|
| Annualized return | 3.84% | 3.67% |
| Sharpe ratio | 0.24 | 0.23 |
| Max drawdown | −56.2% | −56.0% |
| Correlation to benchmark | 0.999 | — |

**What the backtest shows:** a small, statistically borderline ranking edge (6M rank IC = 0.117, p = 0.058; top-bottom spread Sharpe = 0.28, p = 0.089), concentrated at the 6-month horizon and in the second half of the sample (2016–26).

**What it does not show:** a reliable edge in every period. The portfolio beat equal-weight in only 52% of calendar years and slightly underperformed during the 2008–09 crisis. At 0.999 correlation to the benchmark, this is a mild relative tilt, not a differentiated return stream.

---

## Current Ranking (as of 30 April 2026)

| Rank | Country | Composite Score |
|---|---|---|
| 1 | UK | +0.56 |
| 2 | Japan | +0.24 |
| 3 | US | +0.17 |
| 4 | Switzerland | −0.40 |
| 5 | Eurozone | −0.56 |

*Scores and ranks are model output; investment interpretation is analyst judgment layered on top, not a mechanical output of the model itself.*

---



---

## Data Sources

- **Macro/fundamental data:** Bloomberg (PMI, EPS, forward P/E, 2Y yields)
- **Price data:** Yahoo Finance - S&P 500 (US), EWJ (Japan), EZU (Eurozone), EWU (UK), EWL (Switzerland); USD price returns, dividends excluded

---

## Limitations

- Statistical power is inherently limited with only 5 cross-sectional observations per month
- Signal constructions were selected after comparing alternatives on the same sample; results are in-sample and not adjusted for multiple testing
- 3-month horizon evidence is consistently weaker than 6-month across all tests
- Backtest offered no downside protection relative to equal-weight during the 2008–09 crisis

---

## Tech Stack

Python · pandas · NumPy · statsmodels · scipy · matplotlib · yfinance
