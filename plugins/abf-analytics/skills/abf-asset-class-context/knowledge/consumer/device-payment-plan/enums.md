---
title: Consumer — Device Payment Plan — Enum Vocabulary
tier: enums
enum_count: 14
---

# Consumer — Device Payment Plan — Enum / Allowed Values

### investments — Repayment Status

Current repayment classification of the loan.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Prepaid | Write Off Partial Recovery | Write Off No Recovery | Asset Sale | No Recovery

### investments — Performance Status

Current operational status of the asset within the portfolio.

Allowed values:
- Performing | In Debt Collection | In Stock | Sold | Lost and Written Off

### investments — Status

Boolean flag indicating whether the loan is still open and active.

Allowed values:
- True | False

### investments — Is Sold

Boolean flag indicating whether the asset has been sold and is no longer under portfolio ownership.

Allowed values:
- True | False

### subscription — Rental Plan

Frequency at which the subscription payment is due (e.g. monthly, quarterly, semi-annual, annual).

Allowed values:
- Monthly | 3 Months | 6 Months | 12 Months | Other

### subscription — Performance Status

Performance status of the subscription based on transaction-specific contractual definitions.

Allowed values:
- Performing | Delinquent | Default | Prepaid | Written Off | Other

### subscription — Customer Type

Type of customer renting the device/asset.

Allowed values:
- B2B | B2C

### subscription — Is Prepaid

Boolean flag indicating whether the subscription was settled before the anticipated maturity date.

Allowed values:
- True | False

### subscription — Status

Boolean flag indicating whether the subscription is still open and active.

Allowed values:
- True | False

### borrower — Employment

Employment status of the borrower.

Allowed values:
- Employed | Self-Employed | Unemployed | Retired | Student | Other

### borrower — Gender

Gender of the borrower.

Allowed values:
- Male | Female | Other | Not Disclosed

### equipment — Asset Condition

Condition of the asset at the moment of purchase.

Allowed values:
- New | Used | Refurbished

### equipment — Asset Category

Main category group of the physical asset (e.g. Mobile, Computing, Audio-Visual).

Allowed values:
- Mobile | Computing | Wearable | Audio-Visual | Gaming | Other

### cash_flows — CashFlow Type

Classification of the cash flow received (e.g. General Repayment, Principal Repayment, Interest, Fee).

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
