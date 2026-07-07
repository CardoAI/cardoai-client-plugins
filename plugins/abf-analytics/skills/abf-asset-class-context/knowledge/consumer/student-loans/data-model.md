---
title: Consumer — Student Loans — Data Model
main: consumer
sub: student-loans
entities:
  - name: investments
    field_count: 60
    raw_name: investmens
  - name: borrower
    field_count: 28
  - name: calculated
    field_count: 7
  - name: cash_flows
    field_count: 5
---

# Consumer — Student Loans — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 60 | *(source: `investmens`)*  |
| `borrower` | 28 |  |
| `calculated` | 7 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments` *(source: `investmens`)*

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | uid value that uniquely identifies the loan within the originator’s database. |  | ✓ |
| Reporting Date | date | The reference date of the reported data. |  | ✓ |
| Originator Name | string | Name of the originator of the loan |  | ✓ |
| Issue Date | date | date on which the loan was issued. |  | ✓ |
| Original Balance | amount | the total nominal (face) value of the loan at the issue date. |  | ✓ |
| Currency ISO | string | standardized ISO, three-letter currency code representing the currency of the… |  |  |
| Financing Purpose | string | Stated purpose for which the loan proceeds were used (e.g. auto, personal, ho… |  |  |
| Purchase Date | date | date of loan transfer to the SPV or pledge to the lender |  |  |
| Purchase Price | amount | price as % of the purchased principal amount paid to purchase the loan. |  |  |
| Purchased Principal | amount | total nominal amount of the loan that has been purchased or pledged, as of th… |  | ✓ |
| Current Principal Balance | amount | outstanding principal balance, remaining amount of the loan that has not yet … |  | ✓ |
| Apr | percentage | annual percentage rate (apr) is the yearly interest charged to borrowers or p… |  |  |
| Performance Status | string | status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| dpd | integer | number of days by which a scheduled or expected payment is overdue. |  |  |
| Maturity Date | date | current loan maturity date. |  | ✓ |
| Original Maturity Date | date | maturity date at origination, before any modification intervened. |  |  |
| Closing Date | date | date on which the loan is considered closed, with no further collection actio… |  |  |
| Repayment Status | string | type of repayment status as per defined list. | ✓ |  |
| Current Interest Rate | percentage | value of the interest rate applicable to the loan, whether fixed or floating,… |  |  |
| Amortization Type | string | amortization type as per defined list of values. Default value: Fixed Payment | ✓ |  |
| Accrued Interest Amount | amount | total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interests At Pool Addition Date | amount | Accrued interest on the loan at the date it was added to the pool. |  |  |
| Contractual Payment Amount Current | amount | scheduled recurring amount the borrower must pay under the loan agreement, in… |  | ✓ |
| Contractual Payment Amount Original | amount | scheduled recurring amount the borrower must pay under the loan agreement, in… |  |  |
| Interest In Delay | amount | total amount of interest that has not been paid by its respective due dates. |  |  |
| Principal In Delay | amount | total amount of principal that has not been paid by its respective due dates. |  |  |
| Next Payment Date | date | date, as of the reporting date, on which the borrower’s next contractual paym… |  |  |
| Last Delay Date | date | date of the most recent payment made by the borrower. |  |  |
| First Delay Date | date | date on which the borrower first failed to pay the amount due as expected. |  |  |
| Prepaid Date | date | date of the last cash flow in case of borrower prepayment. |  |  |
| Prepaid Amount | amount | total amount paid to fully close the outstanding balance of the loan. |  |  |
| Principal Installment Frequency | string | scheduled frequency of the principal amount payment as per defined list of va… | ✓ |  |
| Interest Installment Frequency | string | scheduled frequency of interest payments, as per defined list of values: | ✓ |  |
| Charge Off Date | date | date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Principal Charge Off Amount | amount | unpaid principal amount at default date as per contractual definition. |  |  |
| Interest Charge Off Amount | amount | due and unpaid interest amount at default date as per contractual definition.\ |  |  |
| Charge Off Reason | string | description or details of the loan that has been charged-off. |  |  |
| Loss Given Default | percentage | borrower’s expected loss in the event of default, measured as of the reportin… |  |  |
| Loss Amount | amount | total charge-off amount, net of recoveries, inclusive of both principal and i… |  | ✓ |
| Loss Date | date | Indicates the date the loss was recorded and the asset was written off. |  | ✓ |
| Net Recovered Amount | amount | total amount repaid post-default, net of collection costs. |  |  |
| Gross Recovered Amount | amount | total recovered amount, as of the reporting date. |  | ✓ |
| Net charge Off Amount | amount | total charge-off amount, net of recoveries, inclusive of both principal and i… |  |  |
| Recovery Amount | amount | Net recovery amount credited to the loan after deducting collection costs. |  | ✓ |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Hardship Amount | amount | Deferred or reduced payment amount associated with an active hardship/modific… |  |  |
| Hardship First Payment Date | date | Date of the first payment under the hardship or modification arrangement. |  |  |
| Hardship Flag | boolean | Boolean indicator of whether the borrower is currently on an active hardship … | ✓ |  |
| Hardship Last Payment Date | date | Date of the last scheduled payment under the current hardship plan. |  |  |
| Write Off Amount | amount | Total amount written off against the loan (principal + accrued interest + fees). |  |  |
| Write Off Date | date | Date on which the write-off was recorded. |  |  |
| Write Off Principal Amount | amount | Principal component of the total write-off amount. |  |  |
| Net Recovered Amount | amount | Recovery amount net of all associated collection and legal costs. |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Remaining Term (Days) | integer | Number of calendar days remaining until the current maturity date. |  |  |
| Remaining Term (Years) | integer | Number of years remaining until the current maturity date (fractional). |  |  |
| Asset Age (Days) | integer | Number of calendar days elapsed since the loan's issue date. |  |  |
| Asset Age (Years) | integer | Number of years elapsed since the loan's issue date (fractional). |  |  |
| Borrower Macro Sector Code | string | Broad economic sector code classifying the borrower's industry or occupation … |  |  |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed/repaid. | ✓ |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | uid type value unique identifier for the borrower within the database |  |  |
| Geography Iso Original | string | standardized geographic subdivision code representing the borrower’s state, p… |  |  |
| Bankruptcy Chapter | string | indicates the chapter of US bankruptcy law reference. |  |  |
| Bankruptcy Date | date | reference date of bankruptcy event. |  |  |
| Bankruptcy Flag | boolean | flag that indicates if the borrower is in bankruptcy. | ✓ |  |
| Bankruptcy Status | string | bankruptcy status of the borrower, as per the defined list of values. | ✓ |  |
| Primary Income Type | string | primary income type of the borrower as per defined list of values. | ✓ |  |
| Primary Income Amount | amount | annual income of the borrower derived from their primary source of earnings. |  |  |
| Fico Score | integer | fico credit score of the borrower, as of the reporting date. |  | ✓ |
| Fico Score Original | integer | original fico credit score of the borrower. |  |  |
| Vantage Score Original | string | vantage credit score of the borrower as of the issue date. |  |  |
| Vantage Score | string | vantage credit score of the borrower, as of the reporting date. |  |  |
| Employment Status | string | employment status of the borrower as per defined list of values. | ✓ |  |
| Employer Name | string | the name of the borrower’s employer. |  |  |
| Employment Title | string | job title or position of the borrower at origination |  |  |
| Employment Duration | string | employment duration of the borrower in years. |  |  |
| Original Pti | percentage | original payment-to-income ratio, indicating the proportion of the borrower's… |  |  |
| Pti | percentage | payment-to-income ratio, indicating the proportion of the borrower's income u… |  |  |
| Original Dti | percentage | original debt-to-income ratio, indicating the proportion of the borrower's in… |  |  |
| Dti | percentage | debt-to-income ratio, indicating the proportion of the borrower's income used… |  |  |
| Total Debt Original | integer | total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Total Debt | integer | total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| degree | string | The academic degree the borrower is enrolled in or has obtained (e.g. Bachelo… |  | ✓ |
| major | string | The borrower's primary field of academic study within their degree programme … |  |  |
| discipline_category | string | High-level grouping of the borrower's field of study into a broader academic … | ✓ |  |
| university_name | string | The name of the higher education institution the borrower attends or attended… |  |  |
| school_state | string | The state in which the borrower's institution is located. |  |  |
| study_level | string | The level of study the borrower is undertaking, indicating where they are in … | ✓ |  |

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

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | UID value that uniquely identifies the loan within the originator’s database. |  | ✓ |
| Realized Amount | amount | Actual cash amount received for the payment event (e.g. principal, interest, … |  | ✓ |
| Payment Date | date | Date on which the cash payment was received or posted by the servicer. |  | ✓ |
| Cash Flow Type | string | Classification of the cash flow received (e.g. General Repayment, Principal R… | ✓ |  |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
