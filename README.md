# Leveraged Accumulator Analysis

## Overview
This project was completed as the **Final Project for 553.649 Advanced Equity Derivatives (JHU, Fall 2024)** under the supervision of Professor Roza Galeeva.  
It investigates the **Leveraged Stock Accumulator**, a structured financial derivative that allows investors to accumulate shares at a discounted strike price, with leverage and early termination features.  

The analysis covers both **single-stock** and **basket** versions of the product, combining **analytical pricing** and **Monte Carlo simulations** to study valuation, risk, and performance.

---

## Product Description
- **Mechanics**:
  - Buy a fixed number of shares daily at a strike price (discounted from initial spot).  
  - If the stock closes **below strike**, the daily quantity doubles (leverage effect).  
  - If price **hits an upper barrier**, the contract terminates early (knock-out).  

- **Extensions**:
  - Basket Accumulator with 3 underlying assets (AAPL, AMZN, META).  
  - Basket dynamics modeled via correlated **Geometric Brownian Motions (GBM)**:contentReference[oaicite:2]{index=2}.

---

## Methodology
1. **Analytical Pricing**
   - Derived using option decomposition:  
     - Equivalent to a portfolio of **up-and-out barrier calls and puts**.  
   - Closed-form expressions obtained via the **Reflection Principle**.  

2. **Monte Carlo Simulation**
   - Path-dependent payoff simulated using GBM.  
   - **Variance reduction**: antithetic variates.  
   - Convergence analysis confirms stability and alignment with analytical results:contentReference[oaicite:3]{index=3}.

3. **Calibration**
   - Implied volatilities estimated from 1Y ATM options:  
     - AMZN: 33.85%, AAPL: 24.71%, META: 36.83%.  
   - 5-year historical correlations computed (AAPL–AMZN: 0.62, AAPL–META: 0.59, AMZN–META: 0.61):contentReference[oaicite:4]{index=4}.  
   - Risk-free rate: 4.3% (1Y Treasury yield, Dec 2024).  

---

## Results
### Single Asset Accumulator
- **Monte Carlo** (100k paths, AMZN parameters):
  - Mean payoff ≈ **-19.77**  
  - 95% CI ≈ (-61.16, 21.62)  
  - Knock-out rate ≈ 55%  
- **Greeks**:  
  - Δ ≈ 181.6 (MC), 107.7 (Analytical)  
  - Vega ≈ -27,937 (MC), -29,357 (Analytical):contentReference[oaicite:5]{index=5}.  
- **Risk**:  
  - 1% VaR ≈ -23,648; 1% CVaR ≈ -27,570.  

### Basket Accumulator
- Modeled via multi-asset GBM with Cholesky-decomposed correlation.  
- Monte Carlo captures **knock-out dynamics** and diversification effects.  
- Backtesting (2010–2024) shows:  
  - Mean payoff ≈ **512**, Std ≈ 1,759.  
  - Strong left-tail risk during bearish periods (e.g., 2021–2022):contentReference[oaicite:6]{index=6}.  

---

## Historical Backtest
- Rolling 1-year windows (AMZN 2010–2024).  
- Demonstrates strong sensitivity to market regime:  
  - Profitable in bull markets.  
  - Severe drawdowns in bear markets.  
- Confirms **asymmetry of payoff distribution**: heavy left tail:contentReference[oaicite:7]{index=7}.  

---

## Key Takeaways
- The Leveraged Accumulator offers **discounted entry** and **systematic accumulation**, attractive in moderately bullish markets.  
- Significant risks: leveraged downside exposure and heavy tail losses.  
- Basket structure helps diversify risk but cannot eliminate tail exposure.  
- Monte Carlo and analytical pricing frameworks are consistent and mutually validating.  

---

## Files
- `553.649_Final_Project_Accumulator_report.pdf` – Full written report.  
- `553.649_Final_Project_Accumulator_code.ipynb` – Python implementation for analytical pricing, Monte Carlo simulation, Greeks, VaR/CVaR, and backtests.  
- `553.649_Final_Project_Accumulator_code.pdf` – Exported version of the notebook.  

---

## Requirements
- Python 3.x  
- `numpy`, `pandas`, `scipy`, `matplotlib`, `yfinance`
