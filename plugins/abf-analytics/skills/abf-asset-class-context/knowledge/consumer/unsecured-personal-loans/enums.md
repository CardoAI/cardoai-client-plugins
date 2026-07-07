---
title: Consumer — Unsecured Personal Loans — Enum Vocabulary
tier: enums
enum_count: 20
---

# Consumer — Unsecured Personal Loans — Enum / Allowed Values

### investments — Financing Purpose

Type of financing purpose as per defined list values.

Allowed values:
- Home Improvement
- Medical
- Living Expenses  Tuition
- Appliance or Furniture
- Travel
- Debt Consolidation
- New Car
- Used Car
- Other Vehicle
- Equipment
- Property
- Other

### investments — Performance Status

Status of the loan performance based on transaction specific contractual definition as per defined list of values.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full recovery | In Stock  | Other

### investments — Performance Status Contractual

Status of the loan performance based on transaction specific contractual definition as per defined list of values.

Allowed values:
- Performing |  In Delay | Default | Grace Period | Full recovery | In Stock | Other

### investments — Repayment Status

Type of repayment status as per defined list.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Interest Rate Type

Interest rate type as per defined list of values. Default value: Fixed Rate.

Allowed values:
- Floating rate underlying exposure (for life)
- Floating rate underlying exposure linked to one index that will revert to another index in the future
- Fixed rate underlying exposure (for life)
- Fixed with future periodic resets
- Fixed rate underlying exposure with compulsory future switch to floating
- Floating rate underlying exposure with floor
- Floating rate underlying exposure with cap)
- Floating rate underlying exposure with both floor
- Other
- Fixed Rate

### investments — Current Interest Rate Index Tenor

Type of interest rate tenor as per defined list of values.

Allowed values:
- Overnight
- IntraDay
- 1 day
- 1 week
- 2 week
- 1 month
- 2 month
- 3 month
- 4 month
- 6 month
- 12 month
- On Demand
- Other

### investments — Current Interest Rate Index

Index to which the interest rate refers when it is variable/floating as per defined list of values.

Allowed values:
- SOFR
- Treasury
- LIBOR (USD)
- LIBID (USD)
- EURODOLLAR
- SWAP (USD)
- FutureSWAP (USD)
- ISDAFIX (USD)
- GCFRepo
- MuniAAA
- Lender's Own Rate
- Other
- Euribor
- EONIA
- European Central Bank Base Rate
- Bank of England Base Rate
- SONIA (UK)

### investments — Days Count Convention

Days count convention as per defined list of values.

Allowed values:
- 30/360
- Act/360
- Act/365
- Act/Act

### investments — Amortization Type

Amortization type as per defined list of values. Default value: Fixed Payment.

Allowed values:
- Fixed Payment
- Constant Principal
- Interest-Only Payments
- Balloon Payments
- Partial Interest-Only Payments

### investments — Principal Installment Frequency

Scheduled frequency of the principal amount payment as per defined list of values. Default value: Monthly.

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investments — Interest Installment Frequency

Scheduled frequency of interest payments, as per defined list of values. Default value: Monthly.

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investments — Hardship Flag

Flag that indicates whether the loan is currently under a hardship arrangement.

Allowed values:
- True | False

### investments — Is Closed

Flag indicating whether the loan account has been fully closed/repaid.

Allowed values:
- True | False

### borrower — Bankruptcy Flag

Flag that indicates if the borrower is in bankruptcy.

Allowed values:
- True | False

### borrower — Bankruptcy Status

Bankruptcy status of the borrower, as per the defined list of values.

Allowed values:
- Withdraw
- Discharge
- Reinstate
- Filed
- Dismiss
- Confirm
- Closed

### borrower — Primary Income Type

Primary income type of the borrower as per defined list of values.

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

Employment status of the borrower as per defined list of values.

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

### borrower — Gender

Gender of the borrower (as per list of values).

Allowed values:
- Male
- Female
- Other

### borrower — Home Ownership

Type of home ownership, as per defined list of values.

Allowed values:
- Owner
- Mortgage
- Rental
- Other

### cash_flows — Type

Type of cash flow as per defined list of values.

Allowed values:
- Funding
- Principal Repayment
- Interest Repayment
- General Repayment
- Repurchase
- Funding Adjustment
- Repayment Adjustment
- Fees
- Prepayment Fees
- Late Fees
- Commission
- Recovery
- Recovery Capital
- Recovery Interest
- Prepayment
- Funding Rejected
- Funding Repaid
- Accounting Write Off
- Rollover
- Indemnity / Giveback
- Loan Sale
- Insurance Repayment
- Escrow Repayment
- Sale Commissions
- Selling Costs
- Interest Repayment Adjustment
- Recovery Fees
- Other
