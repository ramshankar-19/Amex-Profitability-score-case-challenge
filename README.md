# American Express Campus Challenge 2026 - Customer Profitability Model

[![Accuracy](https://img.shields.io/badge/Accuracy-0.841-brightgreen.svg)]()
[![Dataset](https://img.shields.io/badge/Dataset-500K_Customers-blue.svg)]()
[![Methodology](https://img.shields.io/badge/Methodology-Deterministic_Finance_Modeling-orange.svg)]()

## 📌 Project Overview
This repository contains my solution for the **American Express Campus Challenge 2026**. The objective was to predict the top 20% most profitable customers from a highly anonymized and masked dataset of 500,000 credit card accounts. 

Instead of relying on black-box machine learning parameter tuning, this solution achieves a top-tier leaderboard score of **0.841** (a 29% improvement over baseline) by engineering a deterministic, business-driven profitability framework grounded in credit card economics and CECL (Current Expected Credit Losses) risk methodologies.

## 🧠 Core Methodology

### 1. The P&L Profitability Equation
The model evaluates trailing 12-month profitability for each customer using a structured formula mapping the 23 anonymized features to real-world financial drivers:

$$ \text{Profitability} = \left[ \text{NII} + \text{NTM} + \text{Fee Income} - \text{ECL} - \text{Benefit Costs} - \text{Servicing Costs} \right] \times \text{Retention Factor} $$

*   **Net Interest Income (NII):** Yield calculated at 42% on revolving debt balances.
*   **Expected Credit Loss (ECL):** Modeled using Basel/CECL frameworks (Probability of Default × Exposure at Default × Loss Given Default), applying a heavily amplified 2.5x risk penalty to actively purge toxic debt from the top 20%.
*   **Net Transaction Margin (NTM):** Calculated assuming a 2.5% interchange fee on categorical spend.
*   **Accrued Rewards Liability:** Shifted rewards costing from trailing raw redemptions to an *expected accrual liability* (5x on travel/lodging, 1x on other categories) to smooth out lumpy redemption behavior and accurately value long-term point hoarders.

### 2. Resolving NMAR Missingness & Multicollinearity
The dataset featured structural Not Missing At Random (NMAR) data—specifically in categorical spend ($f_6-f_{10}$). 
*   **The Problem:** Zero-filling missing categories artificially zeroes out transaction margins, unfairly penalizing high-spending transactors.
*   **The Solution:** Implemented decile-conditioned imputation using Total Spend ($f_5$) as a fallback. If a customer's sub-categories sum to 0, the model falls back to evaluating $f_5$ to rescue masked "Mega-Spenders."
*   **Multicollinearity:** Removed redundant lending line features ($r > 0.90$) to prevent double-counting and stabilize the final scoring coefficients.

## 📊 Behavioral Customer Segmentation
Through deep exploratory data analysis, the dataset was clustered into 7 behavioral archetypes based on debt balance ($f_1$), churn signals ($f_2, f_3$), and default risk ($f_{11}$). The mathematical weights were systematically tested and calibrated to boundary-optimize the Top 20% inclusion of specific clusters:

| Cluster Archetype | Character Profile | Strategy |
| :--- | :--- | :--- |
| **R3: Heavy Clean Revolver** | High balance, near-zero risk. | **Prioritize** (Core NII drivers) |
| **T1: Clean Transactor** | $0 debt, high transaction volume. | **Prioritize** (Rescued via conditional NTM imputation) |
| **R5: Heavy Risky Revolver** | High balance, high risk score, collection calls. | **Purge** (Removed via 2.5x ECL weight + strict retention decay) |
| **R1: Small Clean Revolver** | Modest balances, clean history. | *Neutral* |
| **R4: Heavy Clean + Cancel**| Good customers flashing churn intent. | *Discounted* via Retention Factor |

## 🚀 Results & Impact
*   **Final Public Leaderboard Score:** 0.841
*   **Baseline Improvement:** +29% (over initial linear baseline of 0.65).
*   **Strategic Win:** Successfully closed a 19-point accuracy gap purely through evidence-based hypothesis testing of financial parameters (interest yield, default penalties) rather than stochastic ML tuning.

## 📂 Repository Structure
*   `Amex_R1_Submission_V7_Accrual_NTM.xlsx`: The final submission file containing predictions and the written profitability framework.
*   `profitability_model.py`: The Python script containing the deterministic calculation engine, imputation logic, and ranking algorithms.
*   *(Note: The 500K customer dataset `6a3eb196bc7a3_campus_challenge_r1_data.csv` is excluded from this repository to comply with competition data-sharing rules).*

## ⚙️ How to Run
1. Ensure you have `pandas` and `numpy` installed.
2. Place the competition CSV dataset in the root directory.
3. Run `python profitability_model.py` to calculate financial components, impute missing values, and generate the ranked Excel output.
