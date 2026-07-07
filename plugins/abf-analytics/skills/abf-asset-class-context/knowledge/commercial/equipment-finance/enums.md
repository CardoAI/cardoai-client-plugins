---
title: Commercial — Equipment Finance — Enum Vocabulary
tier: enums
enum_count: 16
---

# Commercial — Equipment Finance — Enum / Allowed Values

### investments — Equipment Contract Type

Type of contract.

Allowed values:
- Lease | TRAC Lease | Loan | Sale and Leaseback | Hire Purchase | Other

### investments — Asset Category

Classification of the asset.

Allowed values:
- Equipment | Auto | Aircraft | Marine | Other

### investments — Repayment Structure

Repayment structure of the contract.

Allowed values:
- Amortizing | Bullet | Interest Only | Balloon | Other

### investments — Installment Frequency

Scheduled frequency of principal payments.

Allowed values:
- Monthly | Quarterly | Semi-Annually | Annually | Other

### investments — Has Balloon Payment

Indicates if a balloon payment is required.

Allowed values:
- True | False

### investments — Guarantee Class

Type of guarantee involved.

Allowed values:
- Full | Limited | None

### investments — Status

Performance status of the loan based on transaction-specific contractual definition.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full Recovery | Other

### investments — Repayment Status

Terminal repayment / resolution status of the contract.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Prepaid | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Is Closed

Flag indicating whether the contract has been fully closed / repaid.

Allowed values:
- True | False

### ppc_milestones — Milestone Status

Completion status of the milestone.

Allowed values:
- Pending | Completed | Overdue | Disputed

### equipment — Equipment Condition

Current condition of the asset.

Allowed values:
- New | Used | Refurbished | Damaged

### equipment — Maintenance State

Current status of the asset's maintenance.

Allowed values:
- Up To Date | Due Soon | Overdue | In Shop

### borrower — Enterprise Size

Size category of the enterprise (e.g. micro, SME, large).

Allowed values:
- Micro | Small | Medium | Large

### borrower — Bankruptcy Flag

Flag indicating if the debtor is currently in bankruptcy.

Allowed values:
- True | False

### borrower — Bankruptcy Status

Bankruptcy status of the debtor.

Allowed values:
- Withdraw | Discharge | Reinstate | Filed | Dismiss | Confirm | Closed

### cash_flows — Type

type of cash flow as per defined list of values

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
