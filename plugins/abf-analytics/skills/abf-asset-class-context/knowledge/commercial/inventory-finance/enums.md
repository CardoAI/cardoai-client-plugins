---
title: Commercial — Inventory Finance — Enum Vocabulary
tier: enums
enum_count: 21
---

# Commercial — Inventory Finance — Enum / Allowed Values

### investments — Is Secured

Indicates whether a loan is secured or not.

Allowed values:
- True | False

### investments — Performance Status

Current performance classification of the asset.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full Recovery | In Stock | Other

### investments — Loan Status

Terminal repayment / resolution status of the loan.

Allowed values:
- Asset Sale | Fully Repaid | No Recovery | No Repayment | Partially Repaid | Repurchased | Write-off No Recovery | Write-off Partial Recovery

### investments — Repayment Status

Type of loan repayment status.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Prepaid | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Interest Rate Type

The type of interest rate applied to the loan.

Allowed values:
- Fixed | Floating | Variable

### investments — Current Interest Rate Index

The name of the reference rate (e.g. EURIBOR, LIBOR, SOFR) used to calculate the floating rate portion.

Allowed values:
- SOFR | EURIBOR | LIBOR | SONIA | Other

### investments — Current Interest Rate Index Tenor

The duration of the interest rate index (e.g. 1M, 3M, 6M), indicating how often the rate resets.

Allowed values:
- Overnight | 1 Month | 3 Month | 6 Month | 12 Month | Other

### investments — Amortisation Method

Method used to repay the loan (e.g. annuity, bullet, linear).

Allowed values:
- Annuity | Bullet | Linear | Interest Only | Other

### investments — Payment Frequency

Scheduled frequency of principal payments.

Allowed values:
- Monthly | Quarterly | Semi-Annually | Annually | Other

### investments — Interest Frequency

How often interest payments are due (e.g. monthly, quarterly).

Allowed values:
- Monthly | Quarterly | Semi-Annually | Annually | Other

### investments — Is Closed

Flag indicating whether the loan account has been fully closed / repaid.

Allowed values:
- True | False

### investments — Default Flag

Indicator showing whether the loan is in default.

Allowed values:
- True | False

### asset_modification_event — Loan Modified Flag

Indicates whether the loan has been modified.

Allowed values:
- True | False

### asset_modification_event — Modified Type

Type of modification applied to the loan.

Allowed values:
- Collateral Modification | Extension | Interest Rate Change | No Modification | Ope Legis Suspension | Partial Early Repayment | Payment Suspension | Principal Forgiveness | Principal Suspension | Renegotiation | Renegotiation With Extension | Rescheduling | Suspension With Extension | Suspension Without Extension

### collaterals — Category

Broader category of the inventory (e.g. perishable, seasonal, durable, fragile).

Allowed values:
- Perishable | Seasonal | Durable | Fragile | Other

### collaterals — Storage Location Type

Type of storage (e.g. warehouse, bonded warehouse, 3PL, seller-owned).

Allowed values:
- Warehouse | Bonded Warehouse | 3PL | Seller-Owned | Other

### collaterals — Third Party Verification

Indicates if a third-party audit or inspection has verified the inventory.

Allowed values:
- True | False

### collaterals — Concentration Risk Flag

Flag indicating whether a single inventory item or category represents more than a defined threshold (e.g. 20%) of the total collateral pool value — key eligibility criteria field.

Allowed values:
- True | False

### collaterals — Insurance Coverage Flag

Indicates if the inventory is insured.

Allowed values:
- True | False

### companies — Is Sole Proprietorship

Indicates if the company is a sole proprietorship.

Allowed values:
- True | False

### cash_flows — Type

type of cash flow as per defined list of values

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery
