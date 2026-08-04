# Anomaly Detection Pipeline Immersion Aluminium Holding Furnace M15

![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-1798c1?style=for-the-badge&logo=xgboost&logoColor=white)

## 📌 Project Overview
This repository contains an end-to-end machine learning and rule-based pipeline for predicting anomalies in an **Immersion Aluminium Holding Furnace (1120 kg/ch)**. Developed in the context of casting operations (HPDC), this project combines physical domain knowledge with machine learning to prevent catastrophic machine failures (e.g., Short Circuits, Thermal Lag, Eutectic Risk).

The pipeline uses a **Hybrid Approach**:
1. **Layer 1 (Rule-Based Interlock):** Physics-informed deterministic logic for immediate safety-critical actions.
2. **Layer 2 (Machine Learning Ensemble):** A weighted ensemble of XGBoost, One-Class SVM (OCSVM), and Local Outlier Factor (LOF) for detecting complex multivariate anomalies.

---

## 📂 Repository Structure

The project is divided into sequentially executed Jupyter Notebooks and a real-time Streamlit dashboard:

* **`Notebook 1 — Data Cleansing & EDA`**
  Handles initial raw data processing. Applies strict domain-knowledge cleansing rules such as time-slicing and full-zero row removal, while intentionally preserving partial-zero rows crucial for anomaly signatures.
* **`Notebook 2 — Feature Engineering & Rule-Based Labeling`**
  Calculates critical physical features like electrical resistance, `delta_temp_1h`, and Eutectic/Liquidus limits based on the Al-Si phase diagram. Applies the Layer 1 Interlock Logic to assign labels and a 4-class severity level (`NORMAL`, `WARNING`, `CRITICAL`, `FATAL/EMERGENCY`).
* **`Notebook 3 — Training, Validation & Testing`**
  Trains the anomaly detection models. Uses OCSVM and LOF for unsupervised density/boundary anomaly detection, and a multi-class XGBoost model trained on the Layer 1 labels. Combines predictions into a final weighted ensemble.
* **`dashboard.py`**
  A Streamlit-based interactive UI replicating the full pipeline for real-time monitoring. Features a live metric dashboard, actionable alerts (What/Where/Why/Recommendation), and dual-mode input (live simulation vs. batch file upload).

---

## ⚙️ Domain Physics & Parameters
This model is heavily grounded in the physical properties of the **Aluminium-Silicon (Al-Si) alloy** and the furnace's electrical specifications:
* **Operating Setpoint:** 650°C ± 10°C
* **Eutectic Point (Total Freezing Risk):** ~577°C
* **Liquidus Point (Mushy Zone Start):** ~615°C
* **Heater Specs:** 2 x 8 kW = 16 kW (Nominal Voltage: 380V ± 10%)

Anomalies are ranked by severity:
* 🔴 **FATAL/EMERGENCY:** Short Circuits, Melt Leak Detect (immediate emergency stop).
* 🟠 **CRITICAL:** Uncontrolled heating, extreme voltage drops, and severe temperature thresholds.
* 🟡 **WARNING:** Thermal lag, sensor faults, approaching liquidus zone.
* 🟢 **NORMAL:** Standard operations.

---

## 🚀 How to Run

### 1. Model Pipeline
Execute the Jupyter notebooks in order:
1. Run `Notebook 1` to generate `cleaned_data.csv`.
2. Run `Notebook 2` to generate `labeled_data.csv`.
3. Run `Notebook 3` to train and export the models (`model_ocsvm.pkl`, `model_lof.pkl`, `model_xgb.pkl`, `scaler.pkl`).

### 2. Streamlit Dashboard
Ensure all model artifacts and the labeled dataset are in the correct paths (or rely on the built-in synthetic demo mode).
```bash
pip install -r requirements.txt
streamlit run dashboard.py
```
*(If running on a platform like Kaggle, you may need to use tunneling tools like `pyngrok` or `localtunnel` as demonstrated in the notebook).*
