# Application Model

## Information
**Application Scorecard Model - Notes**: written by Mehul Melta

**Data and requirements**: in the files 1. Data. and 2. Instituions code

**Requirements**: Build Application model for loan application approval. The model must have Gini > 0.35 and PSI (Population Stability Index) < 0.02 

**Notebooks:**

01: Processing: Data handle (Noise, Outlier, Corr, Feature engineering, WOE, IV..)  + Hyperparemeters tuning (gridsearch, stratifiedkfold..) + Train for Trees, Boosting and Stacking (also: data handle for LR model with dummies)

02: Train: LR model (with dummies)

03: PSI for model in 01 (the model satisfies requirements)

**Analysis and results**: Work description

##  Overview
An Application Model that scores loan applicants and classifies them by default risk
Requirements: Build Application model for loan application approval. The model must have Gini > 0.35 and PSI (Population Stability Index) < 0.02 

## Dataset 
**Original dataset:** 14,000 samples
**Train/Test/OOT**: sorted by 'disbursement_date', then divide 8/2 for Train/Test and OOT/PSI calc. In Train test samples, split 8/2 for Train/Test
**Target variable:** FPD10+
* `FPD10+` → 1 = default class, 0 = non-default class
  
### 🔑 Key Features
* **Demographic:** `Age`, `Gender`, `Accupation`, ...
* **Loan:** `Short_Term_Count`, `Mid_Term_Count`, `Long_Term_Count`, `Short_Term_Count_Bank`, `Num_Loans`,...
* **Credit Card:** `Num_CC`, `Num_CC_Bank`,`OUTS_BAL_CC_Current`, `CC_Limit_Total`,..
* **Outstanding Balance:** `OUTS_BAL_LOAN_M1 -> 12`, `OUTS_BAL_CC_M1 -> 12`,`OUTS_BAL_ALL_M1 -> 12`
* **Inquiry:** `ENQ_3M/6M/9M/12M`
* **Relationship:** `Num_Relationship`, `Num_New_Loan_3M/6M/9M/12M`
  
## 🎯 Objectives

## 🛠 Methodology & Tools


## 📊 Key Insights


## 🚀 Results


## 🚀 Next Steps / Improvements




