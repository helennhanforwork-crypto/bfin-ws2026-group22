# Kappa Foundation Investment Strategy - BFIN WS2026

## 📌 Project Overview
This repository contains the quantitative models and decision records for the **Kappa Foundation** investment strategy, developed as part of the Investment Finance (BFIN) course at Vietnamese-German University (VGU). 

The objective of this project is to manage an initial fund of $12,000,000 USD to meet mandatory liabilities in 2024 ($2.4M) and 2027 ($3.6M), while maximizing the growth portfolio to maintain a target real purchasing power of $8,000,000 USD by 2030.

## 👥 Team Members - Group 22
* Ngô Thị Hạnh Nhân (103240071)
* Nguyễn Hoàng Thụy (103240156)
* Nguyễn Trần Khánh Linh (103240025)
* Trịnh Hoàng Phương An (103240485)

## 📂 Repository Structure
*   **`Group 22 - BFIN.pdf`**: The official assignment report and Initial Decision Record. It summarizes our asset allocation, valuation assumptions, portfolio strategies, and rebalancing rules.
*   **`data/`**: Directory containing raw datasets (fetched via `yfinance` and Kenneth French Data Library) and processed CSVs (returns, Fama-French factors).
*   **`01_Setup_and_Data.ipynb`**: Handles automated data ingestion, cleaning, and computation of monthly adjusted prices and simple returns.
*   **`02_Bond_Valuation_and_Funding_Risk.ipynb`**: Computes Yield to Maturity (YTM), Macaulay/Modified Duration, and Convexity. It evaluates interest rate shocks and executes the cash-flow matching strategy.
*   **`03_Portfolio_Construction.ipynb`**: Executes a Top-Down investment approach. Includes Sector ETF analysis, Sample Covariance vs. Single-Index Model (SIM) calculations, and Mean-Variance Optimization to find the Maximum Sharpe Ratio.
*   **`04_CAPM_vs_FF3.ipynb`**: Risk and return analysis using the Capital Asset Pricing Model (CAPM) and the Fama-French Three-Factor Model (FF3). 

## ⚙️ Methodology: How We Did It
The foundation's capital is split into two distinct sub-funds using a structured, quantitative approach:

1.  **Liability-Matching Bond Fund (Fixed Income):**
    Instead of simple maturity matching, we implemented a **Minimum-Cost Cash-Flow Matching** strategy. Using linear programming (`scipy.optimize.linprog`), we optimized the holdings of available zero-coupon and coupon bonds to completely immunize the portfolio against interest-rate risk for the 2024 and 2027 liabilities, assuming a highly conservative 0% reinvestment rate.
2.  **Diversified Growth Equity Fund (Portfolio Optimization):**
    For the remaining capital, we utilized a **Top-Down Approach**:
    *   **Sector & Stock Analysis:** Filtered through 8 sector ETFs and selected 11 mega-cap stocks across 5 resilient sectors (Technology, Healthcare, Financials, Energy, Consumer Discretionary).
    *   **Risk Modeling:** To avoid the over-concentration typical of standard Sample Covariance matrices, we employed the **Single-Index Model (SIM)**. 
    *   **Asset Allocation:** Optimized the weights using the Mean-Variance Utility framework (setting risk-aversion $A=3$) to balance growth potential with a strict 15% maximum weight limit per instrument to prevent extreme drawdowns.
3.  **Performance Evaluation:**
    We regressed our final portfolio returns against the **Fama-French 3-Factor (FF3)** model to analyze its structural DNA, confirming a defensive, high-growth exposure (significant negative SMB and HML coefficients) that generated positive historical alpha.