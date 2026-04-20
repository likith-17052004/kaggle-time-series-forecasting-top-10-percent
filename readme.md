# 🏆 Kaggle TS Forecasting Solution (Top 5.4%) | Time Series Forecasting Kaggle

> 🔎 **Keywords:** Kaggle TS Forecasting solution, weighted RMSE Kaggle, CatBoost time series, LightGBM forecasting, time series CV, Kaggle forecasting notebook

---

## 📌 TL;DR (Quick Summary)

* 🏁 **Rank:** 53 / 983 (**Top 5.4%**)
* 📊 **Metric:** Weighted RMSE
* 🤖 **Models:** CatBoost (primary) + LightGBM
* 🔥 **Key Idea:** Forward-chaining CV + native categorical handling (CatBoost) + weighted evaluation

---

## 🔗 Competition Link

👉 [https://www.kaggle.com/competitions/ts-forecasting](https://www.kaggle.com/competitions/ts-forecasting)

---

## 📖 Overview

This repository contains my **end-to-end solution for the Kaggle TS Forecasting competition**, focused on handling structured time-series data with categorical variables and weighted evaluation.

Key highlights:

* Custom **weighted RMSE optimization**
* Robust **forward-chaining time series CV**
* Strong performance using **CatBoost + LightGBM**

---

## 🧩 Problem Statement

The goal was to predict future time series values using:

* Historical observations
* Categorical identifiers (code, sub_category, horizon)
* Sample weights

Challenges included:

* Handling **weighted evaluation metric**
* Preventing **data leakage**
* Managing **categorical + temporal interactions**

---

## 🏗️ Solution Pipeline

```
Data → Feature Selection → Forward CV → Model Training → OOF Predictions → Ensembling → Submission
```

---

## 🚀 Approach (Detailed)

### 1️⃣ Data Setup

* Loaded data from parquet files
* Identified:

  * Target: `y_target`
  * Time column: `ts_index`
  * Weight column: `weight`
* Removed non-feature columns (`id`, target, weights)

---

### 2️⃣ Feature Engineering

* Used **raw features + categorical variables**
* Key categorical columns:

  * `code`, `sub_code`, `sub_category`, `horizon`

💡 **Insight:** Letting CatBoost handle categorical encoding directly improved performance significantly.

---

### 3️⃣ Validation Strategy (CRITICAL)

Used **custom forward-chaining splits**:

* Sorted by time index
* Gradually expanded training window
* Ensured strict temporal ordering

This closely simulated real forecasting scenarios and avoided leakage.

---

### 4️⃣ Evaluation Metric

Custom implementation of **Weighted RMSE**:

* Penalizes errors based on importance weights
* Used consistently for validation and model selection

---

### 5️⃣ Models Used

#### 🌲 CatBoost (Primary Model)

* Handles categorical features natively
* Strong performance on structured + mixed data

#### 🌲 LightGBM

* Fast and efficient baseline
* Complementary to CatBoost

---

### 6️⃣ Cross Validation

* **5-fold forward splits**
* Generated:

  * OOF predictions
  * Test predictions

---

### 7️⃣ Ensembling

* Averaged predictions across folds
* Combined CatBoost + LightGBM outputs

---

## 📈 Results

🏁 **Final Rank:** 53 / 983
🏆 **Top:** 5.4%

---

## 💡 Key Learnings

### ✅ What worked

* Proper time-series CV was crucial
* CatBoost handled categorical features effectively
* Weighted RMSE alignment improved leaderboard score

### ❌ What didn’t work

* Ignoring weights led to poor validation
* Random CV caused leakage

---

## 📁 Repository Structure

```
README.md        → Detailed solution explanation  
model.ipynb      → Complete training + inference notebook  
requirements.txt → Project dependencies  
```

📌 **Note:**

* 📊 **Data Source:** The dataset used in this model is available directly on the Kaggle competition page: [https://www.kaggle.com/competitions/ts-forecasting](https://www.kaggle.com/competitions/ts-forecasting) (not stored in this repo)
* Outputs (predictions/submissions) are generated via the notebook

---

## ▶️ Reproducibility

This solution is intended to be run **directly on Kaggle**.

### Steps (Kaggle)
1. Go to the competition page: https://www.kaggle.com/competitions/ts-forecasting  
2. Click **Code → New Notebook**  
3. Upload `model.ipynb` to the notebook  
4. Ensure the competition dataset is attached  
5. Run all cells to reproduce the results and generate submissions

📌 No local setup required.

### (Optional) Run Locally
If you still want to run locally:

```bash
git clone https://github.com/likith-17052004/kaggle-time-series-forecasting-top-10-percent
cd kaggle-time-series-forecasting-top-10-percent
pip install -r requirements.txt
jupyter notebook model.ipynb
```

---

## 🔮 Future Improvements

* Advanced ensembling strategies
* Feature interaction engineering
* Transformer-based time series models

---

## 🙌 Acknowledgements

Thanks to Kaggle and the community.

---

## ⭐ If this helped

Star ⭐ this repo if you found it useful!

---

## 📬 Contact & Collaboration

For any queries, suggestions, or collaboration opportunities, feel free to reach out:

- 📧 **Email:** likith.narakala@gmail.com
- 💼 **LinkedIn:** [Likith Muni Narakala](https://www.linkedin.com/in/likith-muni-narakala-7b525722a/)

Looking forward to connecting! 🚀
