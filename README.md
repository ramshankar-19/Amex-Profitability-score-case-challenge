# Amex Profitability Score — Case Challenge

This repository contains my submission for the Amex Profitability Score case challenge.

## Objective

Build an interpretable and reproducible approach to score customers by expected profitability. The goal is to provide a model and supporting analysis that help prioritize customers for marketing and retention while explaining the drivers of profitability.

## What’s in this repo

- Amex/1st submission.xlsx — the primary deliverable (workbook) containing my analysis and results.
- README.md — this file: high-level summary, how to inspect the submission, and next steps.

If you expect code, notebooks, or data files in addition to the workbook, please let me know and I can add a reproducible pipeline (Python/R notebooks, requirements, and scripts).

## High-level approach

1. Data exploration and quality checks to understand distributions, missingness, and relationships.
2. Feature engineering to convert transaction and account-level signals into predictive features (recency, frequency, monetary, tenure, product usage, etc.).
3. Model selection and validation using cross-validation and out-of-sample testing. Models considered typically include gradient-boosted trees (e.g., XGBoost / LightGBM), regularized linear models, and simple baselines.
4. Explainability and stability checks using feature importance and model-agnostic explainability tools (SHAP or similar) to surface the top drivers of predicted profitability.
5. Business translation: convert model outputs into a customer scoring framework and provide actionable recommendations.

## How to view the submission

Open the workbook at:

Amex/1st submission.xlsx

The workbook contains the analysis, model outputs, and recommendations from my case study. If you’d like the analysis reproduced as executable code (so the steps are fully reproducible and parameterized), I can add a scripts/ or notebooks/ folder with the necessary files.

## Results & recommendations (summary)

- The model identifies a small set of high-signal features that explain most of the model performance (e.g., monetary and behavioral signals).  
- Deploy the scoring model as a batch process to score the customer base periodically and use scores for targeted campaigns.  
- Monitor model drift and re-train on a cadence informed by business changes (monthly/quarterly depending on volume).

(If you want a more detailed results section with metrics, feature lists, and charts, I can extract those from the workbook and add them to this README.)

## Next steps / Reproducibility

If you want this submission to be fully reproducible from raw data, I can:

- Add a requirements.txt and a small conda environment file.
- Add Jupyter notebooks (or Python scripts) that implement the EDA, feature engineering, training, and evaluation pipeline.
- Containerize the pipeline with Docker for portability.

Tell me which format you prefer (notebooks, scripts, or a packaged pipeline) and I’ll add it.

## Author

ramshankar-19

## License

This repository is provided for the case challenge. If you’d like a license added, tell me which one (MIT, Apache-2.0, etc.) and I’ll include it.
