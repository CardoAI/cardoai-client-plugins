---
title: Commercial — Leasing Finance — Enum Vocabulary
tier: enums
enum_count: 8
---

# Commercial — Leasing Finance — Enum / Allowed Values

### investments — Performance Status

Field that indicates if the loan is still open

Allowed values:
- Performing | In Delay | Default | Grace Period | Full recovery | In Stock  | Other

### investments — Contractual Performance Status

Performance status of the loan based on transaction specific contractual definition

Allowed values:
- Performing |  In Delay | Default | Grace Period | Full recovery | In Stock | Other

### investments — Repayment status

Type of loan repayment status, as per defined listed of values:

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

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

### cash_flows — Cash Flow Type

Classification of the cash flow received (e.g. General Repayment, Principal Repayment, Interest, Fee).

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
