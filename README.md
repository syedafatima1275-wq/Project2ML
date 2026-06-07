# End-to-End Predictive Maintenance MLOps Pipeline 🛠️📊

This repository contains a complete, production-ready MLOps pipeline for equipment failure prediction using **MLflow Tracking, Model Registry, and Version Control**. The project covers the entire machine learning lifecycle—from multi-model experimentation and data scaling to staging validation, production promotion, and zero-downtime version rollback.

---

## 🎯 Project Objectives

- **Experiment Tracking:** Train and evaluate multiple classifiers (Logistic Regression, Random Forest, XGBoost) and log hyperparameters/metrics via MLflow Tracking.
- **Data Pipeline Integrity:** Manage feature scaling distributions across decoupled script architectures using standardized artifact state preservation.
- **Model Registry & Governance:** Version control the champion model and append standard metadata infrastructure (`validation_status`, `team`, `framework`).
- **Production Inference Pipeline:** Serve predictions using live artifacts loaded directly from the MLflow production stage.
- **Continuous Deployment Safety:** Simulate real-world deployment challenges and execute an instant rollback to a stable historical model version.

---

## 🗂️ Core Architecture & Component Flow

The separation of concerns between model development and pipeline deployment is strictly enforced through a persistent artifact framework:

```text
  [ STEP 1: EXPERIMENTATION & TRAINING ]
                    │
         (Logs Metrics & Params) ──> [ MLflow Local Server (Port 5000) ]
                    │
         (Serializes State)      ──> [ scaler.pkl ] (Persistent Feature Boundaries)
                    │
                    ▼
  [ STEP 2: MLFLOW REGISTRY MANAGEMENT ]
                    │
                    ▼
         [ Registered Champion ] ➔ [ Staging Stage ] ➔ [ Production Stage ]
                                                             │
  [ STEP 3: LIVE INFRASTRUCTURE ]                            ▼
         [ Client Sensor Input ] ──(Loads Scaler)──> [ Inference Pipeline ]
                                                             │
         [ Version 2 Hotfix Rollback ] <─────────────────────┘
