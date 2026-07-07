---
title: Consumer — Home Improvement — Enum Vocabulary
tier: enums
enum_count: 15
---

# Consumer — Home Improvement — Enum / Allowed Values

### investments — Financing Purpose

type of financing purpose as per defined list values:

Allowed values:
- Home Improvement
- Appliance or Furniture
- Property

### investments — Performance Status

status of the loan performance based on transaction specific contractual definition as per defined list of values:

Allowed values:
- Performing
- In Delay
- Default
- Grace Period
- Full recovery
- Other

### investments — Repayment Status

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

### investments — Interest Rate Type

interest rate type as per defined list of values. Default value: Fixed Rate

Allowed values:
- Fixed Rate

### investments — Amortization Type

amortization type as per defined list of values. Default value: Fixed Payment

Allowed values:
- Fixed Payment
- Constant Principal
- Balloon Payments

### investments — Day Count Convention

day count convention as per defined list of values:

Allowed values:
- 30/360
- Act/360
- Act/365
- Act/Act

### investments — Principal Installment Frequency

scheduled frequency of the principal amount payment as per defined list of values. Default value: Monthly

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investments — Interest Installment Frequency

scheduled frequency of interest payments as per defined list of values. Default Value: Monthly

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investments — Hardship Flag

flag that indicates whether the loan is currently under a hardship arrangement.

Allowed values:
- True | False

### investments — Is Closed

Flag indicating whether the loan account has been fully closed/repaid.

Allowed values:
- True | False

### borrower — Bankruptcy Flag

Boolean indicator of whether the borrower has filed for bankruptcy.

Allowed values:
- True | False

### borrower — Bankruptcy Status

Current status of the bankruptcy proceeding (e.g. Filed, Active, Discharged, Dismissed).

Allowed values:
- Withdraw | Discharge | Reinstate | Filed | Dismiss | Confirm | Closed

### borrower — Primary Income Type

Nature of the borrower's primary income source (e.g. Salary, Self-Employed, Pension, Benefits).

Allowed values:
- Salary | Self-Employed | Pension | Benefits | Other

### borrower — Employment Status

Borrower's employment status at origination or as of reporting date (e.g. Full-Time, Part-Time, Unemployed).

Allowed values:
- Full-Time | Part-Time | Self-Employed | Unemployed | Retired

### cash_flows — Type

type of cash flow as per defined list of values.

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
