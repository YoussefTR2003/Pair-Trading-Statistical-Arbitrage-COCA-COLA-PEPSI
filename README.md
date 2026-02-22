# Pair Trading Strategy – KO / PEP

This repository implements a **statistical arbitrage (pair trading)** strategy on  
**Coca-Cola (KO)** and **PepsiCo (PEP)** using cointegration and mean-reversion signals.

The strategy trades relative mispricings between two economically related assets rather than forecasting absolute price movements.

---

## 🔍 Strategy Overview

- **Assets**: Coca-Cola (KO) and PepsiCo (PEP)
- **Methodology**:
  - Log-price transformation
  - Cointegration-based spread construction
  - Rolling hedge ratio estimation via OLS
  - Z-score based entry and exit rules
  - Dollar-neutral exposure with dynamic beta scaling
- **Frequency**: Daily
- **Holding logic**: Mean reversion of the spread

---

## 🧠 Core Idea

Let:

\[
S_t = \log(KO_t) - \beta_t \log(PEP_t)
\]

If the spread deviates significantly from its historical mean (high absolute z-score),
the strategy:
- **Shorts the relatively overpriced asset**
- **Buys the relatively underpriced asset**
- Scales exposure using the estimated hedge ratio

The position is closed once the spread reverts toward equilibrium.

---

## ⚙️ Model Components

### 1. Cointegration
- Engle–Granger test on log-prices
- Ensures the spread is stationary and mean-reverting

### 2. Hedge Ratio
- Rolling OLS regression (252 trading days)
- Allows the relationship between assets to evolve over time

### 3. Signal Generation
- Entry when |z-score| > 2.5
- Exit when |z-score| < 0.5

### 4. Risk & PnL
- Dollar-neutral construction
- Exposure normalized by \( 1 + |\beta| \)
- Transaction costs included (0.5 bps per leg)

---

## 📊 Performance Metrics

The script reports:
- Annualized Sharpe Ratio
- CAGR
- Maximum Drawdown
- Equity curve
- Z-score dynamics

> Results are **illustrative** and depend on the sample period and parameters.

---

## 🧪 How to Run

### Install dependencies
```bash
pip install -r requirements.txt
