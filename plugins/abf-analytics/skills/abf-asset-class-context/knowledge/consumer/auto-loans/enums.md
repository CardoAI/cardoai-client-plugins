---
title: Consumer — Auto Loans — Enum Vocabulary
tier: enums
enum_count: 19
---

# Consumer — Auto Loans — Enum / Allowed Values

### investmens — Financing Purpose

type of financing purpose as per defined list values:

Allowed values:
- New Car
- Used Car
- Other Vehicle

### investmens — Performance Status

status of the loan performance based on transaction specific contractual definition as per defined list of values:

Allowed values:
- Performing
- In Delay
- Default
- Grace Period
- Full recovery
- Other

### investmens — Repayment Status

type of repayment status as per defined list.

Allowed values:
- No Repayment
- Partially Repaid
- Fully Repaid
- Repurchased
- Prepaid
- Write-off Partial Recovery
- Write-off No Recovery
- Asset Sale
- No Recovery

### investmens — Days Count Convention

day count convention as per defined list of values:

Allowed values:
- 30/360
- Act/360
- Act/365
- Act/Act

### investmens — Amortization Type

amortization type as per defined list of values: Default: Fixed Payment

Allowed values:
- Fixed Payment
- Constant Principal
- Balloon Payments

### investmens — Principal Installment Frequency

scheduled frequency of the principal amount payment as per defined list of values. Default value: Monthly

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investmens — Interest Installment Frequency

scheduled frequency of the interest amount payment as per defined list of values. Default value: Monthly

Allowed values:
- Monthly
- Quarterly
- Semi-Annually
- Annually

### investmens — Is Closed

Flag indicating whether the loan account has been fully closed/repaid.

Allowed values:
- True | False

### borrower — Bankruptcy Flag

flag that indicates if the borrower is in bankruptcy

Allowed values:
- True | False

### borrower — Bankruptcy Status

bankruptcy status of the borrower, as per the defined list of values.

Allowed values:
- Withdraw | Discharge | Reinstate | Filed | Dismiss | Confirm | Closed

### borrower — Primary Income Type

primary income type of the borrower as per defined list of values.

Allowed values:
- Salary | Self-Employed | Pension | Benefits | Other

### borrower — Employment Status

employment status of the borrower as per defined list of values:

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

### borrower — Home Ownership

type of home ownership, as per defined list of values:

Allowed values:
- Owner
- Mortgage
- Rental
- Other

### borrower — Gender

gender of the invididual as per defined list of values

Allowed values:
- Male
- Female
- Other

### cash_flows — Type

type of cash flow as per defined list of values

Allowed values:
- General Repayment | Principal Repayment | Interest | Fee | Prepayment | Recovery

### collateral — Fuel Type

type of fuel consumed by the vehicle, as per defined list of values:

Allowed values:
- Gasoline
- Diesel
- Battery Electric
- Plug-in Hybrid
- Hybrid Electric
- Natural Gas  LPG
- Hybrid Diesel
- Hybrid Gasoline
- Other

### collateral — Condition

the current state of the vehicle, as per defined list of values:

Allowed values:
- Extra Clean
- Clean
- Average
- Rough
- Damaged

### collateral — Measurement Unit

the unit used to express the vehicle’s distance, selected from a predefined list of valid values:

Allowed values:
- miles
- kilometers

### collateral — Valuation Method

method used for the valuation as per defined list of values:

Allowed values:
- Full Appraisal
- Drive-by
- Automated Value Model
- Indexed
- Desktop
- Managing Agent or Estate Agent
- Purchase Price
- Haircut
- Mark to Market
- Obligor's valuation
- Other
