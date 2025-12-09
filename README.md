##  Insurance Premium Prediction – Classification & Regression Modeling

This project builds a complete machine learning pipeline to estimate a **recommended insurance premium** using both **classification** and **regression** models. The workflow is structured into three main stages:

## 1. Classification: Predicting Whether a Client Will Require an Insurance Payout

A new binary variable **Payout** was created (1 = payout needed, 0 = none), and the following models were trained to classify whether a client would require a payout:

### Models Used
- **Logistic Regression** (baseline)
- **Random Forest Classifier** (GridSearchCV tuned)
- **Gradient Boosting Classifier** (GridSearchCV tuned)

### Performance
All three models performed extremely well, each reaching:

- **97% accuracy**
- **Class 0 recall: 96%**
- **Class 1 recall: 98%**

**Why focus on recall?**  
For an insurance company, **false negatives are costly**—predicting someone *won’t* need a payout when they actually will. High recall minimizes this risk.  
The **Gradient Boosting Classifier** was selected as the final classification model due to its strong recall and tuning flexibility.

## 2. Regression: Predicting the Size of the Insurance Payout

Regression models were trained on clients who required a payout (payout > 0). After one-hot encoding categorical features and splitting into training/testing sets, the following models were evaluated:

### Models Used
- **Polynomial Linear Regression (degrees 1–3)**
- **Random Forest Regressor** (GridSearchCV tuned)
- **Gradient Boosting Regressor** (GridSearchCV tuned)

###  Performance (RMSE)
- **Polynomial Regression (Degree 2):** 203.82  
- **Random Forest Regressor:** 245.89  
- **Gradient Boosting Regressor:** **196.30** *(best overall)*  

The **Gradient Boosting Regressor** was chosen as the final model due to the lowest RMSE and consistent performance.

---

##  3. Final Premium Calculation

The two models work together for new client data:

1. **Classification model** predicts if a payout will be needed.  
2. **Regression model** predicts *how large* that payout will be.  

To compute the premium for a pool of clients, the following formula was used:

###  **Premium Formula**
PREMIUM = AVERAGE PAYOUT AMOUNT * PROBABILITY OF A PAYOUT * LOADING FACTOR. Where a loading factor of 1.2 was used.

Where:
- **Loading Factor = 1.2** (accounts for uncertainty and risk)
- All new client data was carefully one-hot encoded and aligned with training data features before prediction.

The result is a **data-driven recommended insurance premium**, combining probability of payout and expected payout size.

---

## Summary

This project demonstrates:
- End-to-end supervised machine learning workflow  
- Classification & regression modeling  
- Hyperparameter tuning (GridSearchCV)  
- Feature encoding and data preprocessing  
- Practical premium calculation for actuarial applications  

Both final models (Gradient Boosting Classifier & Gradient Boosting Regressor) were retrained on full data and applied to new clients to compute the final recommended insurance premium.
