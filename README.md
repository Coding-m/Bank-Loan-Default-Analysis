# 🏦 Bank Loan Default & Risk Analysis Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Visualization-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Data Analytics](https://img.shields.io/badge/Data%20Analytics-Banking%20Risk%20Insights-1f77b4?style=for-the-badge)
![DAX](https://img.shields.io/badge/DAX-Measures%20%26%20KPIs-8A2BE2?style=for-the-badge)
![Project](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Dataset](https://img.shields.io/badge/Records-255K+-brightgreen?style=for-the-badge)

---

## 📊 Project Overview

This project is a **Power BI-based Bank Loan Default & Risk Analysis Dashboard** designed to identify key factors that influence loan default behavior.

> 🎯 Goal: Understand *which borrowers are most likely to default and why*

A fully interactive **4-page dashboard** was built using **255,000+ loan records** and **20 features**, enabling deep financial risk analysis.

---

## 📈 Key Metrics

| Metric | Value |
|--------|------|
| Total Records | 255,000+ |
| Features Used | 20 |
| Dashboard Pages | 4 |
| Tool Used | Power BI Desktop |
| Language | DAX |
| Default Rate | 11.6% |
| Avg Loan Amount | ₹128,000 |

---

## ❗ Problem Statement

Banks lose significant revenue due to loan defaults. Traditional credit scoring models often fail to capture real-world risk indicators.

This dashboard answers:

- Who is most likely to default?
- Does income affect repayment behavior?
- How does job stability influence risk?
- Does CoSigner reduce default probability?
- Which loan purposes are most risky?

---

## 📁 Dataset Description

### 🔢 Numerical Features

| Feature | Description |
|--------|-------------|
| Age | Borrower age |
| CreditScore | Credit score |
| DTIRatio | Debt-to-Income ratio |
| Income | Annual income |
| InterestRate | Loan interest rate |
| LoanAmount | Loan amount |
| LoanTerm | Repayment duration |
| MonthsEmployed | Job tenure |
| NumCreditLines | Active credit lines |
| Default | Target (0 = No, 1 = Yes) |

---

### 🏷️ Categorical Features

- Employment Type (Full-time, Part-time, etc.)
- Education Level
- Marital Status
- Loan Purpose
- Mortgage Status
- Dependents
- CoSigner Presence
- Income Bracket (Low / Medium / High)
- Credit Score Bins
- Age Groups

---

## 🔑 Key Insights

### 🏆 1. Income is the Strongest Risk Factor
- Low Income → **22.0% default rate**
- Medium Income → **12.8%**
- High Income → **9.5%**

👉 Low-income borrowers are **2.3x riskier**

---

### 💼 2. Job Stability Matters
- 0–1 year → 16.9%
- 1–2 years → 15.5%
- 2–5 years → 12.8%
- 5–10 years → 8.9%

👉 More experience = lower risk

---

### 📉 3. Debt-to-Income (DTI) Impact
- Very High (60%+) → 12.5%
- Low (0–20%) → 10.6%

👉 Higher financial stress increases default probability

---

### 🤝 4. CoSigner Reduces Risk
- Without CoSigner → 12.9%
- With CoSigner → 10.4%

👉 ~19% reduction in default risk

---

### 🏠 5. Loan Purpose Risk
- Business → 12.3% (highest risk)
- Home → 10.2% (safest)

---

### 👥 6. Age Factor
- Teenagers → 22%
- Adults → 17%
- Middle Age → 9%
- Seniors → 5%

👉 Financial maturity reduces risk significantly

---

## 💼 Business Recommendations

### 1. Mandatory CoSigner for Low Income Borrowers
High-risk group (22%) should require shared liability.

### 2. Risk-Based Interest Rates
Higher DTI → higher interest rates.

### 3. Limit Loans for New Employees
Borrowers with <1 year employment show high default risk (16.9%).

### 4. Stronger Rules for Business Loans
Business loans require stricter verification and collateral.

### 5. Improve Credit Scoring Models
Income should have higher weight in risk prediction models.

---

## 📐 DAX Measures

### 🔢 Core Measures


Default Rate % =
DIVIDE(
    COUNTROWS(FILTER(Loan_default, Loan_default[Default] = 1)),

Total Defaulters =
COUNTROWS(FILTER(Loan_default, Loan_default[Default] = 1))
    COUNTROWS(Loan_default),
    0
) * 100


Avg DTI = AVERAGE(Loan_default[DTIRatio])

Avg Interest Rate = AVERAGE(Loan_default[InterestRate])

Risk Multiplier =
DIVIDE(
    CALCULATE([Default Rate %], Loan_default[Income Bracket] = "Low Income"),
    CALCULATE([Default Rate %], Loan_default[Income Bracket] = "High Income"),
    0
)
