[BlackScholes_README.md](https://github.com/user-attachments/files/29403579/BlackScholes_README.md)
# BSM-MODEL-OPTIONS-DASHBOARD# 📈 Black-Scholes Options Pricing Dashboard

> **Author:** Arsh Gulia | FRM Certified | B.A. (Hons.) Business Economics, University of Delhi
> **Domain:** Derivatives · Options Pricing · Greeks · Sensitivity Analysis · Payoff Diagrams

---

## Overview

A fully dynamic **Black-Scholes Options Pricing Dashboard** built entirely in Excel — no macros, no VBA, just 1,222 live formulas. Change any input (stock price, strike, volatility, rate, time) in the Assumptions sheet and every price, Greek, sensitivity table, and payoff diagram updates instantly.

The model prices European Call and Put options on Indian equity (default: ₹2,500 stock), computes all 5 Greeks, and builds a 31×9 sensitivity table replicating the **volatility surface** used by derivatives desks at banks and hedge funds.

---

## Key Results (Default Inputs)

| Parameter | Value |
|-----------|-------|
| Stock Price (S) | ₹2,500 |
| Strike Price (K) | ₹2,500 (At-the-Money) |
| Volatility (σ) | 25% |
| Risk-Free Rate (r) | 6.5% (RBI repo proxy) |
| Time to Expiry (T) | 0.25 years (3 months) |
| Dividend Yield (q) | 1% |

| Output | Call | Put |
|--------|------|-----|
| Option Price | Live formula | Live formula |
| Delta (Δ) | ~0.52 | ~-0.48 |
| Gamma (Γ) | Same for both | Same for both |
| Vega (ν) per 1% vol | Same for both | Same for both |
| Theta (Θ) per day | Negative (time decay) | Negative |
| Rho (ρ) per 1% rate | Positive | Negative |

*All values recalculate when you change inputs.*

---

## Black-Scholes Formulae

```
Call Price  =  S·N(d₁) − K·e^(−rT)·N(d₂)
Put Price   =  K·e^(−rT)·N(−d₂) − S·e^(−qT)·N(−d₁)

d₁  =  [ln(S/K) + (r − q + σ²/2)·T] / (σ·√T)
d₂  =  d₁ − σ·√T
```

### The 5 Greeks

| Greek | Symbol | Measures | Formula |
|-------|--------|----------|---------|
| Delta | Δ | Price sensitivity to stock move | N(d₁) for call |
| Gamma | Γ | Rate of change of Delta | N'(d₁) / (S·σ·√T) |
| Vega | ν | Sensitivity to volatility | S·N'(d₁)·√T ÷ 100 |
| Theta | Θ | Time decay per day | Complex; see sheet |
| Rho | ρ | Sensitivity to interest rate | K·T·e^(−rT)·N(d₂)·0.01 |

---

## Model Structure — 6 Sheets

### Sheet 1 — Dashboard
Cover page with navigation, colour-coding legend, and all Black-Scholes formulae displayed clearly — d₁, d₂, Call, Put, and all 5 Greeks with their interpretations.

### Sheet 2 — Assumptions ← *Start Here*
6 yellow input cells:
- **S** — Current stock price
- **K** — Strike price
- **σ** — Annual volatility
- **r** — Risk-free rate
- **T** — Time to expiry (in years)
- **q** — Dividend yield

All intermediate values shown transparently: d₁, d₂, N(d₁), N(d₂), N'(d₁), discount factor.

### Sheet 3 — Option Pricer
Live pricing output:
- Call and Put prices with intrinsic value, time value, and moneyness label
- All 5 Greeks for both Call and Put with units and interpretations
- **Put-Call Parity verification** — should always show ≈ ₹0.00 difference, confirming model accuracy

### Sheet 4 — Sensitivity Tables
Two large grids:
- **Call price table**: 31 spot prices × 9 volatility levels = 279 combinations
- **Put price table**: same dimensions

This replicates the **vol surface** — the matrix every derivatives desk uses to assess how option value changes with both spot and vol simultaneously. The current spot row (₹2,500) is highlighted in yellow.

### Sheet 5 — Payoff Analysis
P&L at expiry for 8 strategies across 21 spot price scenarios:
- Long Call / Short Call
- Long Put / Short Put
- Long Straddle / Short Straddle
- Bull Spread / Bear Spread

### Sheet 6 — Greeks Deep-Dive
All 5 Greeks calculated at every ₹50 increment from ₹1,500 to ₹3,500 — showing exactly how:
- Delta goes from 0 → 1 as the option moves deep ITM
- Gamma peaks at-the-money and falls away in both directions
- Vega collapses as time to expiry decreases
- Theta accelerates as expiry approaches

---

## How to Use

```
1. Download BlackScholes_Options_Dashboard.xlsx
2. Open in Microsoft Excel or Google Sheets
3. Go to the Assumptions sheet
4. Change the 6 yellow input cells
5. Navigate to any sheet — all values update instantly
```

**To price a specific NSE option:**
- Set S = current Nifty/stock price
- Set K = your chosen strike
- Set σ = implied volatility from NSE option chain
- Set T = days to expiry ÷ 365
- Set r = current RBI repo rate ÷ 100

---

## What the Sensitivity Table Shows

The 31×9 table is the most powerful part of the model. It answers: *"If both the stock price and volatility were different from today, what would this option be worth?"*

Reading **down a column** (fixed vol, changing spot) shows you **Delta intuition** — how much faster the option price changes when in-the-money vs out-of-the-money.

Reading **across a row** (fixed spot, changing vol) shows you **Vega intuition** — a deep out-of-the-money option is far more sensitive to vol changes than an in-the-money one.

This is exactly the analysis a derivatives risk manager runs when assessing a portfolio's sensitivity to a volatility spike (e.g. during market stress).

---

## Put-Call Parity

The model verifies Put-Call Parity on Sheet 3:

```
C + K·e^(−rT)  =  P + S·e^(−qT)
```

The difference should always be ≈ ₹0.00. If it isn't, the model has an error. This is a standard sanity check used in practice to verify option pricing models.

---

## Regulatory Context

Options pricing and Greeks are core to **FRM Part I — Valuation & Risk Models** and **FRM Part II — Market Risk Measurement & Management**:

- **Delta hedging**: Using Delta to construct a market-neutral position
- **Gamma risk**: Why delta hedges need frequent rebalancing
- **Vega risk**: Why options become expensive when volatility spikes (e.g. March 2020)
- **Theta**: Why buying options is a negative carry strategy

Under **Basel III FRTB**, options desks must compute Greeks-based sensitivities for regulatory capital using the **Sensitivity-Based Method (SBM)** — this model is the conceptual foundation for that calculation.

---



---


---


