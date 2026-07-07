---
title: Commercial — Leasing Finance — Data Model
main: commercial
sub: leasing-finance
entities:
  - name: investments
    field_count: 46
  - name: borrower
    field_count: 19
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 9
---

# Commercial — Leasing Finance — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 46 |  |
| `borrower` | 19 |  |
| `calculated` | 8 |  |
| `cash_flows` | 9 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Issue Date` ↔ `investments.Issue Date`
- `borrower.Originator Identifier` ↔ `investments.Originator Identifier`
- `cash_flows.Reporting Date` ↔ `investments.Reporting Date`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Originator Identifier | string | Unique identifier of the loan within the database, as reported by the Origina… |  |  |
| Reporting Date | date | Snapshot/cut-off date to which all figures in this record refer. |  | ✓ |
| Originator Name | string | Legal name of the entity that originated the loan. |  | ✓ |
| Issue Date | date | Date on which the loan was issued |  | ✓ |
| Start date | date | The date when the first payment was made |  |  |
| Last Payment date | date | The date when the most recent payment was made |  |  |
| Maturity Date | date | Current maturity date (as of the Reporting Date) |  | ✓ |
| Original Maturity Date | date | Original contractual final maturity date at the time of origination, before a… |  |  |
| Outstanding balance | double | Unpaid Principal Balance as of Reporting Date, remaining amount of the loan t… |  |  |
| Purchase amount | double | Total loan principal amount purchased by the SPV or pledged by the Borrower |  |  |
| Issue amout | double | Total amount of the loan as of Issue Date (include undrawn portion, if any) |  |  |
| Accrued Interest | amount | Interest accrued on the outstanding balance but not yet collected as of the r… |  |  |
| Accrued Interest At Pool Addition Date | amount | Interest accrued but not yet paid when the loan entered the securitization pool. |  |  |
| Write off date | date | Date in which the loan was recorded as loss |  |  |
| Write off amount | double | Total cumulative amount recorded as loss |  |  |
| Default date | date | The date when the loan has been declared charged-off |  |  |
| Contractual Default date | date | The date when the loan has been declared charged-off |  |  |
| Defaulted Principal amount | double | Unpaid Principal amount at charge-off date as per contractual definition |  |  |
| Contractual Defaulted Principal amount | double | Unpaid Principal amount at charge-off date as per contractual definition |  |  |
| is closed | boolean | Flag indicating whether the loan account has been fully closed / repaid. |  |  |
| DPD | integer | Day past due, indicating the days of delay on any expected cash flow (not on … |  | ✓ |
| Remaining term | integer | The number of months between the Current Maturity Date and the Reporting Date |  | ✓ |
| Performance Status | string | Field that indicates if the loan is still open | ✓ |  |
| Contractual Performance Status | string | Performance status of the loan based on transaction specific contractual defi… | ✓ |  |
| Repayment status | string | Type of loan repayment status, as per defined listed of values: | ✓ |  |
| monthly payment principal | string | Scheduled frequency of principal payments. |  |  |
| monthly payment interst | string | Scheduled frequency of interest payments. |  |  |
| original_term_reported | integer | The number of months between the Current Maturity Date and the Issue Date |  |  |
| Baloon amount | double | The final lump sum payment due at the end of a loan or lease term. |  |  |
| Dealer Account name | string | The name of the dealership or vendor entity associated with the transaction o… |  |  |
| Asset | string | The type or category of the financed asset or product (e.g., vehicle, machine… |  | ✓ |
| Gross Invoice amount | double | The total invoice value before any deductions such as discounts or rebates; i… |  |  |
| Net Invoice amount | double | The invoice amount after all applicable deductions, such as discounts or reba… |  |  |
| Rpa cost | double | The revised or adjusted cost of the Retail Price Adjustment (RPA), factoring … |  |  |
| Net Rpa cost | double | The final RPA cost after applying discounts or adjustments, representing the … |  |  |
| Contract price | double | The full value of the contract, including base price, financing charges, fees… |  |  |
| Currency | string | Unique identifier for the currency in which the amount is denominated. |  |  |
| rating | amount | The most recent credit rating assigned to the borrower |  |  |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, a… |  |  |
| Gross Recovered Amount | amount | Total gross proceeds recovered before deducting recovery costs and expenses. |  | ✓ |
| Net Recovered Amount | amount | Net recovery amount credited to the asset after deducting all collection and … |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| State | string | the state of the borrower |  | ✓ |
| Country | string | the country of the borrower |  |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Pti | percentage | Payment-to-Income ratio: borrower's scheduled loan payment divided by verifie… |  |  |
| Bankruptcy Chapter | string | Chapter of bankruptcy filed by the borrower (e.g. Chapter 7, Chapter 13) wher… |  |  |
| Bankruptcy Date | date | Date on which the borrower filed for bankruptcy protection. |  |  |
| Bankruptcy Flag | boolean | Boolean indicator of whether the borrower has filed for bankruptcy. | ✓ |  |
| Bankruptcy Status | string | Current status of the bankruptcy proceeding (e.g. Filed, Active, Discharged, … | ✓ |  |
| Primary Income Type | string | Nature of the borrower's primary income source (e.g. Salary, Self-Employed, P… | ✓ |  |
| Primary Income Amount | amount | Verified annual gross income from the borrower's primary income source. |  |  |
| Original Pti | percentage | Payment-to-Income ratio calculated at origination using the original loan pay… |  |  |
| Dti | percentage | Debt-to-Income ratio: borrower's total monthly debt obligations divided by gr… |  |  |
| Original Dti | percentage | Debt-to-Income ratio as calculated at the time of loan origination. |  |  |
| Employer Name | string | Name of the borrower's primary employer. |  |  |
| Employment Duration | string | Length of time the borrower has been employed with the current employer (in m… |  |  |
| Employment Status | string | Borrower's employment status at origination or as of reporting date (e.g. Ful… | ✓ |  |
| Employment Title | string | Job title or occupation of the borrower. |  |  |
| Original Fico Score | integer | Borrower's FICO credit score at the time of loan origination. |  |  |
| Originator Identifier | string | Unique code or ID assigned to the originating institution within the platform. |  |  |
| Originator Score | integer | Internal credit score assigned by the originator as of the reporting date. |  |  |
| Originator Score Original | integer | Internal credit score assigned by the originator at the time of origination. |  |  |
| Borrower Id | string | Unique identifier for the borrower entity within the originator or servicer s… |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Mob Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| Mob Cgl | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| Mob Netloss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| Remaining Term (months) | integer | Number of months remaining until the current maturity date. |  |  |
| Loan Term | integer | Total contractual term of the loan expressed in months from origination to sc… |  | ✓ |
| Mob Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |
| Asset Age (months) | integer | Age of the loan expressed in whole months elapsed since the issue date. |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset Identifier | string | Unique identifier for the loan or asset within the servicer/originator system. |  |  |
| Realized Amount | amount | Actual cash amount received for the payment event (e.g. principal, interest, … |  | ✓ |
| Payment Date | date | Date on which the cash payment was received or posted by the servicer. |  | ✓ |
| Cash Flow Type | string | Classification of the cash flow received (e.g. General Repayment, Principal R… | ✓ |  |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
| Issue Date | date | Original date on which the underlying loan or asset was originated/issued. |  | ✓ |
| Pool Addition Date | date | Date on which the asset was added to the securitisation or funding pool. |  |  |
| Total Funding | amount | Total funded/committed amount for the underlying asset at origination or pool… |  |  |
| Reporting Date | date | Cut-off date to which all figures and statuses in this record refer. |  | ✓ |
