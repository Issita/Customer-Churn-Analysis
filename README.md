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

```python
df.info()
```

**Replacing blanks with 0 as tenure is 0 and no total charges are recorded and converted the datatype of TotalCharges**
```python
df['TotalCharges'] = df['TotalCharges'].replace(' ','0')
df['TotalCharges'] = df['TotalCharges'].astype('float')
```

```python
df.info()
```
**Checking the dataset - any null value present in the dataset or not**
```python
df.isnull().sum().sum()
```

```python
df.describe()
```
**Checking the primery key have null value present or not**
```python
df['customerID'].duplicated().sum()
```
**converted 0 and 1 values of senior citizen to yes/no to make it easier to understand**
```python
def conv(value):
    if value == 1:
        return "yes"
    else:
        return "no"

df['SeniorCitizen'] = df["SeniorCitizen"].apply(conv)
```

```python
df.head()
```

```python
ax=sns.countplot(x='Churn',data=df)

ax.bar_label(ax.containers[0])
plt.title('Count of customer by Churn')
plt.show()
```
![](https://github.com/Issita/Customer-Churn-Analysis/blob/main/Count%20of%20customer%20by%20Churn.png)
```python
plt.figure(figsize=(3,4))
gb = df.groupby('Churn').agg({'Churn':'count'})
plt.pie(gb['Churn'],labels=gb.index, autopct="%1.2f%%")
plt.title('Percentage of churned customer',fontsize = 10)
plt.show()
```
![](https://github.com/Issita/Customer-Churn-Analysis/blob/main/Percentage%20of%20churned%20customer.png)
**from the given pie chart we can conclude that 26.54% of our customers have churned out.**
```python
plt.figure(figsize=(3,4))
sns.countplot(x='gender',data=df, hue='Churn')
plt.title('Churn by gender')
plt.show()
```

```python
plt.figure(figsize=(3,4))
ax=sns.countplot(x='SeniorCitizen',data=df, hue='Churn')
ax.bar_label(ax.containers[0])
ax.bar_label(ax.containers[1])
plt.title('Churn by SeniorCitizen')
plt.show()
```

```python
total_counts = df.groupby('SeniorCitizen')['Churn'].value_counts(normalize=True).unstack() * 100

# Plot
fig, ax = plt.subplots(figsize=(4, 4))  # Adjust figsize for better visualization

# Plot the bars
total_counts.plot(kind='bar', stacked=True, ax=ax, color=['#1f77b4', '#ff7f0e'])  # Customize colors if desired

# Add percentage labels on the bars
for p in ax.patches:
    width, height = p.get_width(), p.get_height()
    x, y = p.get_xy()
    ax.text(x + width / 2, y + height / 2, f'{height:.1f}%', ha='center', va='center')

plt.title('Churn by Senior Citizen (Stacked Bar Chart)')
plt.xlabel('SeniorCitizen')
plt.ylabel('Percentage (%)')
plt.xticks(rotation=0)
plt.legend(title='Churn', bbox_to_anchor = (0.9,0.9))  # Customize legend location

plt.show()
```
**comparative a greater pecentage of people in senior citizen category have churned**
```python
plt.figure(figsize = (9,4))
sns.histplot(x = "tenure", data = df, bins = 72, hue = "Churn")
plt.show()
```
**people who have used our services for a long time have stayed and people who have used our sevices**
```python
plt.figure(figsize=(4,4))
ax=sns.countplot(x='Contract',data =df,hue='Churn')
ax.bar_label(ax.containers[0])
plt.title('Count of Customer by Contract')
plt.show()
```
![](https://github.com/Issita/Customer-Churn-Analysis/blob/main/Count%20of%20Customer%20by%20Contract.png)
**people who have month to month contract are likely to churn then from those who have 1 or 2 years or contract.**
```python
df.columns.values
```

```python
columns = ['PhoneService', 'MultipleLines', 'InternetService', 'OnlineSecurity', 
           'OnlineBackup', 'DeviceProtection', 'TechSupport', 'StreamingTV', 'StreamingMovies']

# Number of columns for the subplot grid (you can change this)
n_cols = 3
n_rows = (len(columns) + n_cols - 1) // n_cols  # Calculate number of rows needed

# Create subplots
fig, axes = plt.subplots(n_rows, n_cols, figsize=(15, n_rows * 4))  # Adjust figsize as needed

# Flatten the axes array for easy iteration (handles both 1D and 2D arrays)
axes = axes.flatten()

# Iterate over columns and plot count plots
for i, col in enumerate(columns):
    sns.countplot(x=col, data=df, ax=axes[i], hue = df["Churn"])
    axes[i].set_title(f'Count Plot of {col}')
    axes[i].set_xlabel(col)
    axes[i].set_ylabel('Count')

# Remove empty subplots (if any)
for j in range(i + 1, len(axes)):
    fig.delaxes(axes[j])

plt.tight_layout()
plt.show()
```
![](https://github.com/Issita/Customer-Churn-Analysis/blob/main/multiple_visual.png)
**The majority of customers who do not churn tend to have services like PhoneService, InternetService (particularly DSL), and OnlineSecurity enabled. For services like OnlineBackup, TechSupport, and StreamingTV, churn rates are noticeably higher when these services are not used or are unavailable.**
```python
plt.figure(figsize=(9,4))
ax=sns.countplot(x='PaymentMethod',data =df,hue='Churn')
ax.bar_label(ax.containers[0])
ax.bar_label(ax.containers[1])
plt.title('Churned Customer by Payment Method')
plt.xticks(rotation = 90)
plt.show()
```
![](https://github.com/Issita/Customer-Churn-Analysis/blob/main/Churned%20Customer%20by%20Payment%20Method.png)
**customer is likely to churn when he is using electronic check as a payment method.**
