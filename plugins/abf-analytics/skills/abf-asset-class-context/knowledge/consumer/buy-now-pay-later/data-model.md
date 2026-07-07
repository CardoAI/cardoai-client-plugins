---
title: Consumer — Buy Now Pay Later — Data Model
main: consumer
sub: buy-now-pay-later
entities:
  - name: investments
    field_count: 66
  - name: borrower
    field_count: 24
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 5
---

# Consumer — Buy Now Pay Later — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 66 |  |
| `borrower` | 24 |  |
| `calculated` | 8 |  |
| `cash_flows` | 5 |  |

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset ID | string | Uid value that uniquely identifies the receivable within the originator's dat… |  |  |
| Reference Date | date | Data cut-off date. |  |  |
| Originator | string | Name of the originator of the loans. |  | ✓ |
| Issue Date | date | Date on which the receivable was issued. |  | ✓ |
| Purchased Principal Amount | amount | Outstanding principal balance at the time the loan was purchased into the pool. |  | ✓ |
| Currency ISO | string | Standardized ISO, three-letter currency code representing the currency of the… |  |  |
| Is Autopay | boolean | Flag indicating whether the borrower has enrolled in automatic payment proces… |  |  |
| Financing Purpose | string | Stated purpose for which the loan proceeds were used (e.g. auto, personal, ho… |  |  |
| Purchase Date | date | Date of receivable transfer to the SPV or pledge to the lender. |  |  |
| Purchase Price | amount | Price paid to acquire the loan, typically expressed as a percentage of par or… |  |  |
| Current Principal Balance | amount | Outstanding principal balance, remaining amount of the receivable that has no… |  |  |
| APR | percentage | Annual percentage rate (APR) is the yearly interest charged to borrowers or p… |  | ✓ |
| Deferred Security | boolean | Flag indicating whether there is any deferred interest for the asset. |  |  |
| Performance Status | string | Status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| Performance Status Contractual | string | Performance status based strictly on contractual payment obligations, without… | ✓ |  |
| DPD | integer | Number of days by which a scheduled or expected payment is overdue. |  | ✓ |
| Maturity Date | date | Current receivable maturity date. |  | ✓ |
| Maturity Date Original | date | Maturity date at origination, before any modification intervened. |  |  |
| Closing Date | date | Date on which the receivable is considered closed, with no further collection… |  |  |
| Repayment Status | string | Type of repayment status as per defined list. | ✓ |  |
| Current Interest Rate | percentage | Interest rate applicable to the loan as of the reporting date (annualised). |  |  |
| Amortization Type | string | Describes the principal repayment structure (e.g. Fully Amortising, Bullet, I… | ✓ |  |
| Accrual Start Date | date | Date when interest or fees begin to accrue on the asset. |  |  |
| Accrued Interest Amount | amount | Interest accrued on the outstanding principal balance but not yet collected a… |  |  |
| Accrued Interests At Pool Addition Date | amount | Accrued interest on the loan at the date it was added to the pool. |  |  |
| Interest In Delay | amount | Cumulative interest amount that is overdue/past due as of the reporting date. |  |  |
| Principal In Delay | amount | Total amount of principal that has not been paid by its respective due dates. |  |  |
| Next Payment Date | date | Date, as of the reporting date, on which the borrower's next contractual paym… |  |  |
| Last Payment Date | date | Date of the most recent payment made by the borrower. |  |  |
| Last Delay Date | date | Most recent date on which the loan was observed in a delinquent/delayed status. |  |  |
| First Delay Date | date | Date on which the borrower first failed to pay the amount due as expected. |  |  |
| Prepaid Date | date | Date of the last cash flow in case of borrower prepayment. |  |  |
| Periodical Prepaid Amount | amount | Amount prepaid during the current reporting period. |  |  |
| Prepaid Principal Amount | amount | Cumulative principal amount that has been prepaid over the life of the loan. |  | ✓ |
| Scheduled Principal Payment Frequency | string | Frequency at which scheduled principal repayments are due (e.g. Monthly, Quar… | ✓ |  |
| Scheduled Interest Payment Frequency | string | Frequency at which scheduled interest payments are due. | ✓ |  |
| Charge Off Date | date | Date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Principal Charge Off Amount | amount | Unpaid principal amount at default date as per contractual definition. |  |  |
| Interest Charge Off Amount | amount | Due and unpaid interest amount at default date as per contractual definition. |  |  |
| Payment Date | date | Date of the most recent payment received from the borrower. |  | ✓ |
| Scheduled Principal Amount | amount | Contractually scheduled principal repayment amount due in the current period. |  |  |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Gross Recovered Amount | amount | Total recovered amount, as of the reporting date. |  |  |
| Net Recovered Amount | amount | Total amount repaid post-default, net of collection costs. |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Country | string | Full country name of the borrower's primary residential address. |  |  |
| State | string | Region, state, or province of the borrower's primary residential address. |  | ✓ |
| Original Balance | amount | The total nominal (face) value of the receivable at the issue date. |  | ✓ |
| Loss Amount | amount | Total charge-off amount, net of recoveries, inclusive of both principal and i… |  | ✓ |
| Loss Date | date | Indicates the date the loss was recorded and the asset was written off. |  | ✓ |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Remaining Term Days | integer | Number of calendar days remaining until the current maturity date. |  |  |
| Remaining Term Years | integer | Number of years remaining until the current maturity date (fractional). |  |  |
| Asset Age Days | integer | Number of calendar days elapsed since the loan's issue date. |  |  |
| Asset Age Years | integer | Number of years elapsed since the loan's issue date (fractional). |  |  |
| Seller Merchant Code | string | Broad economic sector code classifying the borrower's industry or occupation … |  | ✓ |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed/repaid. | ✓ |  |
| Contractual Payment Amount Current | amount | Scheduled recurring amount the borrower must pay under the loan agreement, in… |  | ✓ |
| Contractual Payment Amount Original | amount | Scheduled recurring amount the borrower must pay under the loan agreement, in… |  |  |
| Sale Date | date | Date when the receivable was sold. |  |  |
| Sale Price | amount | Receivable sale or repurchase amount. |  |  |
| Is Fraud | boolean | Flag indicating whether the asset has been flagged as fraudulent. |  |  |
| Modification Date | date | Reporting date when the modification event occurred. |  |  |
| Modification End Date | date | Date when the modification event has concluded and the borrower has resumed t… |  |  |
| Modification Details | string | Additional details related to the event. |  |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | Unique identifier for the borrower entity within the originator or servicer s… |  |  |
| Bankruptcy Chapter | string | Chapter of bankruptcy filed by the borrower (e.g. Chapter 7, Chapter 13) wher… |  |  |
| Bankruptcy Date | date | Date on which the borrower filed for bankruptcy protection. |  |  |
| Bankruptcy Flag | boolean | Boolean indicator of whether the borrower has filed for bankruptcy. | ✓ |  |
| Bankruptcy Status | string | Current status of the bankruptcy proceeding (e.g. Filed, Active, Discharged, … | ✓ |  |
| Primary Income Type | string | Primary income type of the borrower as per defined list of values. | ✓ |  |
| Primary Income Amount | amount | Annual income of the borrower derived from their primary source of earnings. |  |  |
| FICO Score | integer | Borrower FICO credit score as of the reporting date. |  | ✓ |
| Original FICO Score | integer | Borrower's FICO credit score at the time of loan origination. |  |  |
| Originator Score | integer | Credit score of the borrower assigned by the originator as of the reporting d… |  |  |
| Originator Score Original | integer | Credit score of the borrower assigned by the originator as of the issue date. |  |  |
| PTI Current | percentage | Payment-to-income ratio, indicating the proportion of the borrower's income u… |  |  |
| PTI Original | percentage | Original payment-to-income ratio, indicating the proportion of the borrower's… |  |  |
| DTI Current | percentage | Debt-to-income ratio, indicating the proportion of the borrower's income used… |  |  |
| DTI Original | percentage | Original debt-to-income ratio, indicating the proportion of the borrower's in… |  |  |
| Employer Name | string | The name of the borrower's employer. |  |  |
| Employment Duration | string | Employment duration of the borrower in years. |  |  |
| Employment Status | string | Employment status of the borrower as per defined list of values. | ✓ |  |
| Employment Title | string | Job title or position of the borrower at origination. |  |  |
| Birth Year | integer | Borrower's year of birth. |  |  |
| Gender | string | Gender of the individual as per defined list of values. |  |  |
| Zip Code | string | Five digit zip code of the borrower at application time. |  |  |
| Total Debt | amount | Total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Total Debt Original | amount | Total amount of all short-term and long-term debts the individual owes, as of… |  |  |

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
| Total Recoveries | amount | Cumulative total of all recovery amounts collected over the life of the defau… |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Uid value that uniquely identifies the loan within the originator's database. |  | ✓ |
| Effective Amount | amount | Paid amount at the reference date. |  |  |
| Cashflow Reference Date | date | Date of the cash flow. |  |  |
| Type | string | Type of cash flow as per defined list of values. | ✓ | ✓ |
| Expected Amount | amount | Expected amount at the reference date. |  | ✓ |
