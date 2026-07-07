---
title: Commercial — Corporate Loans — Data Model
main: commercial
sub: corporate-loans
entities:
  - name: investments
    field_count: 67
  - name: borrower
    field_count: 12
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 6
---

# Commercial — Corporate Loans — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 67 |  |
| `borrower` | 12 |  |
| `calculated` | 8 |  |
| `cash_flows` | 6 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Payment Date` ↔ `investments.Payment Date`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | uid value that uniquely identifies the loan within the originator’s database. |  | ✓ |
| Reporting Date | date | Snapshot/cut-off date to which all figures in this record refer. |  | ✓ |
| Originator Name | string | Legal name of the entity that originated the loan. |  | ✓ |
| Issue Date | date | Date on which the loan was originally disbursed/drawn. |  | ✓ |
| Purchased Principal | amount | total nominal amount of the loan that has been purchased or pledged, as of th… |  | ✓ |
| Commitment Current | amount | notional principal amount committed by a lender into the loan or facility, as… |  |  |
| Global Commitment Current | amount | total notional amount contractually committed by all lenders to the facility … |  |  |
| Funded Amount | amount | nominal principal amount of the facility outstanding (excluding undrawn commi… |  |  |
| Commitment Fees | percentage | Total fee charged by a lender to a borrower for the undrawn portion of a comm… |  |  |
| Origination Fee Percentage | percentage | the percentage of the loan amount charged as a fee by the lender or originato… |  |  |
| Exp Settlement Date | date | The expected loan settlement date |  |  |
| Asset Currency Abbreviation | string | ISO 4217 three-letter code for the currency in which the loan is denominated … |  |  |
| Financing Purpose | string | Stated purpose for which the loan proceeds were used (e.g. auto, personal, ho… |  | ✓ |
| Settlement Date | date | date of loan transfer to the SPV or pledge to the lender |  |  |
| Purchase Price | amount | Price paid to acquire the loan, typically expressed as a percentage of par or… |  |  |
| Current Principal Balance | amount | Outstanding principal balance of the loan as of the reporting date. |  | ✓ |
| Apr | percentage | Annual Percentage Rate the all-in annualised cost of the loan including inter… |  |  |
| Performance Status | string | Current performance classification of the loan (e.g. Performing, Non-Performi… | ✓ |  |
| Performance Status Contractual | string | Performance status based strictly on contractual payment obligations, without… | ✓ |  |
| DPD | integer | number of days by which a scheduled or expected payment is overdue. |  | ✓ |
| Maturity Date | date | Current contractual final maturity date of the loan (may differ from original… |  | ✓ |
| Maturity Date Original | date | Original contractual final maturity date at the time of origination. |  |  |
| Closing Date | date | Date on which the loan agreement was legally executed and closed. |  |  |
| Repayment Status | string | Indicates whether the loan is current, delinquent, in default, prepaid, or ch… | ✓ |  |
| Amortization Type | string | Amortization type as per defined list of values: | ✓ | ✓ |
| Ballon Amount | amount | The final lump sum payment due at the end of the asset term if applicable. |  |  |
| Current Interest Rate | percentage | value of the interest rate applicable to the loan, whether fixed or floating,… |  |  |
| Current Index | percentage | current value of the index rate, which constitutes the floating component of … |  |  |
| Current Interest Rate Index | string | index to which the interest rate refers when it is variable/floating as per d… | ✓ |  |
| Current Interest Rate Index Tenor | string | type of interest rate tenor as per defined list of values | ✓ |  |
| Current Interest Rate Margin | percentage | value of interest rate margin (spread) for floating rates; for fixed rates, i… |  |  |
| Index Valuation Date | date | reference date of the interest rate index. |  |  |
| Interest Rate Cap | percentage | maximum interest rate that can be applied to a floating-rate financial instru… |  |  |
| Interest Rate Floor | percentage | minimum interest rate that can be applied to a floating-rate financial instru… |  |  |
| Accrued Interest Amount | amount | total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interests At Pool Addition Date | amount | Accrued interest on the loan at the date it was added to the pool. |  |  |
| Pik Rate | percentage | interest rate applied to a loan where interest is accrued and added to the pr… |  |  |
| Pik Type | string | Payment-in-Kind type as per defined list of values: | ✓ |  |
| Pik Amount | amount | cumulative value of all payments made in kind, as of the reporting date |  |  |
| First Expected Payment Date | date | scheduled date when the first payment is expected, as of the issue date. |  |  |
| Interest In Delay | amount | total amount of interest that has not been paid by its respective due dates. |  |  |
| Principal In Delay | amount | total amount of principal that has not been paid by its respective due dates. |  |  |
| Next Payment Date | date | Scheduled date of the next contractual payment. |  |  |
| Last Payment Date | date | date of the most recent payment made by the borrower. |  |  |
| First Delay Date | date | date on which the borrower first failed to pay the amount due as expected. |  |  |
| Last Delay Date | date | latest date in which the loan was in delay |  |  |
| Prepaid Date | date | date of the last cash flow in case of borrower prepayment. |  |  |
| Prepaid Amount | amount | total amount paid to fully close the outstanding balance of the loan. |  |  |
| Interest Installment Frequency | string | scheduled frequency of interest payments, as per defined list of values. Defa… | ✓ |  |
| Sale Price | date | Loan sale or repurchase price as % of par |  |  |
| Sale Date | date | Date when the loan was sold |  |  |
| Charge Off Date | date | date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Principal Charge Off Amount | amount | unpaid principal amount at default date as per contractual definition |  |  |
| Interest Charge Off Amount | amount | due and unpaid interest amount at default date as per contractual definition |  |  |
| Gross Recovered Amount | amount | total recovered amount, as of the reporting date. |  | ✓ |
| Net Recovered Amount | amount | total amount repaid post-default, net of collection costs. |  |  |
| Modification Date | date | reporting date when the modification event occurred |  |  |
| Modification End Date | date | date when the modification event has concluded and the borrower has resumed t… |  |  |
| Modification Details | string | additional details related to the event |  |  |
| Payment Date | date | Date of the most recent payment received from the borrower. |  | ✓ |
| Scheduled Principal Amount | amount | Contractually scheduled principal repayment amount due in the current period. |  |  |
| Loss Given Default | percentage | borrower’s expected loss in the event of default, measured as of the reportin… |  |  |
| Loss Amount | amount | total charge-off amount, net of recoveries, inclusive of both principal and i… |  | ✓ |
| Loss Date | date | Date in which the asset was written off. |  | ✓ |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Recovery Amount | amount | Net recovery amount credited to the loan after deducting collection costs. |  | ✓ |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID |  | UID type value unique identifier for the company borrower |  |  |
| Primary Income | string | Annual income of the Borrower |  |  |
| Total debt | string | Total borrower debts |  |  |
| dti | string | The current debt-to-income ratio, indicating the proportion of the borrower's… |  |  |
| pti | date | Payment-to-Income ratio, indicating the proportion of the Debtor's income use… |  |  |
| Fico score | integer | Current FICO credit score of the Borrower |  |  |
| State | date | Borrower’s original State |  | ✓ |
| Is deceased | percentage | Indicates whether the Borrower is deceased |  |  |
| Bankruptcy status | string | Bankruptcy status of the borrower, as per the pre-defined list of values:  - … | ✓ |  |
| employer_status | string | List: - Employed - Private Sector - Employed - Public Sector - Employed - Sec… | ✓ |  |
| employment_title | string | The job title or role held by the borrower at their current place of employment. |  |  |
| employment_duration | integer | The anticipated or contractual length of the borrower's future employment wit… |  |  |

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
| Lease ID | string | Unique identifier of the lease within the database, as reported by the Origin… |  |  |
| Payment Date | date | Date when a payment is processed and recorded in the system. |  | ✓ |
| CF Type | string | Type of cash flow as per defined list of values |  |  |
| Effective Amount | amount | Paid amount at the Reference Date. |  |  |
| Expected Amount | amount | Total amount expected to be paid by the borrower on the scheduled due date. |  | ✓ |
| Currency | string | Abbreviation of the original lease currency in which amounts are denominated … |  |  |
