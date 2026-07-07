---
title: Consumer — Auto Loans — Data Model
main: consumer
sub: auto-loans
entities:
  - name: investments
    field_count: 63
    raw_name: investmens
  - name: borrower
    field_count: 30
  - name: calculated
    field_count: 9
  - name: cash_flows
    field_count: 5
  - name: collateral
    field_count: 23
---

# Consumer — Auto Loans — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 63 | *(source: `investmens`)*  |
| `borrower` | 30 |  |
| `calculated` | 9 |  |
| `cash_flows` | 5 |  |
| `collateral` | 23 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments` *(source: `investmens`)*

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | uid value that uniquely identifies the loan within the originator’s database |  | ✓ |
| Reporting Date | date | Snapshot/cut-off date to which all figures in this record refer. |  | ✓ |
| Originator | string | name of the originator of the loans. |  | ✓ |
| Issue Date | date | date on which the loan was issued. |  | ✓ |
| Original Balance | amount | the total nominal (face) value of the loan at the issue date. |  | ✓ |
| Currency Iso | string | standardized ISO, three-letter currency code representing the currency of the… |  |  |
| Financing Purpose | string | type of financing purpose as per defined list values: | ✓ |  |
| Original Ltv | percentage | loan-to-value (ltv) at origination. |  | ✓ |
| Purchase Date | date | date of loan transfer ot the spv or pledge to the lender |  |  |
| Purchased Principal | amount | Total principal amount of the loan added to the collateral pool of the transa… |  | ✓ |
| Purchase Price | percentage | price as % of the purchased principal amount paid to purchase the loan. |  |  |
| UPB | amount | unpaid principal balance, remaining amount of the loan that has not yet been … |  | ✓ |
| APR | percentage | annual percentage rate (apr) is the yearly interest charged to borrowers or p… |  | ✓ |
| Performance Status | string | status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| DPD | integer | number of days by which a scheduled or expected payment is overdue. |  | ✓ |
| LTV | percentage | loan-to-value (LTV) as of the reporting date |  | ✓ |
| Maturity Date Original | date | maturity date at origination, before any modification intervened. |  |  |
| Maturity Date | date | current loan maturity date. |  | ✓ |
| Closing Date | date | date on which the loan is considered closed, with no further collection actio… |  |  |
| Repayment Status | string | type of repayment status as per defined list. | ✓ |  |
| Current Interest Rate | percentage | value of the interest rate applicable to the loan, whether fixed or floating,… |  |  |
| Days Count Convention | string | day count convention as per defined list of values: | ✓ |  |
| Amortization Type | string | amortization type as per defined list of values: Default: Fixed Payment | ✓ |  |
| Accrued Interest Amount | amount | total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interests At Pool Addition Date | amount | total accrued interest at the pool addition date |  |  |
| Interest In Delay | amount | total amount of interest that has not been repaid as of the most recent sched… |  |  |
| Principal In Delay | amount | total amount of principal that has not been paid by its respective due dates. |  |  |
| Next Payment Date | date | date, as of the reporting date, on which the borrower’s next contractual paym… |  |  |
| Contractual Payment Amount Current | amount | scheduled recurring amount the borrower must pay under the loan agreement, in… |  | ✓ |
| Contractual Payment Amount Original | amount | scheduled recurring amount the borrower must pay under the loan agreement, in… |  |  |
| Last Payment Date | date | date of the most recent payment made by the borrower. |  |  |
| First Delay Date | date | date on which the borrower first failed to pay the amount due as expected. |  |  |
| Last Delay Date | date | latest date in which the loan was in delay |  |  |
| Prepaid Date | date | date of the last cash flow in case of borrower prepayment. |  |  |
| Prepaid Amount | amount | total amount paid to fully close the outstanding balance of the loan. |  |  |
| Principal Installment Frequency | string | scheduled frequency of the principal amount payment as per defined list of va… | ✓ |  |
| Interest Installment Frequency | string | scheduled frequency of the interest amount payment as per defined list of val… | ✓ |  |
| Sale Date | date | date when the loan was sold. |  |  |
| Sale Price | percentage | loan sale or repurchase amount |  |  |
| Charge Off Date | date | date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Charge Off Reason | string | description or details of the loan that has been written off. |  |  |
| Principal Charge Off Amount | amount | unpaid principal amount at default date as per contractual definition |  |  |
| Interest Charge Off Amount | amount | due and unpaid interest amount at default date as per contractual definition |  |  |
| Gross Recovered Amount | amount | total recovered amount, as of the reporting date. |  | ✓ |
| Net Recovered Amount | amount | total recovered amount net of collection costs, as of the reporting date. |  |  |
| Loss Amount | amount | total charge-off amount, net of recoveries, inclusive of both principal and i… |  | ✓ |
| Loss Date | date | Indicates the date the loss was recorded and the asset was written off. |  | ✓ |
| Modification Date | date | reporting date when the modification event occurred |  |  |
| Modification End Date | date | date when the most recent modification event has concluded and the borrower h… |  |  |
| Modification Details | string | additional details related to the event |  |  |
| Originator rating original | string | rating or credit score of the loan assigned by the originator as of the issue… |  |  |
| Originator Rating | string | rating or credit score of the loan assigned by the originator as of the repor… |  |  |
| Loss Given Default | amount | borrower’s expected loss in the event of default, measured as of the reportin… |  |  |
| Hardship Amount | amount | loan current principal balance amount currently under a hardship arrangement,… |  |  |
| Hardship Flag | boolean | flag that indicates whether the loan is currently under a hardship arrangement |  |  |
| Hardship First Payment Date | date | the date when the borrower's first payment under the hardship arrangement was… |  |  |
| Hardship Last Payment Date | date | the date when the most recent payment was made under the hardship arrangement |  |  |
| Remaining Term (Years) | integer | Number of years remaining until the current maturity date (fractional). |  |  |
| Asset Age (Days) | integer | Number of calendar days elapsed since the loan's issue date. |  |  |
| Asset Age (Years) | integer | Number of years elapsed since the loan's issue date (fractional). |  |  |
| Borrower Macro Sector Code | string | Broad economic sector code classifying the borrower's industry or occupation … |  |  |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed/repaid. | ✓ |  |
| Original LTV | percentage | Specifically refers to the LTV captured at the time of origination, as oppose… |  | ✓ |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | uid type value unique identifier for the borrower within the database |  |  |
| Pti Current | percentage | payment-to-income ratio, indicating the proportion of the borrower's income u… |  |  |
| Bankruptcy Chapter | string | indicates the chapter of us bankruptcy law reference. |  |  |
| Bankruptcy Date | date | reference date of bankruptcy event. |  |  |
| Bankruptcy Flag | boolean | flag that indicates if the borrower is in bankruptcy | ✓ |  |
| Bankruptcy Status | string | bankruptcy status of the borrower, as per the defined list of values. | ✓ |  |
| Primary Income Type | string | primary income type of the borrower as per defined list of values. | ✓ |  |
| Primary Income Amount | amount | annual income of the borrower derived from their primary source of earnings. |  |  |
| Fico Score | string | fico credit score of the borrower, as of the reporting date. |  | ✓ |
| Fico Score Original | string | original fico credit score of the borrower. |  |  |
| Pti Original | percentage | original payment-to-income ratio, indicating the proportion of the borrower's… |  |  |
| Dti Current | percentage | debt-to-income ratio, indicating the proportion of the borrower's income used… |  |  |
| Dti Original | percentage | original debt-to-income ratio, indicating the proportion of the borrower's in… |  |  |
| Employer Name | string | the name of the borrower’s employer. |  |  |
| Employment Duration | string | employment duration of the borrower in years. |  |  |
| Employment Status | string | employment status of the borrower as per defined list of values: | ✓ |  |
| Employment Title | string | the current job title or position of the borrower. |  |  |
| Original Fico Score | string | original fico credit score of the borrower. |  |  |
| Originator Score | string | credit score of the borrower assigned by the originator as of the reporting date |  |  |
| Originator Score Original | string | credit score of the borrower assigned by the originator as of the issue date |  |  |
| Vantage Score | string | vantage credit score of the borrower, as of the reporting date. |  |  |
| Vantage Score Original | string | vantage credit score of the borrower as of the issue date. |  |  |
| Total Debt Original | amount | total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Total Debt Original | amount | the total amount of all short-term and long-term debts the individual owes |  |  |
| Home Ownership | string | type of home ownership, as per defined list of values: | ✓ |  |
| State | string | the state of the borrower |  | ✓ |
| Country | string | the country of the borrower |  |  |
| Birth Year | string | borrower's birth year. |  |  |
| Gender | string | gender of the invididual as per defined list of values | ✓ |  |
| Zip Code | string | five digit zip code of the borrower at application time. |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Mob Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| Mob Cgl | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| Mob Netloss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| Remaining Term (months) | integer | Number of months remaining until the current maturity date. |  |  |
| Asset Age (months) | integer | Number of months elapsed since the loan's issue date (fractional). |  |  |
| Recovery Date | date | date when the recovery amount was made |  | ✓ |
| Loan Term | integer | Total contractual term of the loan expressed in months from origination to sc… |  | ✓ |
| Mob Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | double | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | uid value that uniquely identifies the loan within the originator’s database. |  | ✓ |
| CF Reference Date | date | date when the borrower made the payment. |  |  |
| Type | string | type of cash flow as per defined list of values | ✓ | ✓ |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
| Effective Amount | amount | paid amount at the reference date. |  |  |

### `collateral`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Vehicle ID | string | uid value that uniquely identifies the vehicle within the originator’s database. |  |  |
| Vin | string | vehicle identification number - as provided by the oem |  |  |
| Book Value At Purchase | amount | the recorded value of the vehicle at the time of purchase, before any depreci… |  |  |
| Registration Date | date | the date on which the vehicle was officially registered. |  |  |
| Book Value At Purchase | amount | the book value of the vehicle, as of the reporting date, after accounting for… |  |  |
| Model | string | the vehicle model |  | ✓ |
| Fuel Type | string | type of fuel consumed by the vehicle, as per defined list of values: | ✓ |  |
| Condition | string | the current state of the vehicle, as per defined list of values: | ✓ | ✓ |
| Vehicle Color | string | the exterior color of the vehicle, as specified by the manufacturer or regist… |  |  |
| Energy Performance Certificate Value | string | the value of the vehicle as reported by the certificate provider, as of the r… |  |  |
| Energy Performance Certificate Provider Name | string | the full legal name of the valuation provider certificate provider. |  |  |
| Measurement Unit | string | the unit used to express the vehicle’s distance, selected from a predefined l… | ✓ |  |
| Distance Original | double | the total distance the vehicle had traveled at the time of purchase. |  |  |
| Distance | double | the total distance covered by the vehicle, as of the reporting date. |  | ✓ |
| Manufacturer | string | original equipment manufacturer  – the name of the vehicle manufacturer. |  |  |
| Manufacturer ID | string | uid type value unique identifier of the manufacturer that produced a physical… |  |  |
| Vehicle Depreciation | amount | the cumulative depreciation expense recognized for the vehicle as of the repo… |  |  |
| Depreciation Percentage | amount | the percentage rate, over the depreciation frequency, at which the vehicle is… |  |  |
| Depreciation Frequency | amount | the period at which depreciation is applied to the vehicle over its estimated… |  |  |
| Valuation Method | string | method used for the valuation as per defined list of values: | ✓ |  |
| Valuation Amount | amount | the estimated monetary value of the vehicle as of the valuation date. |  |  |
| Valuation Date | date | vehicle's valuation date |  |  |
| Category | string | vehicle's category as of reporting date |  | ✓ |
