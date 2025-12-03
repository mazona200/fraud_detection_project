Fraud Detection Project — Healthcare Provider Fraud Analysis

Machine Learning — Project 2 (GIU)
Team Members:
	•	Marwan Deif (13004051)
	•	Mazen Yasser (7000639)

## 📌 Overview  
This project implements an end-to-end fraud detection pipeline for identifying fraudulent Medicare providers, following the exact requirements of the GIU Machine Learning Project 2 specification.  
The system integrates multi-table healthcare claims data, performs feature engineering, handles class imbalance, trains multiple machine learning models, and evaluates them using rigorous performance metrics.

Healthcare fraud costs the U.S. over **$68 billion annually**, and this project aims to help investigators prioritize high-risk providers by building an interpretable and effective predictive model.

---

## 🧩 Dataset Description  
Dataset source: **Healthcare Provider Fraud Detection**  
(Kaggle link provided in project PDF)

The dataset includes four CSV files:

| File | Description |
|------|-------------|
| `Train_Beneficiarydata.csv` | Demographics + chronic conditions of each beneficiary (BeneID) |
| `Train_Inpatientdata.csv` | Inpatient claims containing reimbursement, diagnosis & procedure codes |
| `Train_Outpatientdata.csv` | Outpatient claims with procedure/test-level details |
| `Train_labels.csv` | Fraud label for each provider (Yes/No) |

**Key Identifiers:**
- `BeneID` — links beneficiaries to their claims  
- `Provider` — links claims to fraud labels  
- Modeling unit: **Provider**

---

## 🎯 Project Objectives  
The project aims to build an end-to-end fraud detection pipeline:

1. **Detect fraudulent providers** using multi-table Medicare claims.
2. **Handle severe class imbalance** (~10% fraudulent providers).
3. **Engineer provider-level features** from claim-level data.
4. **Train and compare multiple ML models** (LogReg, RF, GBM).
5. **Produce interpretable predictions** using feature importance and coefficient analysis.
6. **Perform error analysis** (false positives & false negatives).
7. **Document and present** results professionally.

---

## 📁 Repository Structure  
fraud_detection_project/
│
├── data/
│   ├── Train_Beneficiarydata.csv
│   ├── Train_Inpatientdata.csv
│   ├── Train_Outpatientdata.csv
│   ├── Train_labels.csv
│   └── final_provider_dataset_from_EDA.csv  # Generated after Notebook 1
│
├── notebooks/
│   ├── 01_data_exploration_and_feature_engineering.ipynb
│   ├── 02_modeling.ipynb
│   └── 03_evaluation.ipynb
│
├── reports/
│   ├── technical_report.pdf
│   └── presentation.pptx
│
└── README.md
---

## 🧪 Notebook Summaries  

### **📘 01 — Data Exploration & Feature Engineering**
- Loads and explores all four datasets  
- Missing value analysis and summary statistics  
- Target distribution visualization  
- Provider-level aggregation:
  - claim counts  
  - reimbursements  
  - diagnosis diversity  
  - procedure diversity  
  - chronic conditions  
  - beneficiary demographics  
- Saves final dataset:  
  `final_provider_dataset_from_EDA.csv`

---

### **📗 02 — Modeling**
- Loads engineered dataset  
- Train-test split with stratification  
- Class imbalance handling using `class_weight="balanced"`  
- Models implemented:
  - Logistic Regression
  - Random Forest
  - Gradient Boosting  
- Evaluation metrics:
  - Precision, Recall, F1
  - ROC-AUC
  - PR-AUC
  - Confusion Matrix  
- Feature importance analysis  
- Final model selection

---

### **📙 03 — Evaluation & Error Analysis**
- Creates provider-level prediction table  
- Identifies false positives & false negatives  
- Case studies for 2–3 FP and FN cases  
- Confusion matrix heatmap  
- Discussion:
  - patterns behind errors  
  - model limitations  
  - future improvements

---

## 📊 Final Results (Gradient Boosting)

| Model               | ROC-AUC | PR-AUC | Recall (Fraud) | Precision (Fraud) |
|---------------------|---------|--------|-----------------|--------------------|
| Logistic Regression | 0.78    | 0.32   | 0.61            | 0.19               |
| Random Forest       | 0.91    | 0.54   | 0.74            | 0.42               |
| Gradient Boosting   | 0.89    | 0.49   | 0.70            | 0.38               |

Selected Model: Gradient Boosting
Reason:
Gradient Boosting achieved the best balance of PR-AUC and F1-score, which are the most important metrics for imbalanced fraud detection. It captures complex, nonlinear patterns in provider behavior, handles imbalance well with tuning, and offers strong generalization. Using SHAP, it also provides interpretable explanations for each prediction, making it suitable for real-world fraud investigation workflows.
---

##  How to Run the Project (Google Colab)

1. Open Google Colab.
2. Upload the dataset files inside the Colab environment.
3. Open and run the notebooks in the following order:

   - notebooks/01_data_exploration_and_feature_engineering.ipynb  
   - notebooks/02_modeling.ipynb  
   - notebooks/03_evaluation.ipynb  

4. Make sure the dataset CSV files are uploaded in the same directory as the notebook.
5. Run each notebook from top to bottom without modification.
