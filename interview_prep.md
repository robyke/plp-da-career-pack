# Interview Preparation

## Technical Questions

### 1. What is a LEFT JOIN?

A LEFT JOIN returns all rows from the left table and matching rows from the right table. If there is no matching row in the right table, the result still keeps the row from the left table and shows NULL values for the missing columns.

Example:

```sql
SELECT u.user_id, u.county, t.amount
FROM users u
LEFT JOIN transactions t
ON u.user_id = t.user_id;
```

I would use a LEFT JOIN when I want to keep all customers, including customers who may not have made a transaction.

### 2. How do you handle missing data?

I first check how much data is missing and which columns are affected. Then I decide whether to remove, replace or investigate the missing values depending on the business meaning.

For example, in my PesaPap capstone, a missing transaction amount was replaced using the median positive transaction amount instead of the mean because the median is less affected by extreme values.

I also document every cleaning decision so the process is reproducible.

### 3. What is the difference between mean and median?

The mean is calculated by adding all values and dividing by the number of values.

The median is the middle value after the data is sorted.

I prefer the median when the data contains strong outliers or is highly skewed because it is less affected by extreme values.

For example, transaction amounts can contain unusually large payments, so the median can sometimes describe the typical transaction better than the mean.

### 4. What does a p-value mean?

A p-value measures how compatible the observed result is with the null hypothesis.

A small p-value, such as below 0.05, gives evidence against the null hypothesis.

In my PesaPap capstone, I used a Mann-Whitney U test to compare customer value between Referral and Social acquisition channels. The p-value was approximately 6.24 × 10^-8, so I rejected the null hypothesis at the 0.05 significance level.

Because the dataset was synthetic and channel engagement differences were built into the generator, I interpreted the result as a demonstration of the statistical method rather than proof of a real-world causal relationship.

### 5. How would you investigate a sudden drop in sales?

I would first confirm that the drop is real and not caused by missing data, duplicate records or a reporting problem.

Then I would compare the affected period with previous periods and break the results down by important dimensions such as branch, product, customer segment, acquisition channel or location.

I would also check whether transaction volume, average order value or both changed.

After identifying where the decline happened, I would investigate possible causes such as product availability, pricing, customer activity, seasonality or operational issues.

Finally, I would summarise the main cause, quantify its impact and recommend an action.

## Behavioural Questions

### 1. Tell me about a time you solved a data quality problem.

**Situation:**  
During my PesaPap capstone project, the synthetic transaction dataset included duplicate transaction IDs, inconsistent text formatting, a missing transaction amount, a negative amount and a transaction that occurred before the customer's signup date.

**Task:**  
I needed to create a reliable cleaned dataset that could be used for SQL analysis, exploratory analysis, statistical testing and dashboard reporting.

**Action:**  
I created a reusable Python cleaning function using pandas. I removed duplicate transaction IDs, standardised text fields, imputed the missing amount using the median positive transaction amount, removed invalid non-positive transactions and checked transaction dates against signup dates. I also created a cleaning log to document every issue and correction.

**Result:**  
The process reduced the raw dataset from 70,828 transactions to 70,824 valid transactions. The final cleaned dataset contained 70,824 unique transaction IDs and produced a verified transaction value of KES 111,178,105.

### 2. Tell me about a time you used data to make a recommendation.

**Situation:**  
In my PesaPap capstone, the Head of Growth needed to understand which customers and acquisition channels contributed the most value and where retention efforts should be focused.

**Task:**  
My goal was to analyse customer value, segmentation, acquisition performance and retention, then translate the results into clear business recommendations.

**Action:**  
I used Python, pandas and SQL to analyse customer behaviour. I created customer segments using transaction frequency and value, built cohort retention analysis and compared acquisition channels. I also developed a Looker Studio dashboard to communicate the main findings.

**Result:**  
The analysis showed that High Value customers contributed about 68.95% of total transaction value, Referral generated about KES 29.03 million and 478 customers were inactive. Based on these results, I recommended protecting High Value customers, prioritising Referral acquisition while monitoring cost, and creating reactivation campaigns for inactive customers.
