# 🏷️ Application Model

## Information
* **Application Scorecard Model - Notes**: written by Mehul Melta
* **Data and requirements**: in the files 1. Data. and 2. Instituions code
* **Requirements**: Build Application model for loan application approval. The model must have Gini > 0.35 and PSI (Population Stability Index) < 0.02 

**Notebooks:**

* 01: Processing: Data handle (Noise, Outlier, Corr, Feature engineering, WOE, IV..)  + Hyperparemeters tuning (gridsearch, stratifiedkfold..) + Train for Trees, Boosting and Stacking (also: data handle for LR model with dummies)

* 02: Train: LR model (with dummies)

* 03: PSI for model in 01 (the model satisfies requirements)

**Analysis and results**: Work description

## 📌 Overview
An Application Model that scores loan applicants and classifies them by default risk
Requirements: Build Application model for loan application approval. The model must have Gini > 0.35 and PSI (Population Stability Index) < 0.02 

## 📂 Dataset 
* **Original dataset:** 14,000 samples
* **Train/Test/OOT**: sorted by 'disbursement_date', then divide 8/2 for Train/Test and OOT/PSI calc. In Train test samples, split 8/2 for Train/Test
* **Target variable:** FPD10+.  `FPD10+` → 1 = default class, 0 = non-default class
  
### 🔑 Key Features
* **Demographic:** `Age`, `Gender`, `Occupation`, ...
* **Loan:** `Short_Term_Count`, `Mid_Term_Count`, `Long_Term_Count`, `Short_Term_Count_Bank`, `Num_Loans`,...
* **Credit Card:** `Num_CC`, `Num_CC_Bank`,`OUTS_BAL_CC_Current`, `CC_Limit_Total`,..
* **Outstanding Balance:** `OUTS_BAL_LOAN_M1 -> 12`, `OUTS_BAL_CC_M1 -> 12`,`OUTS_BAL_ALL_M1 -> 12`
* **Inquiry:** `ENQ_3M/6M/9M/12M`
* **Relationship:** `Num_Relationship`, `Num_New_Loan_3M/6M/9M/12M`
  
## 🎯 Objectives and Methodology
* Perform EDA: handle N/A, duplicate, outliers, correlation analysis, explore distributions, Imbalanced data..
* Feature Engineering:
  
(1) Trend features (using ALL balance): ['BAL_CHANGE_ALL'] = ['OUTS_BAL_ALL_M1'] - ['OUTS_BAL_ALL_M6']

(2) 'AVG_OUTS_BAL_ALL' = Avg (.._ALL_M1,3,6,12)

(3) Keep only M1,3,6,12 for Loan, CC, All

(4) Income stress = Out bal all m1/mth income

For Credit risk models, a lots of high correlation features (corr > 0.7..) so we try also non linear models (tree, boosting) so that we could keep high-corr features in the models

* Feature Selection metrics/tools: (1) LogReg (with dummies): WOE, IV for LogReg and (2) other models: SHAP, LightGBM 
* Train models: (1) LogReg (with dummies) and (2) other models: LogReg, Random Forest, ExtraTrees, GradBoost, AdaBoost, CatBoost, XGB, LightGBM, Stacking (base learners: LGBM, CAT, XGM; meta learner: LogReg); handle for imbalanced data (class_weight='balanced'; scale_pos_weight for XGB,...)
* Evaluate metrics: (1) LogReg (with dummies):  p-values, Gini, KS; (2) other models: F2-score, Recall, PR AUC, Gini, KS (since False Negative is costly)
* Hyperparameter tuning: Cv gridsearch, stratified k-fold (k=5), scoring (for optimization) = F2 score

## Features selected
<img width="740" height="719" alt="image" src="https://github.com/user-attachments/assets/d46f1dfa-904c-440a-9147-6ec4569dceb8" />

## 🚀 Results

(1) LogReg (with dummies): Gini = 0.3055 -> not good

(2) Other models: 
* Good models: All models are good, except GradBoost, AdaBoost and LogReg. Gini 0.63 - 0.66, KS ~ 0.6, F2 ~ 0.6, Recall ~ 0.6.
  <img width="687" height="593" alt="image" src="https://github.com/user-attachments/assets/940c4dcc-9a87-404c-b358-b8b3bd8ac27d" />


  I choose XGB as the representative model for PSI calc (model/feature drift checking).
  
* PSI on model score: 0.0202 -> stable 
* PSI for individual (numeric) features: most features have small PSI (<0.03); features with high PSI: mth_since _issue_date (3.75), Income stress (0.4), Bal change all (0.3)...
<img width="420" height="322" alt="image" src="https://github.com/user-attachments/assets/86431bbb-be40-40e1-9e12-a7d086933ece" />


## 🚀 Next Steps / Improvements
Possible try:
* SMOTENC (if categorical features are encoded numerically) inside CV pipline



