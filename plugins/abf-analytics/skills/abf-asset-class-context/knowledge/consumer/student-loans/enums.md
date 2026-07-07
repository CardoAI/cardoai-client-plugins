---
title: Consumer — Student Loans — Enum Vocabulary
tier: enums
enum_count: 14
---

# Consumer — Student Loans — Enum / Allowed Values

### investmens — Performance Status

status of the loan performance based on transaction specific contractual definition as per defined list of values:

Allowed values:
- Performing
- In Delay
- Default
- Grace Period
- Full recovery
- In Stock
- Other

### investmens — Repayment Status

type of repayment status as per defined list.

Allowed values:
- No Repayment
- Partially Repaid
- Fully Repaid
- Repurchased
- Prepaid
- Write-off Partial Recovery
- Write-off No Recovery
- Asset Sale
- No Recovery

### investmens — Amortization Type

amortization type as per defined list of values. Default value: Fixed Payment

Allowed values:
- Fixed Payment
- Constant Principal
- Interest-Only Payments
- Partial Interest-Only Payments
- Installment Plan

### investmens — Principal Installment Frequency

scheduled frequency of the principal amount payment as per defined list of values. Default value: Monthly

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investmens — Interest Installment Frequency

scheduled frequency of interest payments, as per defined list of values:

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investmens — Hardship Flag

Boolean indicator of whether the borrower is currently on an active hardship plan.

Allowed values:
- True | False

### investmens — Is Closed

Flag indicating whether the loan account has been fully closed/repaid.

Allowed values:
- True | False

### borrower — Bankruptcy Flag

flag that indicates if the borrower is in bankruptcy.

Allowed values:
- True | False

### borrower — Bankruptcy Status

bankruptcy status of the borrower, as per the defined list of values.

Allowed values:
- Withdraw
- Discharge
- Reinstate
- Filed
- Dismiss
- Confirm
- Closed

### borrower — Primary Income Type

primary income type of the borrower as per defined list of values.

Allowed values:
- Gross annual income
- Net annual income (net of tax and social security)
- Net annual income (net of tax only)
- Net annual income (net of social security only)
- Estimated net annual income (net of tax and social security)
- Estimated net annual income (net of tax only)
- Estimated net annual income (net of social security only)
- Disposable Income
- Borrower is legal entity
- Other

### borrower — Employment Status

employment status of the borrower as per defined list of values.

Allowed values:
- Employed - Private Sector
- Employed - Public Sector
- Employed - Sector Unknown
- Unemployed
- Self-employed
- Student
- Pensioner
- No Employment, Obligor is Legal Entity
- Other

### borrower — discipline_category

High-level grouping of the borrower's field of study into a broader academic discipline (e.g. STEM, Business, Humanities, Healthcare). Enables portfolio-level analysis of income and employment risk across academic sectors.

Allowed values:
- STEM | Business & Economics | Humanities & Social Sciences | Healthcare & Life Sciences | Law | Arts & Design | Education | Trade & Vocational | Other

### borrower — study_level

The level of study the borrower is undertaking, indicating where they are in the academic progression. Undergraduate borrowers typically have smaller balances and longer repayment horizons; postgraduate and professional students carry higher balances but generally stronger earning trajectories.

Allowed values:
- Undergraduate | Postgraduate| Postgraduate Research | Other

### cash_flows — Cash Flow Type

Classification of the cash flow received (e.g. General Repayment, Principal Repayment, Interest, Fee).

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
