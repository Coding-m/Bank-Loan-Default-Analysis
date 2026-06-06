# Bank-Loan-Default-Analysis
Power BI dashboard analyzing 50,000+ bank loan records to identify key default risk predictors

🏦 Bank Loan Default & Risk Analysis Dashboard



📌 Table of Contents

1)Project Overview
2)Problem Statement
3)Dataset Description
4)Key Findings
5)Business Recommendations
6)DAX Measures


🎯 Project Overview

"Which borrowers are most likely to default on their loan — and why?"

This project presents a 4-page interactive Power BI dashboard built to analyze bank loan default patterns across 255,000+ loan records containing 20 features. 
The goal was to move beyond surface-level reporting and identify the root causes of loan default using financial, demographic, and behavioral data.
Metric                                Value
📊 Total Records Analyzed             255,000+
🔢 Features Used                      20
📄 Dashboard Pages                    4
🛠️ Primary Tool                       Power BI Desktop
📐 Formula Language                   DAX
🎯 Overall Default Rate               11.6%
💰 Average Loan Amount                ₹128,000


🔍 Problem Statement
Banks lose billions of dollars annually due to loan defaults. Traditional credit scoring models often miss key behavioral and demographic signals that predict default risk.
This dashboard was built to answer 5 critical business questions:

1. Which income group carries the highest default risk?
2. Does job stability affect a borrower's likelihood to default?
3. How does DTI ratio relate to default behavior?
4. Does having a CoSigner reduce default risk?
5. Which loan purposes are most prone to default?

📁 Dataset Description
The dataset contains 255,000+ loan records with the following features:

Numerical Features
Feature                                               Description                                           Type
Age                          Borrower's age in years                                                  Continuous
CreditScore                  Numerical credit score                                                   Continuous
DTIRatio                     Debt-to-Income Ratio (0-1)                                               Continuous
IncomeAnnual                 income of borrower                                                       Continuous
InterestRateLoan             interest rate %                                                          Continuous
LoanAmountTotal              loan amount                                                              Continuous
LoanTerm                     Loan repayment period                                                    Continuous
MonthsEmployed               Job tenure in months                                                     Continuous
NumCreditLines               Number of active credit lines                                            Discrete
DefaultTarget                variable (1=Default, 0=No Default)                                       Binary


Categorical Features
Feature                                               Description                                           Type
EmploymentType              Full-time, Part-time, Self-employed, Unemployed                           Employment status
EducationHigh               School, Bachelor's, Master's, PhD                                         Educationlevel
MaritalStatus               Single, Married, Divorced                                                 Marital status 
LoanPurpose                 Home, Business, Education, Auto, Other                                    Reason for loan
HasMortgage                 Yes / No                                                                  Existing mortgage
HasDependents               Yes / No                                                                  Financial dependents
HasCoSigner                 Yes / No                                                                  CoSigner presence
IncomeBracket               Low, Medium, High                                                         Derived income 
categoryCreditScoreBins     Very Low, Low, Medium, High                                               Derived credit category
AgeGroup                    Teenagers, Adults, Middle Age, Senior Citizen                             Derived age category



🔑 Key Findings
Finding 1 — Income is the Single Strongest Predictor 🏆
Low Income   → 22.0% default rate
Medium Income → 12.8% default rate  
High Income  →  9.5% default rate

🔑Risk Multiplier: Low income borrowers are 2.3x more likely to default than high income borrowers

Finding 2 — Job Stability Dramatically Reduces Risk
0-1 Year Employment   → 16.9% default rate
1-2 Years Employment  → 15.5% default rate
2-5 Years Employment  → 12.8% default rate
5-10 Years Employment →  8.9% default rate

🔑Every additional year of employment reduces default risk significantly

Finding 3 — DTI Ratio Confirms Financial Stress Theory
Very High DTI (60%+) → 12.5% default rate
High DTI (40-60%)    → 11.9% default rate
Medium DTI (20-40%)  → 11.5% default rate
Low DTI (0-20%)      → 10.6% default rate

🔑Higher financial burden = higher default probability

Finding 4 — CoSigner Acts as Financial Safety Net
Without CoSigner → 12.9% default rate
With CoSigner    → 10.4% default rate

🔑CoSigner presence reduces default risk by 19% Accountability and shared liability drive repayment

Finding 5 — Business Loans Carry Highest Purpose Risk
Business   → 12.3% | Auto       → 11.9%
Education  → 11.8% | Other      → 11.8%
Home       → 10.2% ← 🔑Safest — backed by physical asset


Finding 6 — Age Group Reveals Experience Effect
Teenagers        → 22.0% (limited financial experience)
Adults           → 17.0% (early career instability)
Middle Age Adults →  9.0% (peak earning stability)
Senior Citizens  →  5.0% (decades of financial discipline)


💼 Business Recommendations

Based on the analysis, here are 5 actionable recommendations for banking risk teams:

1. Require CoSigner for All Low Income Borrowers

=>Low income borrowers default at 22% — 2.3x higher than high income
=>Making a CoSigner mandatory creates financial accountability
=>CoSigner presence already proven to reduce default from 12.9% to 10.4%


2. Charge Risk-Adjusted Interest Rates Based on DTI Bins

=>DTI ratio directly predicts default behavior
=>Very High DTI borrowers (60%+) default at 12.5% vs Low DTI at 10.6%
=>Higher interest rates for high DTI segments compensate for increased risk exposure


3. Limit Loan Amounts for Borrowers With Less Than 1 Year Employment

=>Borrowers employed less than 1 year default at 16.9%
=>Job stability is a key predictor of repayment capacity
=>Capping loan amounts reduces bank exposure to unstable income sources


4. Apply Stricter Approval Criteria for Business Loan Applications

=>Business loans carry the highest default rate at 12.3%
=>Business income is unpredictable compared to salaried employment
=>Stricter documentation and collateral requirements reduce this risk


5. Weight Income Bracket Heavily in Credit Scoring Models

=>Income bracket is the single strongest predictor found in this analysis
=>Difference between Low and High income default rates is 131%
=>Current credit scoring models may underweight income as a standalone risk factor

📐 DAX Measures
-- Default Rate Percentage
Default Rate % = 
DIVIDE(
    COUNTROWS(FILTER(Loan_default, Loan_default[Default] = 1)),
    COUNTROWS(Loan_default),
    0
) * 100

-- Total Defaulters
Total Defaulters = 
COUNTROWS(
    FILTER(Loan_default, Loan_default[Default] = 1)
)

-- Average DTI Ratio
Avg DTI = AVERAGE(Loan_default[DTIRatio])

-- Average Interest Rate
Avg Interest Rate = AVERAGE(Loan_default[InterestRate])

Advanced Measures
-- Year over Year Loan Change
YOY Loan Change % = 
VAR CurrentYear = CALCULATE(SUM(Loan_default[LoanAmount]))
VAR PreviousYear = CALCULATE(
    SUM(Loan_default[LoanAmount]),
    DATEADD(Loan_default[Loan Date],-1,YEAR)
)
RETURN
DIVIDE(CurrentYear - PreviousYear, PreviousYear, 0) * 100

-- Risk Multiplier (Low vs High Income)
Risk Multiplier = 
DIVIDE(
    CALCULATE([Default Rate %], 
        Loan_default[Income Bracket] = "Low Income"),
    CALCULATE([Default Rate %], 
        Loan_default[Income Bracket] = "High Income"),
    0
)

-- High Risk Borrowers Count
High Risk Borrowers = 
COUNTROWS(
    FILTER(Loan_default,
        Loan_default[DTIRatio] > 0.40 &&
        Loan_default[Default] = 1
    )
)

Calculated Columns
-- DTI Risk Bins
DTI Bins = 
SWITCH(TRUE(),
    Loan_default[DTIRatio] <= 0.20, "Low (0-20%)",
    Loan_default[DTIRatio] <= 0.40, "Medium (20-40%)",
    Loan_default[DTIRatio] <= 0.60, "High (40-60%)",
    "Very High (60%+)"
)

-- Months Employed Bins
MonthsEmployed Bins = 
SWITCH(TRUE(),
    Loan_default[MonthsEmployed] <= 12,  "0-1 Year",
    Loan_default[MonthsEmployed] <= 24,  "1-2 Years",
    Loan_default[MonthsEmployed] <= 60,  "2-5 Years",
    Loan_default[MonthsEmployed] <= 120, "5-10 Years",
    "10+ Years"
)
