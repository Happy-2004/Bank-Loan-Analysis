# Bank Loan Data Analysis using SQL

## Overview

This project involves a detailed analysis of bank loan data using SQL. The goal is to derive actionable insights into loan performance, borrower risk, repayment behavior, and lending trends. This SQL-driven report is ideal for financial institutions to make better decisions about funding, credit risk, and customer profiling.

## Objectives

- Track monthly loan applications and funding.
- Analyze repayment patterns and borrower metrics.
- Segment loans into "Good" and "Bad" based on status.
- Break down data by loan purpose, home ownership, employment length, and more.
- Identify risk trends and key performance indicators (KPIs).

## Dataset

The dataset includes bank loan transactions with the following fields:

- **Loan Data**: ID, issue date, loan amount, total payment, interest rate, DTI.
- **Borrower Info**: State, employment length, loan term, home ownership.
- **Loan Attributes**: Loan status, purpose, grade.

## Schema

```sql
CREATE TABLE bank_loan_data (
    id INT,
    issue_date DATE,
    loan_amount DECIMAL(10, 2),
    total_payment DECIMAL(10, 2),
    int_rate DECIMAL(5, 4),
    dti DECIMAL(5, 4),
    loan_status VARCHAR(50),
    address_state VARCHAR(50),
    term VARCHAR(20),
    emp_length VARCHAR(50),
    purpose VARCHAR(100),
    home_ownership VARCHAR(50),
    grade VARCHAR(5)
);
```

## Business Problems and SQL Solutions

### KPI Section

#### 1. Total Loan Applications

```sql
SELECT COUNT(id) AS Total_Applications FROM bank_loan_data;
```

---

#### 2. MTD Loan Applications (Month = 12)

```sql
SELECT COUNT(id) AS Total_Applications 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12;
```

---

#### 3. PMTD Loan Applications (Month = 11)

```sql
SELECT COUNT(id) AS Total_Applications 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 11;
```

---

#### 4. Total Funded Amount

```sql
SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data;
```

---

#### 5. MTD Total Funded Amount

```sql
SELECT SUM(loan_amount) AS Total_Funded_Amount 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12;
```

---

#### 6. PMTD Total Funded Amount

```sql
SELECT SUM(loan_amount) AS Total_Funded_Amount 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 11;
```

---

#### 7. Total Amount Received

```sql
SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data;
```

---

#### 8. MTD Total Amount Received

```sql
SELECT SUM(total_payment) AS Total_Amount_Collected 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12;
```

---

#### 9. PMTD Total Amount Received

```sql
SELECT SUM(total_payment) AS Total_Amount_Collected 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 11;
```

---

#### 10. Average Interest Rate

```sql
SELECT AVG(int_rate) * 100 AS Avg_Int_Rate FROM bank_loan_data;
```

---

#### 11. MTD Average Interest Rate

```sql
SELECT AVG(int_rate) * 100 AS MTD_Avg_Int_Rate 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12;
```

---

#### 12. PMTD Average Interest Rate

```sql
SELECT AVG(int_rate) * 100 AS PMTD_Avg_Int_Rate 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 11;
```

---

#### 13. Average DTI

```sql
SELECT AVG(dti) * 100 AS Avg_DTI FROM bank_loan_data;
```

---

#### 14. MTD Average DTI

```sql
SELECT AVG(dti) * 100 AS MTD_Avg_DTI 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12;
```

---

#### 15. PMTD Average DTI

```sql
SELECT AVG(dti) * 100 AS PMTD_Avg_DTI 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 11;
```

---

### Good Loan Analysis

#### 16. Good Loan Percentage

```sql
SELECT
  (COUNT(CASE WHEN loan_status = 'Fully Paid' OR loan_status = 'Current' THEN id END) * 100.0) / 
  COUNT(id) AS Good_Loan_Percentage
FROM bank_loan_data;
```

---

#### 17. Good Loan Applications

```sql
SELECT COUNT(id) AS Good_Loan_Applications 
FROM bank_loan_data 
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
```

---

#### 18. Good Loan Funded Amount

```sql
SELECT SUM(loan_amount) AS Good_Loan_Funded_Amount 
FROM bank_loan_data 
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
```

---

#### 19. Good Loan Amount Received

```sql
SELECT SUM(total_payment) AS Good_Loan_Amount_Received 
FROM bank_loan_data 
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
```

---

### Bad Loan Analysis

#### 20. Bad Loan Percentage

```sql
SELECT
  (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) / 
  COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data;
```

---

#### 21. Bad Loan Applications

```sql
SELECT COUNT(id) AS Bad_Loan_Applications 
FROM bank_loan_data 
WHERE loan_status = 'Charged Off';
```

---

#### 22. Bad Loan Funded Amount

```sql
SELECT SUM(loan_amount) AS Bad_Loan_Funded_Amount 
FROM bank_loan_data 
WHERE loan_status = 'Charged Off';
```

---

#### 23. Bad Loan Amount Received

```sql
SELECT SUM(total_payment) AS Bad_Loan_Amount_Received 
FROM bank_loan_data 
WHERE loan_status = 'Charged Off';
```

---

### Loan Status Summary

#### 24. Loan Status Breakdown

```sql
SELECT
  loan_status,
  COUNT(id) AS LoanCount,
  SUM(total_payment) AS Total_Amount_Received,
  SUM(loan_amount) AS Total_Funded_Amount,
  AVG(int_rate * 100) AS Interest_Rate,
  AVG(dti * 100) AS DTI
FROM bank_loan_data
GROUP BY loan_status;
```

---

#### 25. MTD Loan Status Summary

```sql
SELECT 
  loan_status, 
  SUM(total_payment) AS MTD_Total_Amount_Received, 
  SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12 
GROUP BY loan_status;
```

---

### Loan Overview Analysis

#### 26. Monthly Trends

```sql
SELECT 
  MONTH(issue_date) AS Month_Number, 
  DATENAME(MONTH, issue_date) AS Month_Name, 
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date);
```

---

#### 27. State-wise Loan Distribution

```sql
SELECT 
  address_state AS State, 
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY address_state
ORDER BY address_state;
```

---

#### 28. Term-wise Loan Distribution

```sql
SELECT 
  term, 
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY term
ORDER BY term;
```

---

#### 29. Employment Length Distribution

```sql
SELECT 
  emp_length AS Employee_Length, 
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY emp_length
ORDER BY emp_length;
```

---

#### 30. Purpose of Loan

```sql
SELECT 
  purpose, 
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY purpose
ORDER BY purpose;
```

---

#### 31. Home Ownership Analysis

```sql
SELECT 
  home_ownership, 
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY home_ownership
ORDER BY home_ownership;
```

---

## Findings and Conclusion

- **Monthly Trends**: Lending spikes in certain months show seasonal borrowing behavior.
- **Good vs. Bad Loans**: Helps assess credit risk and improve underwriting.
- **Geographic and Term Analysis**: Uncovers regional lending behaviors and preferences.
- **Purpose & Profile**: Employment length and home ownership significantly correlate with loan performance.
