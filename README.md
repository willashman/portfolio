# Data Science Portfolio

Five end-to-end projects spanning machine learning, experimentation, data engineering, time-series forecasting, and LLM application development. Each project is structured as a standalone repository with reproducible code, documented methodology, and honest evaluation of results.

## Projects

### [01 — Churn Prediction Pipeline](./01-churn-prediction-pipeline/)

A production-oriented churn scoring system built on the IBM Telco Customer Churn dataset (7,043 customers, 27% churn rate). The pipeline covers feature engineering, model training with hyperparameter optimization, model serving, experiment tracking, and drift monitoring.

A logistic regression baseline is compared against an Optuna-tuned XGBoost model under class imbalance, using PR-AUC and F1 as lead metrics rather than accuracy. The baseline was slightly stronger on PR-AUC and F1 (0.669 and 0.637 vs. 0.654 and 0.634), while XGBoost provided a richer platform for interpretability and deployment through SHAP explanations, MLflow tracking, a FastAPI inference endpoint, a Dockerized container, a Streamlit monitoring dashboard, and Population Stability Index drift detection.

**Stack:** Python, XGBoost, Optuna, Scikit-Learn, SHAP, MLflow, FastAPI, Streamlit, Docker

---

### [02 — A/B Testing & Causal Inference](./02-ab-test-causal-inference/)

An experiment analysis of the Cookie Cats mobile game, evaluating whether moving the first difficulty gate from level 30 to level 40 improves player retention. The analysis covers power analysis, sample-ratio mismatch checks, frequentist hypothesis testing, bootstrap confidence intervals, player-segment breakdowns with Bonferroni correction, and a causal inference extension using difference-in-differences on a synthetic regional panel.

The result: moving the gate to level 40 reduced 7-day retention from 19.02% to 18.20% (p = 0.0016), a −0.82 percentage point effect, implying roughly 8,200 fewer retained players per million installs. The recommendation is to keep the gate at level 30.

**Stack:** Python, statsmodels, SciPy, pandas, matplotlib

---

### [03 — Weather Data Pipeline](./03-weather-data-pipeline/)

A modern data stack pipeline that ingests historical weather data from the Open-Meteo API, loads it into DuckDB with idempotent upserts, and transforms it through a dbt project following the staging → intermediate → marts pattern. The mart layer produces a star schema with a daily weather fact table and a station dimension table.

Data quality is enforced through dbt tests covering not-null constraints, uniqueness, referential integrity, accepted value ranges, and a custom singular test for temperature range validation. Orchestration is handled by an Apache Airflow DAG running in Docker.

**Stack:** Python, DuckDB, dbt, Apache Airflow, Docker, Open-Meteo API

---

### [04 — Demand Forecasting](./04-demand-forecasting/)

A model comparison study on the Store Item Demand dataset (~913K rows, 10 stores, 50 items, 5 years of daily sales). Seven models are evaluated under the same expanding-window temporal cross-validation: naive, seasonal naive, 7-day and 30-day moving averages, Prophet, LightGBM with engineered features, and a PyTorch LSTM.

The LSTM achieved the lowest MAPE (23.56 ± 13.15) while LightGBM was the strongest fast model (MAPE 31.59, training in ~1 second vs. ~23 seconds for LSTM). This creates a practical business tradeoff: the LSTM improved accuracy, but LightGBM may be preferable when retraining speed and simpler operations matter. Prophet and LightGBM also provide uncertainty intervals for inventory buffer decisions.

**Stack:** Python, PyTorch, LightGBM, Prophet, statsmodels, Scikit-Learn, pandas, matplotlib

---

### [05 — RAG SEC Filings](./05-rag-sec-filings/)

A retrieval-augmented generation system for querying SEC 10-K filings in natural language. Analysts upload EDGAR filings, and the system ingests, chunks, embeds, retrieves, and generates cited answers grounded in the source text.

Three chunking strategies (fixed-size token windows, sentence-aware packing, and section-based splits aligned to 10-K Item boundaries) are compared on retrieval recall. Section-based chunking achieved 0.94 recall@5 and 1.00 recall@10 on the evaluation set. The system includes input guardrails for prompt injection and off-topic filtering, output validation for citation and numeric faithfulness checking, per-query cost tracking, and a Streamlit interface.

**Stack:** Python, FAISS, sentence-transformers, Groq (Llama 3.1), NLTK, tiktoken, BeautifulSoup, Streamlit

---

## Technical Themes

These projects are designed to demonstrate recurring production concerns, not just modeling:

- **Evaluation honesty** — PR-AUC over accuracy under imbalance, walk-forward CV that never leaks future data, retrieval recall that accounts for labeling artifacts, and limitations sections in every README.
- **Serving and deployment** — FastAPI with Pydantic validation, Docker containers, Streamlit dashboards, and Airflow orchestration.
- **Data quality** — dbt test suites, PSI-based drift monitoring, idempotent database loads, and input/output guardrails.
- **Experiment rigor** — Power analysis, multiple comparison correction, bootstrap intervals, and causal inference extensions beyond naive A/B testing.

## Repository Structure

```
portfolio-projects/
├── 01-churn-prediction-pipeline/
├── 02-ab-test-causal-inference/
├── 03-weather-data-pipeline/
├── 04-demand-forecasting/
├── 05-rag-sec-filings/
└── README.md
```

Each project contains its own README with detailed methodology, results, limitations, and reproduction instructions.

## About

Will Ashman — M.S. Data Science, Ball State University. Background in machine learning, NLP, ETL pipeline development, and stakeholder-facing analytics.

[LinkedIn](https://www.linkedin.com/in/williamashman) · [GitHub](https://github.com/willashman/portfolio)
