---
title: Consumer — Unsecured Personal Loans — Data Model
main: consumer
sub: unsecured-personal-loans
entities:
  - name: investments
    field_count: 75
  - name: borrower
    field_count: 28
  - name: calculated
    field_count: 9
  - name: cash_flows
    field_count: 5
---

# Consumer — Unsecured Personal Loans — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 75 |  |
| `borrower` | 28 |  |
| `calculated` | 9 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Uid value that uniquely identifies the loan within the originator's database. |  | ✓ |
| Reference Date | date | Data cut-off date. |  |  |
| Originator | string | Name of the originator of the loan. |  | ✓ |
| Issue Date | date | Date on which the loan was issued. |  | ✓ |
| Purchased Principal | amount | Total nominal (par) amount of the loan that has been purchased or pledged, as… |  | ✓ |
| Currency ISO | string | Three-letter currency code (standardized ISO) representing the currency of th… |  |  |
| Financing Purpose | string | Type of financing purpose as per defined list values. | ✓ |  |
| Purchase Date | date | Date of loan transfer to the SPV or pledge to the lender. |  |  |
| Purchase Price | amount | Price as % of par paid to purchase the loan. |  |  |
| Current Principal Balance | amount | Outstanding principal balance, remaining amount of the loan that has not yet … |  |  |
| APR | percentage | Annual percentage rate (APR) is the yearly interest charged to borrowers or p… |  | ✓ |
| Performance Status | string | Status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| Performance Status Contractual | string | Status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| DPD | integer | Number of days by which a scheduled or expected payment is overdue. |  | ✓ |
| Maturity Date | date | Current loan maturity date. |  | ✓ |
| Maturity Date Original | date | Maturity date at origination, before any modification intervened. |  |  |
| Closing Date | date | Date on which the loan is considered closed, with no further collection actio… |  |  |
| Repayment Status | string | Type of repayment status as per defined list. | ✓ |  |
| Current Interest Rate | percentage | Value of the interest rate applicable to the loan, whether fixed (coupon) or … |  |  |
| Interest Rate Type | string | Interest rate type as per defined list of values. Default value: Fixed Rate. | ✓ |  |
| Current Interest Rate Margin | percentage | Value of interest rate margin (spread) for floating rates; not applicable in … |  |  |
| Current Index | percentage | Current value of the index rate applicable to floating rates. |  |  |
| Index Valuation Date | date | Reference date of the current index value. |  |  |
| Current Interest Rate Index Tenor | string | Type of interest rate tenor as per defined list of values. | ✓ |  |
| Current Interest Rate Index | string | Index to which the interest rate refers when it is variable/floating as per d… | ✓ |  |
| Interest Rate Cap | percentage | Maximum interest rate that can be applied (floating rates only). |  |  |
| Interest Rate Floor | percentage | The minimum interest rate that can be applied to a floating-rate financial in… |  |  |
| Days Count Convention | string | Days count convention as per defined list of values. | ✓ |  |
| Amortization Type | string | Amortization type as per defined list of values. Default value: Fixed Payment. | ✓ |  |
| Accrued Interest Amount | amount | Total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interests At Pool Addition Date | amount | Accrued interest on the loan at the date it was added to the pool. |  |  |
| Interest In Delay | amount | Total amount of interest that has not been paid on due dates. |  |  |
| Principal In Delay | amount | Total amount of principal that has not been paid on due dates. |  |  |
| Next Payment Date | date | Date, as of the reporting date, on which the borrower's next contractual paym… |  |  |
| Last Delay Date | date | Latest date in which the loan was in delay. |  |  |
| First Delay Date | date | Date of the last cash flow in case of borrower prepayment. |  |  |
| Prepaid Date | date | Date on which the loan was fully or partially prepaid ahead of schedule. |  |  |
| Periodical Prepaid Amount | amount | Amount prepaid during the current reporting period. |  |  |
| Prepaid Amount | amount | Total amount paid to fully close the outstanding balance of the loan. |  |  |
| Contractual Payment Amount Current | amount | Scheduled recurring amount the borrower must pay under the loan agreement, in… |  | ✓ |
| Contractual Payment Amount Original | amount | Scheduled recurring amount the borrower must pay under the loan agreement, in… |  |  |
| Principal Installment Frequency | string | Scheduled frequency of the principal amount payment as per defined list of va… | ✓ |  |
| Interest Installment Frequency | string | Scheduled frequency of interest payments, as per defined list of values. Defa… | ✓ |  |
| Last Payment Date | date | Date of the most recent payment received from the borrower. |  |  |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Gross Recovered Amount | amount | Total recovered amount, as of the reporting date. |  |  |
| Net Recovered Amount | amount | Total amount repaid post-default, net of collection costs. |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Hardship Amount | amount | Loan current principal balance amount currently under a hardship arrangement,… |  |  |
| Hardship First Payment Date | date | Date when the borrower's first payment under the hardship arrangement was sch… |  |  |
| Hardship Flag | boolean | Flag that indicates whether the loan is currently under a hardship arrangement. | ✓ |  |
| Hardship Last Payment Date | date | The date when the most recent payment was made under the hardship arrangement. |  |  |
| Country | string | Full country name of the borrower's primary residential address. |  |  |
| State | string | Region, state, or province of the borrower's primary residential address. |  | ✓ |
| Original Balance | amount | The total nominal (par) value of the loan at the issue date. |  | ✓ |
| Write Off Amount | amount | Total amount written off against the loan (principal + accrued interest + fees). |  |  |
| Write Off Date | date | Date on which the write-off was recorded. |  |  |
| Write Off Principal Amount | amount | Principal component of the total write-off amount. |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Remaining Term Days | integer | Number of calendar days remaining until the current maturity date. |  |  |
| Remaining Term Years | integer | Number of years remaining until the current maturity date (fractional). |  |  |
| Asset Age Days | integer | Number of calendar days elapsed since the loan's issue date. |  |  |
| Asset Age Years | integer | Number of years elapsed since the loan's issue date (fractional). |  |  |
| Seller Merchant Code | string | Broad economic sector code classifying the seller's industry or occupation (e… |  | ✓ |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed/repaid. | ✓ |  |
| Charge Off Date | date | Date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Charge Off Reason | string | Description or details of the loan that has been charged-off. |  |  |
| Principal Charge Off Amount | amount | Unpaid principal amount at default date as per contractual definition |  |  |
| Interest Charge Off Amount | amount | Due and unpaid interest amount at default date as per contractual definition |  |  |
| Modification Date | date | Reporting date when the modification event occurred |  |  |
| Modification End Date | date | Date when the event ends in case type is equal to principal suspension |  |  |
| Modification Type | string | Type of the modification made to the asset. |  |  |
| Sale Date | date | date on which the loan was repurchased or sold |  |  |
| Sale Price | amount | loan sale or repurchase price as % of par |  |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Bankruptcy Chapter | string | Indicates the chapter of US bankruptcy law reference. |  |  |
| Bankruptcy Date | date | Reference date of bankruptcy event. |  |  |
| Bankruptcy Flag | boolean | Flag that indicates if the borrower is in bankruptcy. | ✓ |  |
| Bankruptcy Status | string | Bankruptcy status of the borrower, as per the defined list of values. | ✓ |  |
| Primary Income Type | string | Primary income type of the borrower as per defined list of values. | ✓ |  |
| Primary Income Amount | amount | Annual income of the borrower derived from their primary source of earnings. |  |  |
| PTI Current | percentage | Payment-to-income ratio, indicating the proportion of the borrower's income u… |  |  |
| PTI Original | percentage | Original payment-to-income ratio, indicating the proportion of the borrower's… |  |  |
| DTI Current | percentage | Debt-to-income ratio, indicating the proportion of the borrower's income used… |  |  |
| DTI Original | percentage | Original debt-to-income ratio, indicating the proportion of the borrower's in… |  |  |
| Employer Name | string | The name of the borrower's employer. |  |  |
| Employment Duration | string | Employment duration of the borrower in years. |  |  |
| Employment Status | string | Employment status of the borrower as per defined list of values. | ✓ |  |
| Employment Title | string | Job title or position of the borrower at origination. |  |  |
| FICO Score | integer | FICO credit score of the borrower, as of the reporting date. |  | ✓ |
| FICO Score Original | integer | FICO credit score of the borrower as of the issue date. |  |  |
| Originator Identifier | string | Unique code or ID assigned to the originating institution within the platform. |  |  |
| Originator Score | integer | Credit score of the borrower assigned by the originator as of the reporting d… |  |  |
| Originator Score Original | integer | Credit score of the borrower assigned by the originator as of the issue date. |  |  |
| Borrower ID | string | Uid type value unique identifier for the borrower within the database. |  |  |
| Birth Year | integer | Borrower's year of birth. |  |  |
| Gender | string | Gender of the borrower (as per list of values). | ✓ |  |
| Zip Code | string | Five digit zip code of the borrower at application time. |  |  |
| Total Debt Original | amount | Total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Total Debt | amount | Total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Home Ownership | string | Type of home ownership, as per defined list of values. | ✓ |  |
| Deceased Flag | boolean | Indicates whether the borrower is deceased. |  |  |
| Deceased Date | date | Borrower's deceased date. |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| MOB Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| MOB CGL | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| MOB Net Loss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| Remaining Term Months | integer | Number of months remaining until the current maturity date. |  |  |
| Loan Term | integer | Total contractual term of the loan expressed in months from origination to sc… |  | ✓ |
| MOB Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |
| Asset Age Months | integer | Age of the loan expressed in whole months elapsed since the issue date. |  |  |
| Total Recoveries | amount | Cumulative total of all recovery amounts collected over the life of the defau… |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Uid value that uniquely identifies the loan within the originator's database. |  | ✓ |
| Effective Amount | amount | Paid amount at the reference date. |  |  |
| CF Reference Date | date | Date of the cash flow. |  |  |
| Type | string | Type of cash flow as per defined list of values. | ✓ | ✓ |
| Expected Amount | amount | Expected amount at the reference date. |  | ✓ |
