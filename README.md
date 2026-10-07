# Predictive Modeling of Material Take-Off (MTO) Overrun Risks in Brownfield EPC Projects

[![Python 3.10](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![LightGBM](https://img.shields.io/badge/Model-LightGBM-success.svg)](https://lightgbm.readthedocs.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **A Dual-Task Machine Learning Approach to Quantifying MTO Growth for Proactive Cost Control in Brownfield Oil & Gas Revamps.**  
> *Capstone Project in partial fulfillment of the Postgraduate Diploma in Artificial Intelligence and Machine Learning, Asian Institute of Management (AIM).*

---

## 📌 Executive Summary & Problem Overview

In the Engineering, Procurement, and Construction (EPC) oil and gas industry, brownfield revamps face significant capital expenditure volatility due to unexpected Material Take-Off (MTO) volume growth. Standard industry estimation relies on arbitrary, flat 10%–15% contingency markups that treat standard utility piping identically to high-pressure, severe-temperature, or toxic exotic alloy circuits.

This repository implements an end-to-end machine learning pipeline that transforms early Front-End Engineering Design (FEED) parameters into predictive risk intelligence:
1. **Task 1: Classification (Risk Flagging):** Flags high-risk piping subsystems likely to exceed a 15% material overrun.
2. **Task 2: Regression (Growth Quantification):** Forecasts exact percentage material volume growth to replace blanket heuristics with dynamic, risk-adjusted buffers.

---

## 📊 Key Results & Benchmarks

All models were evaluated under a **5-Fold Group K-Fold cross-validation strategy grouped strictly by `Project_ID`** to ensure zero data leakage across brownfield facilities.

### Task 1: Classification Benchmark (>15% Overrun)
| Model Architecture | Cross-Validation | PR-AUC Score | Status |
| :--- | :--- | :--- | :--- |
| **LightGBM Classifier** | **5-Fold Group K-Fold** | **0.9741** | **Champion** |
| Logistic Regression | 5-Fold Group K-Fold | 0.9719 | Linear Baseline |
| XGBoost Classifier | 5-Fold Group K-Fold | 0.9703 | Candidate |
| Random Forest Classifier | 5-Fold Group K-Fold | 0.9668 | Candidate |

### Task 2: Regression Benchmark (Exact % Growth)
| Regressor Architecture | Cross-Validation | RMSE (%) | $\Delta$ RMSE | Status |
| :--- | :--- | :--- | :--- | :--- |
| **LightGBM Regressor** | **5-Fold Group K-Fold** | **3.5090%** | **-0.2889%** | **Champion** |
| XGBoost Regressor | 5-Fold Group K-Fold | 3.7176% | -0.0803% | Candidate |
| Random Forest Regressor | 5-Fold Group K-Fold | 3.7756% | -0.0223% | Candidate |
| Ridge Regression | 5-Fold Group K-Fold | 3.7979% | 0.0000% | Baseline |

### Commercial Impact
Narrows material volume uncertainty from $\pm 15\%$ down to an empirical $\pm 3.5\%$ band, **releasing $1.6M to $2.3M in trapped working capital** per $20M piping procurement package while preventing costly emergency air-freight re-orders.

---

## 🏗️ Repository Architecture

```text
├── data/
│   └── synthetic_brownfield_mto_data.csv  # 8,500-record engineered brownfield dataset
├── models/                                # Serialized production artifacts (.pkl)
│   ├── lightgbm_classifier.pkl
│   ├── lightgbm_regressor.pkl
│   └── standard_scaler.pkl
├── notebooks/                             # Reproducible step-by-step Jupyter notebooks
│   ├── 01_Data_Generation_and_Sanitization.ipynb
│   ├── 02_Data_Preprocessing_and_EDA.ipynb
│   ├── 03_Model_Training_and_Cross_Validation.ipynb
│   ├── 04_Model_Explainability_and_Fairness_Audit.ipynb
│   └── Technical_Deck_Slides.ipynb
├── presentations/                         # Final capstone slide decks
│   ├── EPC_Executive_Deck.pptx            # Business-facing presentation
│   └── Technical_Deck_Slides.slides.html  # Interactive technical presentation
├── reports/                               # Final Capstone Project Report
│   └── Predictive_Modeling_of_MTO_Overrun_Risks_Villanueva.pdf
├── src/                                   # Application and pipeline scripts
│   ├── app.py                             # Interactive Streamlit decision-support app
│   └── generate_business_deck.py          # PowerPoint deck generator
├── requirements.txt                       # Environment dependency manifest
└── README.md