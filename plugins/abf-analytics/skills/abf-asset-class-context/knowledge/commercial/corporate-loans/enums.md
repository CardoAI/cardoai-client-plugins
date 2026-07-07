---
title: Commercial — Corporate Loans — Enum Vocabulary
tier: enums
enum_count: 10
---

# Commercial — Corporate Loans — Enum / Allowed Values

### investments — Performance Status

Current performance classification of the loan (e.g. Performing, Non-Performing, Defaulted, Watch-list).

Allowed values:
- Performing | In Delay | Default | Grace Period | Full recovery | In Stock  | Other

### investments — Performance Status Contractual

Performance status based strictly on contractual payment obligations, without applying any grace periods.

Allowed values:
- Performing |  In Delay | Default | Grace Period | Full recovery | In Stock | Other

### investments — Repayment Status

Indicates whether the loan is current, delinquent, in default, prepaid, or charged off.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Amortization Type

Amortization type as per defined list of values:

Allowed values:
- Fixed Payment | Constant Principal | Interest-Only Payments | Balloon Payments | Partial Interest-Only Payments | Graduated Increase Repayment | Graduated Decrease Repayment | Interest Accrual Period | Step-Up Repayment | Step-Down Repayment | Negative | Zero Coupon | Perpetual | BNPL (Pay-In-N) | BNPL (Pay-Later) | BNPL (Interest Bearing) | Installment Plan | Credit Cards | Charge Cards

### investments — Current Interest Rate Index

index to which the interest rate refers when it is variable/floating as per defined list of values

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

### investments — Current Interest Rate Index Tenor

type of interest rate tenor as per defined list of values

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

### investments — Pik Type

Payment-in-Kind type as per defined list of values:

Allowed values:
- Optional
- Full
- To Maturity
- Partial

### investments — Interest Installment Frequency

scheduled frequency of interest payments, as per defined list of values. Default Value: Monthly

Allowed values:
- Daily | Weekly | Monthly | Quarterly | Semi Annual | Annual | 28 Days | Bi-Weekly | Semi-Monthly | Bi-Monthly | Other

### borrower — Bankruptcy status

Bankruptcy status of the borrower, as per the pre-defined list of values:
 - Withdraw
 - Discharge
 - Reinstate
 - Filed
 - Dismiss
 - Confirm
 - Closed

Allowed values:
- - Withdraw
- - Discharge
- - Reinstate
- - Filed
- - Dismiss
- - Confirm
- - Closed

### borrower — employer_status

List:
- Employed - Private Sector
- Employed - Public Sector
- Employed - Sector Unknown
- Unemployed
- Self-employed
- Student
- Pensioner
- No Employment, Obligor is Legal Entity"
- Other

Allowed values:
- - Employed - Private Sector
- - Employed - Public Sector
- - Employed - Sector Unknown
- - Unemployed
- - Self-employed
- - Student
- - Pensioner
- - No Employment, Obligor is Legal Entity"
- - Other
