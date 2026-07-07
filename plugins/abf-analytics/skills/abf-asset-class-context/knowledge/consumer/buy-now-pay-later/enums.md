---
title: Consumer — Buy Now Pay Later — Enum Vocabulary
tier: enums
enum_count: 12
---

# Consumer — Buy Now Pay Later — Enum / Allowed Values

### investments — Performance Status

Status of the loan performance based on transaction specific contractual definition as per defined list of values.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full recovery | In Stock | Other

### investments — Performance Status Contractual

Performance status based strictly on contractual payment obligations, without applying any grace periods.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full recovery | In Stock | Other

### investments — Repayment Status

Type of repayment status as per defined list.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Amortization Type

Describes the principal repayment structure (e.g. Fully Amortising, Bullet, Interest Only, Balloon).

Allowed values:
- Fixed Payment | Constant Principal | Interest-Only Payments | Balloon Payments | Partial Interest-Only Payments | Graduated Increase Repayment | Graduated Decrease Repayment | Interest Accrual Period | Step-Up Repayment | Step-Down Repayment | Negative | Zero Coupon | Perpetual | BNPL (Pay-In-N) | BNPL (Pay-Later) | BNPL (Interest Bearing) | Installment Plan | Credit Cards | Charge Cards

### investments — Scheduled Principal Payment Frequency

Frequency at which scheduled principal repayments are due (e.g. Monthly, Quarterly, Semi-Annual, Annual).

Allowed values:
- Daily | Weekly | Monthly | Quarterly | Semi Annual | Annual | 28 Days | Bi-Weekly | Semi-Monthly | Bi-Monthly | Other

### investments — Scheduled Interest Payment Frequency

Frequency at which scheduled interest payments are due.

Allowed values:
- Daily | Weekly | Monthly | Quarterly | Semi Annual | Annual | 28 Days | Bi-Weekly | Semi-Monthly | Bi-Monthly | Other

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
