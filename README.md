# Customer-Churn-Analysis

## **Objective**
The analysis explores customer churn patterns, focusing on various factors such as payment methods, contract types, tenure, and demographic attributes. The goal is to identify which factors are most strongly associated with higher churn rates to guide customer retention strategies.

##  Key Insights & Findings:

- **Contract Type and Churn:**

    - Customers on month-to-month contracts exhibit the highest churn rate, with 42% of such customers likely to churn.
      Incontrast, customers on one-year and two-year contracts have churn rates of 11% and 3%, respectively.
   - **Implication:** Longer contract periods serve as a strong retention tool, as customers with extended commitments are far less likely to leave.

- **PaymentMethods and Churn:**

    - Customers paying via electronic checks show the highest churn rate at 45%, while those using credit cards, bank transfers, or mailed checks have significantly      lower churn rates, averaging around 15-18%.
    - **Implication:** The convenience, security, and trust issues related to electronic payments might be contributing factors. Encouraging customers to switch to       more stable payment methods could reduce churn.
 
 - **ChurnbyTenure:**

    - Customers with less than one year of tenure are the most likely to churn, with a 50% churn rate. Those with 1-3 years of tenure show a decreasing churn trend       at 35%, while customers who have been with the company for more than three years have a churn rate of just 15%.
     - **Implication:** Engaging customers early in their journey, especially within the first year, is critical for retention.
      
 - **ChurnbyInternet Service Type:**
 
   - Customers using Fiber Optic services show a higher churn rate of 30%, compared to DSL customers with a churn rate of 20%.
   - **Implication:** This could be due to increased competition or dissatisfaction with service quality. Understanding customer satisfaction with service speed and     reliability may help retain fiber optic users.
   
 - **Senior Citizens and Churn:**
 
    - The analysis reveals that senior citizens (aged 65+) have a churn rate of 41%, compared to a 26% churn rate among non-senior citizens.
     - **Implication:** Special retention programs and targeted customer service for senior customers may help reduce churn in this demographic

**Python Code**

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('Customer Churn.csv')
df.head()
```
