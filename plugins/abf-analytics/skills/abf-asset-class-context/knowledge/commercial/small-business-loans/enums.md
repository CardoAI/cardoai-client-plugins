---
title: Commercial — Small Business Loans — Enum Vocabulary
tier: enums
enum_count: 22
---

# Commercial — Small Business Loans — Enum / Allowed Values

### investments — Current Interest Rate Index Tenor

Type of interest rate tenor as per defined list of values.

Allowed values:
- Overnight | IntraDay | 1 Day | 1 Week | 2 Week | 1 Month | 2 Month | 3 Month | 4 Month | 6 Month | 12 Month | On Demand | Other

### investments — Current Interest Rate Index

Index to which the interest rate refers when it is variable / floating.

Allowed values:
- SOFR | Treasury | LIBOR (USD) | LIBID (USD) | EURODOLLAR | SWAP (USD) | FutureSWAP (USD) | ISDAFIX (USD) | GCFRepo | MuniAAA | Lender's Own Rate | Euribor | EONIA | European Central Bank Base Rate | Bank of England Base Rate | SONIA (UK) | Other

### investments — Amortization Type

Amortization type as per defined list of values.

Allowed values:
- Fixed Payment | Constant Principal | Interest-Only Payments | Balloon Payments | Partial Interest-Only Payments

### investments — Interest Installment Frequency

Scheduled frequency of interest payments.

Allowed values:
- Monthly | Quarterly | Semi-Annually | Annually

### investments — Payment Frequency

Scheduled frequency of principal repayments.

Allowed values:
- Monthly | Quarterly | Semi-Annually | Annually | Other

### investments — Is Closed

Flag indicating whether the loan account has been fully closed / repaid.

Allowed values:
- True | False

### investments — Performance Status

Status of the loan performance based on transaction-specific contractual definition.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full Recovery | Other

### investments — Performance Status Contractual

Performance status based strictly on contractual payment obligations, without applying any grace periods.

Allowed values:
- Performing | In Delay | Default | Grace Period | Full Recovery | Other

### investments — Repayment Status

Type of repayment status as per defined list.

Allowed values:
- No Repayment | Partially Repaid | Fully Repaid | Repurchased | Prepaid | Write-off Partial Recovery | Write-off No Recovery | Asset Sale | No Recovery

### investments — Seniority Type

Classification or level of seniority assigned to the financial asset within the capital structure.

Allowed values:
- Senior Secured | Secured | Senior Unsecured | Subordinated | Mezzanine | Junior Secured | Junior Subordinated | Junior Unsecured | Super Priority | Preferred Equity | Equity

### investments — Lien Type

Lien position of the loan or instrument in the capital structure.

Allowed values:
- 1st Lien | 2nd Lien | 3rd Lien | 1st Lien – First Out | 1st Lien - Last Out | Other | N/A

### investments — Deferred Flag

Flag indicating whether there is any deferred interest for the asset.

Allowed values:
- True | False

### investments — Modification Type

Type of modification applied to the loan.

Allowed values:
- Extension | Interest Rate Change | No Modification | Partial Early Repayment | Payment Suspension | Principal Forgiveness | Principal Suspension | Renegotiation | Renegotiation With Extension | Rescheduling | Suspension With Extension | Suspension Without Extension | Other

### asset_modification — Loan Modified Flag

Indicates whether the loan has been modified.

Allowed values:
- True | False

### asset_modification — Modified Type

Type of modification applied to the loan.

Allowed values:
- Extension | Interest Rate Change | No Modification | Partial Early Repayment | Payment Suspension | Principal Forgiveness | Principal Suspension | Renegotiation | Renegotiation With Extension | Rescheduling | Suspension With Extension | Suspension Without Extension | Other

### borrower — Enterprise Size

Size category of the enterprise (e.g. micro, SME, large).

Allowed values:
- Micro | Small | Medium | Large

### borrower — Bankruptcy Flag

Flag indicating if the borrower is currently in bankruptcy.

Allowed values:
- True | False

### borrower — Bankruptcy Status

Bankruptcy status of the borrower.

Allowed values:
- Withdraw | Discharge | Reinstate | Filed | Dismiss | Confirm | Closed

### borrower — Guarantor Flag

Indicates whether a personal or corporate guarantor is in place for the loan. Common in SBL where the principal owner provides a personal guarantee.

Allowed values:
- True | False

### borrower — Guarantor Type

Type of guarantee supporting the loan.

Allowed values:
- Personal Guarantee | Corporate Guarantee | Government Guarantee | Partial Guarantee | None

### borrower — Government Guarantee Flag

Indicates whether the loan benefits from a government-backed guarantee scheme (e.g. SBA 7(a), UKGBS). Key eligibility and loss mitigation field for SBL pools.

Allowed values:
- True | False

### cash_flows — Type

Type of cash flow as per defined list of values.

Allowed values:
- Funding | Principal Repayment | Interest Repayment | General Repayment | Repurchase | Funding Adjustment | Repayment Adjustment | Fees | Prepayment Fees | Late Fees | Commission | Recovery Capital | Prepayment | Funding Rejected | Funding Repaid | Accounting Write Off | Rollover | Indemnity / Giveback | Loan Sale | Insurance Repayment | Escrow Repayment | Sale Commissions | Selling Costs | Interest Repayment Adjustment | Recovery Fees | Other
