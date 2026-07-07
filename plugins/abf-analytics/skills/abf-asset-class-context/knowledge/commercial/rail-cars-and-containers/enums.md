---
title: Commercial — Rail Cars And Containers — Enum Vocabulary
tier: enums
enum_count: 14
---

# Commercial — Rail Cars And Containers — Enum / Allowed Values

### regulatory — ACEP Program Flag

True if the container is enrolled in the ACEP continuous examination programme.

Allowed values:
- True | False

### regulatory — Hazmat Approved Flag

Whether the asset is approved for hazardous materials transport.

Allowed values:
- True | False

### regulatory — Regulatory Compliance Status

Current regulatory compliance classification.

Allowed values:
- Compliant | Due Soon | Overdue | Restricted

### investments — Performance Status

Current performance classification of the asset.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full Recovery | In Stock | Other

### investments — Repayment Status

Terminal repayment / resolution status of the loan.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Prepaid | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### lease — Lease Type

Classification of the lease structure.

Allowed values:
- Operating Lease | Master Lease | Per Diem | Trip Lease | Short-Term | Long-Term

### lease — Rent Payment Frequency

Frequency of rental payments.

Allowed values:
- Daily | Weekly | Monthly | Other

### lease — Maintenance Responsibility

Party responsible for maintenance and repair costs under the lease.

Allowed values:
- Lessor | Lessee | Shared

### operations — Asset Status

Current operational status of the asset.

Allowed values:
- On-Lease | Off-Lease | In Transit | In Depot | Under Repair | Lost/Stolen | Scrapped

### operations — Loaded Flag

True if the asset is currently loaded.

Allowed values:
- True | False

### maintenance — Last Inspection Date

Date of last inspection (AAR/CSC).

Allowed values:
- IICL | Cargo Worthy | Wind & Water Tight | As-Is

### maintenance — Next Inspection Due Date

Next scheduled inspection due date.

Allowed values:
- Up-to-date | Due Soon | Overdue | In Shop

### maintenance — Repair Date

Date of last repair.

Allowed values:
- Running Repair | Heavy Shop | Damage | Wreck | Cosmetic | Other

### cash_flows — Type

type of cash flow as per defined list of values

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
