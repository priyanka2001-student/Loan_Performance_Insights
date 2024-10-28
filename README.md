# Loan Performance Insights

## Summary Dashboard

![Summary](https://github.com/user-attachments/assets/664f3adb-9477-4f67-bbc7-d8b9266ce39a)

## Overview Dashboard

![Overview](https://github.com/user-attachments/assets/4a754f68-82f6-4598-b80f-79db163a1695)

## Table of Contents

[Project Overview](#project-overview)

[ Dataset Details](#dataset-details)

[Tools Utilized](#tools-utilized)

[Data Cleaning/Preparation](#DataCleaning/Preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Recommendations](#recommendations)

[Limitations](#limitations)

## Project Overview
This Dashboard is designed to monitor and evaluate our bank's lending activities and performance, aiming to provide insights into key loan-related metrics and their trends over time.

## Dataset Details

- **Dataset:** `Bank Loan Data.csv`
- **Records:** 38,576
- **Columns:** 24

### Column Descriptions

1. **id:** Unique identifier for each loan application.
2. **address_state:** State where the borrower resides.
3. **application_type:** Indicates if the application is individual or joint.
4. **emp_length:** Length of employment in years.
5. **emp_title:** Job title of the borrower.
6. **grade:** Credit grade assigned based on the loan application.
7. **home_ownership:** Indicates whether the borrower rents, owns, or has a mortgage.
8. **issue_date:** Date the loan was issued.
9. **last_credit_pull_date:** Most recent date the borrower's credit was checked.
10. **last_payment_date:** Date of the last payment made on the loan.
11. **loan_status:** Current status of the loan (e.g., fully paid, charged off).
12. **next_payment_date:** Date when the next payment is due.
13. **member_id:** Unique identifier for the member associated with the loan.
14. **purpose:** Purpose of the loan (e.g., car, home improvement).
15. **sub_grade:** More specific credit grade based on additional criteria.
16. **term:** Duration of the loan in months.
17. **verification_status:** Indicates if the income is verified or not.
18. **annual_income:** Annual income of the borrower.
19. **dti:** Debt-to-income ratio of the borrower.
20. **installment:** Monthly payment amount for the loan.
21. **int_rate:** Interest rate applied to the loan.
22. **loan_amount:** Total amount of the loan.
23. **total_acc:** Total number of credit accounts held by the borrower.
24. **total_payment:** Total payments made over the life of the loan.


## Tools Utilized
- **Microsoft SQL Server**
- **Tableau Desktop** - For Report Creation
  - Links to the Financial_Loan Project and additional Tableau Public Dashboards:
  
    [Insert Link] [add link ]

## Data Cleaning/Preparation
During the initial phase of data preparation, I executed the following steps:
- Data Loading and Inspection using **MS SQL Server**
  - Employed it to import and refine the dataset.
  - The "emp_title" field, originally set as VARCHAR(50), was expanded to VARCHAR(100) to accommodate longer entries.
  - The "id" column was designated as the *Primary Key*.
  - All NVARCHAR fields were converted to VARCHAR.
  - The "total_payment" field, initially a SMALLINT, was updated to INT to allow for larger values.
  - The "loan_amount" field was similarly adjusted to INT.

## Exploratory Data Analysis
The exploratory data analysis focused on investigating the financial loan dataset to address essential questions, such as:

A) Key Performance Indicators (KPIs)
1. What is the *Total Loan Applications*? This includes:
   - Current Month-to-Date (MTD) loan applications
   - Previous Month-to-Month (PMTD) for tracking changes.
   
2. What is the *Total Funded Amount*? This involves:
   - Current Month-to-Date (MTD) total funded amount
   - Previous Month-to-Month (PMTD) for metric tracking.

3. What is the *Total Amount Received*? This includes:
   - Current Month-to-Date (MTD) to ascertain total amount received
   - Previous Month-to-Month (PMTD) for tracking variations.

4. What is the *Average Interest Rate*? This comprises:
   - Current Month-to-Date (MTD) to determine the average interest rate
   - Previous Month-to-Month (PMTD) for tracking changes.

5. What is the *Average Debt-to-Income Ratio* (DTI)? Evaluating the average DTI for borrowers provides insights into their financial health, including:
   - Current Month-to-Date (MTD) average DTI
   - Previous Month-to-Month (PMTD) for tracking changes.
   
   *Note: Both current and previous month calculations will facilitate Month-over-Month (MoM) trend analysis.*

B) What distinguishes Good Loans from Bad Loans?

C) What is the overall Loan Status?

The analysis will consider the following aspects:

   a) Monthly Loan Trends

   b) Loans by State

   c) Loans by Employment Length
   
   d) Loans by Purpose

   e) Loans by Home Ownership


## Data Analysis
As previously mentioned, the analyses were conducted exclusively using **MS SQL Server**. Below are the key analyses performed:

1. **Total Loan Applications** related to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMTD)*
   - Total Loan Applications
   ```SQL 
   SELECT
         COUNT(id) AS Total_Application
   FROM Bank_Loan_Data;
   ```
   - Month-to-Date (MTD) Total Loan Applications
   ```SQL
   SELECT
         COUNT(id) AS MTD_Total_Loan_Applications
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 12
       AND YEAR(issue_date) = 2021;
   ```
   - Previous Month-to-Month (PMTD)
   ```SQL
   SELECT
         COUNT(id) AS PMTD_Total_Loan_Applications
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 11
       AND YEAR(issue_date) = 2021;
   ```
   Image showcasing Total Loan Applications, sourced from Tableau.

   ![Total_loan_apps](https://github.com/user-attachments/assets/b6d0cdc5-6d71-4339-aa7d-389be47222fc)

---

2. **Total Funded Amount** in terms of *Month-to-Date (MTD)* and *Previous Month-to-Date (PMTD)*
   - Total Funded Amount
   ```SQL
   SELECT SUM(loan_amount) AS Total_Funded_Amount
   FROM Bank_Loan_Data;
   ```
   - Month-to-Date (MTD)
   ```SQL
   SELECT
       SUM(loan_amount) AS MTD_Total_Funded_Amount
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 12
       AND YEAR(issue_date) = 2021;
   ```
   - Previous Month-to-Date (PMTD)
   ```SQL
   SELECT
         SUM(loan_amount) AS PMTD_Total_Funded_Amount
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 11
       AND YEAR(issue_date) = 2021;
   ```
   Image illustrating Total Funded Loans.

   ![Total_Funded Amount](https://github.com/user-attachments/assets/8c79dd20-1452-41dd-87ae-05169261e398)

---

3. **Total Amount Received** with respect to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMTD)*
   - Total Amount Received
   ```SQL
   SELECT
        SUM(total_payment) AS Total_Amount_Received
   FROM Bank_Loan_Data;
   ```
   - Month-to-Date (MTD)
   ```SQL
   SELECT
        SUM(total_payment) AS MTD_Total_Amount_Received
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 12
       AND YEAR(issue_date) = 2021;
   ```
   - Previous Month-to-Date (PMTD)
   ```SQL
   SELECT
        SUM(total_payment) AS PMTD_Total_Amount_Received
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 11
       AND YEAR(issue_date) = 2021;
   ```
   Image showcasing Total Amount Received.

   ![Total_Amount_Received](https://github.com/user-attachments/assets/49022554-78b9-4fe4-92ff-bc5a48399202)

---

4. **Average Interest Rate** with regard to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMTD)*
   - Overall Average Interest Rate
   ```SQL
   SELECT
        ROUND(AVG(int_rate), 4) * 100 AS Avg_Interest_Rate
   FROM Bank_Loan_Data;
   ```
   - Month-to-Date (MTD)
   ```SQL
   SELECT
        ROUND(AVG(int_rate), 4) * 100 AS MTD_Avg_Interest_Rate
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 12
       AND YEAR(issue_date) = 2021;
   ``` 
   - Previous Month-to-Date (PMTD)
   ```SQL
   SELECT
        ROUND(AVG(int_rate), 4) * 100 AS PMTD_Avg_Interest_Rate
   FROM Bank_Loan_Data
   WHERE
       MONTH(issue_date) = 11
       AND YEAR(issue_date) = 2021;
   ```
   Image for Average Interest Rates.

   ![Avg_Int_Rate](https://github.com/user-attachments/assets/330e2bac-417e-434b-b509-7f8d6f8e8839)

---

5. **Average Debt-to-Income Ratio** concerning *Month-to-Date (MTD)* and *Previous Month-to-Date (PMTD)*
   - Overall Average DTI
   ```SQL
   SELECT
        ROUND(AVG(dti), 4) * 100 AS Avg_DTI
   FROM Bank_Loan_Data;
   ```
   - Month-to-Date (MTD)
   ```SQL
   SELECT
         ROUND(AVG(dti), 4) * 100 AS MTD_Avg_DTI
   FROM Bank_Loan_Data
   WHERE
         MONTH(issue_date) = 12
         AND YEAR(issue_date) = 2021;
   ```
   - Previous Month-to-Date (PMTD)
   ```SQL
   SELECT
        ROUND(AVG(dti), 4) * 100 AS PMTD_Avg_DTI
   FROM Bank_Loan_Data
   WHERE
         MONTH(issue_date) = 11
         AND YEAR(issue_date) = 2021;
   ```
   Image depicting Average DTIs.

   ![Avg_DTIs](https://github.com/user-attachments/assets/2d8101f5-aaa2-4e92-90e7-9d721b2cc4a8)
---
### B. Good Loans Vs Bad Loans Issued

To evaluate the bank's lending performance and assess loan quality, we distinguish between **'Good Loans'** and **'Bad Loans'** based on specific criteria, including application percentages, funded amounts, and total received amounts.

#### Good Loans Issued (Good Debt)
Good loans are those where borrowers successfully repay their debts within the specified period, typically classified as "Fully Paid" or "Current."

1. **Good Loan Percentage**
   ```sql
   SELECT 
       (COUNT(CASE WHEN loan_status IN ('Fully Paid', 'Current') THEN id END) * 100.0) 
       / COUNT(id) AS Good_loan_percentage
   FROM Bank_Loan_Data;
   ```

2. **Good Loan Applications**
   ```sql
   SELECT
       COUNT(id) AS Good_loan_Applications
   FROM Bank_Loan_Data
   WHERE loan_status IN ('Fully Paid', 'Current');
   ```

3. **Good Loan Funded Amount**
   ```sql
   SELECT
       SUM(loan_amount) AS Good_loan_Funded_Amount
   FROM Bank_Loan_Data
   WHERE loan_status IN ('Fully Paid', 'Current');
   ```

4. **Good Loan Total Amount Received**
   ```sql
   SELECT
       SUM(total_payment) AS Good_Loan_Received_Amount
   FROM Bank_Loan_Data
   WHERE loan_status IN ('Fully Paid', 'Current');
   ```

![Good_Loans_Issued](https://github.com/user-attachments/assets/9bece66f-b67b-4118-bc61-a543b4e8c5a6)

From the analysis, **86%** of loans were categorized as good, indicating a high repayment rate. A total of **33,200** good loans were issued, amounting to **$370.2M** funded, with **$435.8M** received, yielding a profit of **$65.6M**.

---

#### Bad Loans Issued (Bad Debt)
Bad loans are defined as those where borrowers fail to meet repayment obligations, typically classified as "Charged Off."

1. **Bad Loan Percentage**
   ```sql
   SELECT 
       (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) 
       / COUNT(id) AS Bad_loan_percentage
   FROM Bank_Loan_Data;
   ```

2. **Bad Loan Applications**
   ```sql
   SELECT
       COUNT(id) AS Bad_Loan_Application
   FROM Bank_Loan_Data
   WHERE loan_status = 'Charged Off';
   ```

3. **Bad Loan Funded Amount**
   ```sql
   SELECT
       SUM(loan_amount) AS Bad_Loan_Funded_Amount
   FROM Bank_Loan_Data
   WHERE loan_status = 'Charged Off';
   ```

4. **Bad Loans Amount Received**
   ```sql
   SELECT
       SUM(total_payment) AS Bad_Loan_Amount_Received
   FROM Bank_Loan_Data
   WHERE loan_status = 'Charged Off';
   ```

![Bad_Loan_Issued](https://github.com/user-attachments/assets/89c04637-5574-43b3-994b-34286205eb4e)

The data reveals that **13%** of loans were classified as bad, with **5,300** applications leading to **$65.5M** funded but only **$37.3M** received, resulting in a loss of **$28.2M**.

---

### Additional Insights

#### a) Loan Applications By Monthly Trends
![Total_Loan_Apps By_Month](https://github.com/user-attachments/assets/121e5a19-d597-4160-89ef-948bd16861e5)

The trend indicates a steady increase in loan applications, peaking in December, likely driven by seasonal factors and economic conditions.

#### b) Loan Applications By States
![Tot_Loan_Apps_By_State](https://github.com/user-attachments/assets/16ff3f7a-7525-438b-8edd-185744e56966)

**California** leads with **6,894** applications, reflecting its population and economic activity, while states in the Midwest and South show lower application figures.

**Total Funded Amount by States**
![Tot_Fnd_Amt_by_State](https://github.com/user-attachments/assets/e0fe1ee6-a788-4310-95c5-d5f7ed08677a)

California also has the highest funded amount at **$78.5M**, indicating a correlation between application volume and funding.

**Total Amount Received By States**
![Tot_Amt_Rcvd_by_State](https://github.com/user-attachments/assets/7dfc8100-f99a-401f-afb1-393f51261d8d)

California tops again with **$83.9M** received, further underscoring its economic significance.

---

#### c) Loan Applications By Employee Length

![Loan_Apps_by_Emp_length](https://github.com/user-attachments/assets/a319edca-c033-4d71-a526-5d048f98c7c8)

- **New employees** show the highest application rates, while those with over **10 years** tend to apply less frequently.

**Total Funded Amount**

![Funded_Amount_by_Emp_Length](https://github.com/user-attachments/assets/8c770bf9-cb10-4216-bb21-09f5e76e455e)

Long-tenured employees receive more funding, likely due to trust and stability.

**Total Amount Received**

![Amount_Received_by_Emp_Length](https://github.com/user-attachments/assets/338d9e3f-2c65-4cd6-9bb0-bad3ca2002b8)

Similar trends are observed, with longer-tenured employees receiving larger amounts.

---

#### d) Loan Applications By Purpose

![Loan_Apps_by_Purpose](https://github.com/user-attachments/assets/b7cb041d-0d2d-4a78-8031-9d4d634f6dd9)

**Debt consolidation** leads the purpose for loans, followed by **credit card debt** and **home improvement**.

**Loan Funded Amount by Purpose**

![Funded_Amount_by_Purpose](https://github.com/user-attachments/assets/60432b07-a50e-4d84-ae7f-365c1644dbda)

Debt consolidation receives the largest funding, highlighting financial pressures on borrowers.

**Loan Amount Received by Purpose**

![Amount_Received_by_Purpose](https://github.com/user-attachments/assets/93afeaf9-d0e1-4007-9b10-4a50656619fd)

Debt consolidation also tops the amount received, indicating successful repayment in this category.

---

#### e) Loan Applications by Home Ownership

![Tot_Loan_Apps_by_Home_Owned](https://github.com/user-attachments/assets/e1d2652a-1e0e-4ef6-8c72-ff8a3ac4db97)

**Renters** account for the majority of loan applications, with **homeowners with mortgages** following closely.

**Funded Amount By Home Ownership**

![Tot_Fnd_Amt_by_Home_Owned](https://github.com/user-attachments/assets/0e1ab471-2907-4448-b9cc-ccc5197c33ff)

Mortgaged homeowners receive the largest funding amounts, while renters also have significant funding.

**Amount Received By Home Ownership**

![Tot_Amt_Rcvd_by_Home_Owned](https://github.com/user-attachments/assets/b2b0c783-d2fa-4242-bc97-32bf73b15700)

Consistently, mortgaged homeowners lead in the total amount received, indicating higher repayment success.

---

## Recommendations

Based on the analysis, the following actions are recommended:

1. **Investigate February Trends**: The bank should explore the reasons behind the dip in loan applications in February. Understanding whether this is a seasonal trend or related to external factors will help in making informed decisions about loan offerings during that month.

2. **Leverage High Demand Periods**: The peak application months from July to December present a strong opportunity for the bank to increase loan offerings and marketing efforts, aligning with higher demand during this period.

3. **Focus on Tenured Employees**: Employees with over 10 years of service show higher repayment rates. If factors such as loyalty or salary are contributing to this trend, it may be wise to prioritize loan offerings to this group. Additionally, consider those with 2 years of tenure, as they have shown promising repayment potential compared to those with 3 or 4 years.

4. **Target Renters and Mortgage Holders**: While renters lead in application numbers, those with mortgages have a higher repayment rate. Therefore, the bank should consider targeting both demographics for loans, with a greater emphasis on mortgage holders due to their better return rates.

5. **Implement Targeted Marketing**: The bank could benefit from targeted marketing campaigns or special loan promotions during high-demand months to further drive application numbers.

## Limitations

- **Lack of Economic Context**: The analysis lacks specific economic conditions during the loan periods, making it difficult to assess external influences on loan performance and applicant behavior.

- **Absence of Mortality Data**: The absence of "death rates" or related metrics limits the analysis's depth, particularly in understanding factors that might contribute to loan defaults.
