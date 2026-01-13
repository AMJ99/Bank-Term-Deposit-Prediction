# Banking Term Deposit Subscription Prediction

## Project Overview

This project aims to predict whether a customer will subscribe to a **bank term deposit** using demographic, behavioral and campaign-related data.  
The dataset is **highly imbalanced**, making careful preprocessing, resampling, and evaluation critical.

The project compares **Artificial Neural Networks (ANN)** with **traditional Machine Learning models**, focusing on **ROC–AUC** as the primary evaluation metric.

---

## Dataset

- **Source:** Kaggle – Bank Dataset Classification  
- **Link:** https://www.kaggle.com/datasets/rashmiranu/banking-dataset-classification

### Files Used
- `BankData/new_train.csv` – Original dataset  
- `Pre_processed.csv` – Dataset after encoding and scaling (Only used as a save-point)

> Note: `BankData/new_test.csv` not used since Subscription (target feature) not included.

---

## Project Workflow

### 1. Data Import
- Dataset already cleaned
- Initial sanity checks performed

### 2. Exploratory Data Analysis (EDA)
- **Non-visual analysis:** class imbalance, feature distributions
- **Visual analysis:** feature distributions, campaign behavior, features vs target
- **Key observations:**
  - Strong class imbalance
  - Campaign behavior is the strongest predictor
  - Low multicollinearity in features

### 3. Data Preprocessing
- Encoding: Binary Encoding / One-Hot Encoding / Label Encoding
- Scaling: StandardScaler / RobustScaler
- Train–test split with stratification

### 4. Handling Class Imbalance
Techniques explored:
- SMOTE
- B-SMOTE (final choice)

Borderline-SMOTE was selected as it improves learning near the decision boundary while reducing noise.

---

## Models Implemented

### Artificial Neural Networks
- **Vanilla ANN**
- **Tuned ANN (Keras Tuner)**
  - Tuned layers, neurons, dropout, learning rate
  - Early stopping applied
  - Optimization metric: ROC–AUC

### Machine Learning Models
- Logistic Regression
- Random Forest
- XGBoost  
(All models tuned using RandomizedSearchCV)

---

## Model Evaluation

### Metrics Used
- ROC–AUC (primary metric due to imbalance)
- Accuracy
- Confusion Matrix
- Classification Report

### Model Comparison

| Model | Accuracy | ROC–AUC |
|------|---------|--------|
| Logistic Regression | 0.813 | 0.881 |
| Random Forest | 0.894 | 0.905 |
| XGBoost | **0.895** | **0.915** |
| Vanilla ANN | 0.839 | 0.893 |
| Tuned ANN | 0.863 | 0.900 |

---

## Key Conclusions

### How should marketing campaigns be executed?
- Campaign behavior is the strongest driver of subscription
- Longer call duration and recent follow-ups increase conversion
- Excessive contact attempts reduce success (diminishing returns)

### Who should the bank target?
- Moderate demographic influence
- Higher conversion among:
  - Customers aged 25–45
  - Students and retirees
  - Higher education levels
  - Single customers

### How and when should campaigns be run?
- Cellular communication outperforms telephone calls
- Higher success in December, March, September, and October

### What can be deprioritized?
- Loan status
- Day of the week

---

## Final Conclusion

- Tuned ANN significantly improved minority class prediction over the baseline ANN
- XGBoost achieved the highest ROC–AUC overall
- ANN offers flexibility for future tuning and deployment
- Structured data makes traditional ML models highly effective

---

## Recommendations & Future Scope

- Use embedding layers in ANN for encoded categorical features
- Experiment with ADASYN for imbalance handling
- Perform deeper feature engineering on campaign behavior
- Explore cost-sensitive learning and ensemble approaches

---

## How to Run the Project

1. Clone the repository:  
git clone https://github.com/AMJ99/Bank-Term-Deposit-Prediction  
cd Bank-Term-Deposit-Prediction  

2. Install dependencies:  
pip install -r requirements.txt  

3. Run the notebook:  
Open Bank_Deposit_Classification.ipynb in Jupyter Notebook and execute all cells.






