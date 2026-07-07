---
title: Commercial — Ecommerce Finance — Enum Vocabulary
tier: enums
enum_count: 9
---

# Commercial — Ecommerce Finance — Enum / Allowed Values

### investments — Repayment Structure

Daily holdback %, revenue share %, fixed daily debit

Allowed values:
- Daily Holdback % | Revenue Share % | Fixed Daily Debit | Amortising | Bullet | Other

### investments — Installment Frequency

Scheduled frequency of payments.

Allowed values:
- Daily | Weekly | Monthly | Quarterly | Semi-Annual | Annual | Other

### investments — Performance Status

Performance status of the loan based on transaction specific contractual definition

Allowed values:
- Performing | In Delay | Default | Grace Period | Full Recovery | Written Off | Other

### investments — Repayment Status

Type of loan repayment status, as per defined listed of values: 
- no_repayment
- partially_repaid
- fully_repaid
- repurchased
- prepaid
- write_off_partial_recovery
- write_off_no_recovery
- asset_sale
- no_recovery

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Prepaid | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Is closed

Field that indicates if the loan is still open

Allowed values:
- True | False

### investments — Default Flag

Boolean indicator of whether the facility is currently classified as in default.

Allowed values:
- True | False

### investments — Is Closed

Boolean flag indicating whether the facility has been fully closed.

Allowed values:
- True | False

### borrower — Is Sole Proprietorship

Indicates if the company is a sole proprietorship (yes/no).

Allowed values:
- True | False

### cash_flows — Type

type of cash flow as per defined list of values

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
