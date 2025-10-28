# Predicting Seasonal Vaccine Uptake Using Machine Learning and Explainable AI (XAI)
**University of Hertfordshire — HackTheDataUH25 (Group 5)**  
MSc Data Science (7PAM2015 – Research Methods)  
**Supervisor:** Pedro Carrilho  
22nd October 2025  

---

## 📘 Project Overview
This notebook presents our group’s end-to-end workflow for predicting whether an individual received the **seasonal flu vaccine** using demographic, behavioural, and opinion-based data.  

We combine **advanced preprocessing**, **H2O AutoML modeling**, and **Explainable AI (XAI)** techniques to deliver both high accuracy and model transparency.  
Our focus is not only *who* gets vaccinated, but *why* — identifying the behavioural and socio-economic factors that drive uptake.

---

## 🎯 Objectives
- Predict the target variable `seasonal_vaccine` (1 = Vaccinated, 0 = Not Vaccinated).  
- Perform Exploratory Data Analysis (EDA) to uncover data patterns and correlations.  
- Apply robust preprocessing:  
  - Missing-value imputation (MICE – Bayesian Ridge)  
  - Encoding (Ordinal + One-Hot)  
  - Scaling (Yeo-Johnson + StandardScaler)  
- Train and compare multiple ML models using **H2O AutoML** (F1 as primary metric).  
- Interpret results via **feature importance (varimp)** for explainability.

---

## 📊 Dataset Summary
| Property | Description |
|-----------|-------------|
| **Source** | HackTheDataUH25 Challenge Dataset (adapted from H1N1/Seasonal Vaccine dataset) |
| **Rows** | 4 756 respondents |
| **Features** | 31 attributes |
| **Target Variable** | `seasonal_vaccine` → Binary (1 = Vaccinated, 0 = Not Vaccinated) |
| **Data Types** | 19 numeric, 10 categorical, 2 ID columns |
| **Missing Values** | Up to 48 % in some columns (`employment_sector`, `health_insurance`) |

---

## 🧹 Data Preprocessing Pipeline
1. **Imputation (MICE – Bayesian Ridge)**  
   - Handles multivariate missing data using predictive relationships among columns.  
2. **Encoding of Categorical Variables**  
   - Ordinal → for ordered factors (e.g., flu concern, flu knowledge)  
   - One-Hot → for nominal features (e.g., age_group, education, race)  
3. **Feature Scaling & Normalization**  
   - Yeo-Johnson Transform → handles positive + zero values  
   - StandardScaler → zero-mean unit-variance distribution  
4. **Validation Split** = 80 % training / 20 % validation  

---

## ⚙️ Model Training with H2O AutoML
| Parameter | Setting | Purpose |
|------------|----------|---------|
| `max_models` | 25 | Train up to 25 candidate models |
| `nfolds` | 5 | Cross-validation for stability |
| `balance_classes` | True | Compensate class imbalance |
| `sort_metric` | F1 | Optimise precision + recall |
| `max_runtime_secs` | 900 (15 min) | Hackathon time limit |

### Top 5 Models by F1 Score
| Rank | Algorithm | F1 (Valid) | AUC | LogLoss |
|------|------------|------------|-----|----------|
| 1 | **GBM** | 0.814 | 0.872 | 0.465 |
| 2 | XGBoost | 0.812 | 0.868 | 0.458 |
| 3 | XGBoost (Grid) | 0.809 | 0.868 | 0.454 |
| 4 | Deep Learning | 0.788 | 0.846 | 0.500 |
| 5 | Deep Learning (Grid) | 0.780 | 0.830 | 0.561 |

---

## 🔍 Explainable AI (Feature Importance)
Feature importances were extracted using `model.varimp()` from H2O for the top models.  

**Top Predictors**
1. `health_insurance` → Insured individuals vaccinate more often.  
2. `doctor_recc_seasonal` → Doctor’s advice is a strong motivator.  
3. `opinion_seas_vacc_effective` → Belief in vaccine effectiveness boosts uptake.  
4. `flu_knowledge` → Awareness improves preventive behaviour.  
5. `opinion_seas_risk` → Higher risk perception correlates with vaccination.  

**Visualization:** Cross-model heatmap comparing normalized feature importance (DeepLearning, GBM, XGBoost).

---

## 📈 Results and Discussion
- **Best Model:** GBM (F1 = 0.814, AUC = 0.872).  
- **Accuracy:** ≈ 77 %.  
- Tree-based models outperformed Deep Learning on tabular survey data.  
- Healthcare access and doctor recommendation most influential factors.  
- High interpretability confirmed through consistent varimp patterns.  

---

## 🚀 Future Work
- Integrate **SHAP Explainability** for feature-level interpretation.  
- Experiment with **Stacked Ensembles** for greater accuracy.  
- Extend to **real-time vaccination datasets** for deployment.  
- Develop an interactive **dashboard / web app** for public health use.  

---

## 👥 Team Members
| Role | Member |
|------|---------|
| Team Lead / Coordinator | Srikar Charan |
| EDA & Data Cleaning | Yalamati Lokesh, Shaik Sony |
| Feature Engineering & Imputation | Raghava Reddy Kudumula, Boddupally Raghuvaran |
| Model Training & AutoML | Vinnakota Raviteja, Sharath Reddy Thadisna |
| Explainable AI & Visualization | T. Shrijith, Biradar Karan |
| Documentation & Presentation | All Members |

---

## 🔗 Resources
- 📓 https://colab.research.google.com/github/HackTheDataUH25/data_science_challenge_2025/blob/main/Hackathon_Challenge.ipynb
- 💾  https://github.com/HackTheDataUH25/data_science_challenge_2025 
- 🧑‍🏫 Supervisor: Pedro Carrilho  
- 🏫 University of Hertfordshire  

---

## 🏆 Acknowledgements
We thank **Mr. Pedro Carrilho** for his guidance and the HackTheDataUH25 organisers for this learning opportunity.  

---

## 📜 License
Released under the **MIT License** — free for educational and research use with citation.  

---

> 💡 **Tip:** Run this notebook sequentially to reproduce data preprocessing, H2O AutoML training, and XAI visualizations.
