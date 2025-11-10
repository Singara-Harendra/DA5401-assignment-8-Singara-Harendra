# 🚲 Ensemble Learning for Complex Regression Modeling on Bike Share Data

### 📘 Course: DA5401 — Assignment 8  
**Topic:** Ensemble Learning for Complex Regression  
**Objective:** To apply and compare Bagging, Boosting, and Stacking techniques for predicting hourly bike rental demand.

---

## 🧠 Project Overview

This project explores how **ensemble learning** methods—**Bagging**, **Boosting**, and **Stacking**—can improve predictive performance compared to single regression models.

The dataset used is the **Bike Sharing Demand** dataset (`hour.csv`), which contains ~17,000 hourly samples of bike rentals influenced by temporal and weather-related factors.

---

## 🧩 Problem Statement

The goal is to predict the **total count of rented bikes (`cnt`)** based on environmental and temporal features.  
This is a **non-linear regression task** with high variability and complex feature interactions.

---

## ⚙️ Implementation Steps

### 🅰️ Part A – Data Preprocessing and Baseline
- Loaded and cleaned the dataset.
- Dropped irrelevant columns: `instant`, `dteday`, `casual`, `registered`.
- Applied **One-Hot Encoding** for categorical features (`season`, `weathersit`, `mnth`, `hr`, `weekday`).
- Implemented:
  - **Decision Tree Regressor** (`max_depth=6`)
  - **Linear Regression**
- Evaluated both using **5-Fold Cross-Validation (CV)** and **Test RMSE**.  
  ✅ *Best Baseline Model:* Linear Regression (RMSE ≈ 100.45)

---

### 🅱️ Part B – Ensemble Techniques for Bias and Variance Reduction
#### 1️⃣ Bagging (Variance Reduction)
- Base learner: Decision Tree Regressor
- Tuned parameters: `n_estimators`, `max_depth`, `min_samples_split`
- Reduced variance moderately  
  ✅ *Bagging RMSE:* 95.01

#### 2️⃣ Boosting (Bias Reduction)
- Model: Gradient Boosting Regressor
- Tuned parameters: `n_estimators`, `learning_rate`, `max_depth`, `subsample`
- Significantly reduced bias  
  ✅ *Boosting RMSE:* 47.70

---

### 🅲 Part C – Stacking for Optimal Performance
- Base learners (Level-0):
  - K-Nearest Neighbors Regressor  
  - Tuned Bagging Regressor  
  - Tuned Gradient Boosting Regressor  
- Meta-learner (Level-1): Ridge Regression (CV-tuned on `alpha`)
- Achieved best bias–variance tradeoff.  
  ✅ *Stacking RMSE:* 46.37

---

### 🅳 Part D – Final Analysis

| Model | Description | RMSE | Observation |
|:--|:--|--:|:--|
| **Linear Regression** | Baseline single model | 100.4459 | Moderate bias and variance |
| **Bagging Regressor** | Variance reduction via averaging | 95.0080 | Slight variance reduction |
| **Gradient Boosting Regressor** | Sequential bias reduction | 47.7000 | Major improvement |
| **Stacking Regressor** | Combines all models with Ridge meta-learner | **46.3724** | Best overall performance |

🧩 **Conclusion:**
> The **Stacking Regressor** achieved the lowest RMSE by optimally combining multiple diverse models.  
> This demonstrates the power of ensemble diversity in balancing bias and variance for complex regression problems.

---
