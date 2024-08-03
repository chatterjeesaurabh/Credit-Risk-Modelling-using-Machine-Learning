# Credit Risk Modelling using Machine Learning

This project aims to design a machine learning model to assess and predict *credit risk* with customer ranking by analyzing borrower profiles and historical data. 

## Introduction

- **Credit risk** is the probability of a financial loss resulting from a borrower's failure to repay a loan. Lenders can mitigate credit risk by analyzing factors about a borrower's creditworthiness, such as their current debt load and income. Using data driven approach with customer financial historical data features and leveraging machine learning, it is possible to accurately predict credit risk.

- Performed feature selection using statistical tests such as **Chi-Square** and **ANOVA**. Assessed Multicollinearity using **VIF**. Trained on several machine learning models with hyperparameter tuning.


|            | Module                                                       | Contents |
| ---------- | ------------------------------------------------------------ | ------- |
| 1          | [Feature Engineering](https://github.com/chatterjeesaurabh/Credit-Risk-Modelling-using-Machine-Learning/blob/main/Part_1_Feature_Selection.ipynb)                                                 | Cleaning, Feature Selection: Chi-Square test, VIF, ANOVA  |
| 2          | [Model Development](https://github.com/chatterjeesaurabh/Credit-Risk-Modelling-using-Machine-Learning/blob/main/Part_2_Model_Development.ipynb)       | Feature Encoding, Model Training, Hyperparameter Tuning, Evaluation       |



## Datasets

1. **CIBIL Dataset:** [case_study2.xlsx](https://github.com/chatterjeesaurabh/Credit-Risk-Modelling-using-Machine-Learning/blob/main/case_study2.xlsx) : Credit Information Bureau (India) Limited (CIBIL) dataset of 51,336 customers with CIBIL Credit Score and other loan payment history. 
- CIBIL Score Range: 300-900, above 750 is considered good. All banks send the customer's credit and payment history to CIBIL Bureau which determines the CIBIL Credit Score for the customer. 
- Input features (60): Number of days past due (DPD), Time since last missed payment, Credit card utilization, etc.
- Target variable: `Approved_Flag`: Customer Priority Levels - P1, P2, P3, P4. Customer with higher priority are more likely to get loan approval.




2. **Bank Product Dataset:** [case_study1.xlsx](https://github.com/chatterjeesaurabh/Credit-Risk-Modelling-using-Machine-Learning/blob/main/case_study1.xlsx) : Bank products (loan, credit card, etc) hold by the customer. Consists of 25 features.

Total features = 60 + 25 = 85 features \
Feature descriptions: [Features_Target_Description.xlsx](https://github.com/chatterjeesaurabh/Credit-Risk-Modelling-using-Machine-Learning/blob/main/Features_Target_Description.xlsx)


## Method

### Feature Engineering

1. **Handling Missing Values:**
- The 2nd dataset has significant number of NULL values (present as -99999) in many features. Instead of Imputation (mean/median/other), which ultimately is an assumption which may be far from True, following way is used to remove the NULL rows or the whole column.
- If number of NULL rows:
  - < 10,000 : Remove the Rows
  - \> 10,000 : Remove the Column / feature

2. **Categorical Feature Selection:**
- To determine which categorical features are associated with the Target variable (categorical).
- Estimate **Chi-Sqaure** test : get **p-value** for each feature.
- Keep only those features whose **p-value** < **alpha** (0.05).

3. **Numerical Feature Selection:**
- To determine which numerical features are associated with the Target variable (categorical with > 2 features).
- Test to be done : **ANOVA** (since input features are Numerical and Target varible 'Approved_Flag' is categorical with > 2 categories).
- But before performing ANOVA, **Multicollinearity** between the feature variables needs to be determined using: **VIF (Variance Inflation Factor)**.
- Keep only those features which passes the VIF test and then **p-value** < **alpha** (0.05) in the ANOVA test.

**VIF** (*Variance Inflation Factor*):
- Used to identify Multicollinearity among independent features.
- VIF<sub>i</sub> = 1 / (1- R<sub>i</sub><sup>2</sup>), where R<sub>i</sub><sup>2</sup> is the *coefficient of determination**.
- if VIF<sub>i</sub> > 6 : Highly Multicollinear with other features : remove that feature variable.

**ANOVA** (*Analysis of Variance*): It is a statistical technique used to determine whether there are significant differences between the means of three or more groups by analyzing the variation within and between the groups. 

4. Encoding categorical variables and scaling numerical features.


### Model Development

- Random Forest and XGBoost ensemble models were used to predict customer credit risk ranking with four categories: P1, P2, P3 and P4.
- Evaluation Metrics: Accuracy, Precision, Recall, F1 Score.
- Hyperparameter tuning performed using GridSearchCV. Obtained accuracy of 81%.

## Result Analysis: Explain to Business End User

Customer risk ranking categories: P1 (best) to P4 (worse).

**Risk Appetite:** How much the Bank is willing to sell loan.
- Low : not willing to sell too much : <U>Target already achieved</U> : focus only on P1
- High : willing to sell more loans : <U>Target far from being achieved</U> : accept P1, P2, P3 also. 

**Business Interpretation**: P1, P2 covers the risks. P3, P4 can be used to achieve target.

**Feedback Loop / Model Retraining**:
- Update data features, labels and model based on the feedback received from the end business user.


## Contributions
[Saurabh Chatterjee](https://github.com/chatterjeesaurabh) </br>
MTech, Signal Processing and Machine Learning </br>
Indian Institute of Technology (IIT) Kharagpur

