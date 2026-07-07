---
title: Commercial — Revenue Based Finance — Data Model
main: commercial
sub: revenue-based-finance
entities:
  - name: investments
    field_count: 68
  - name: asset_modification
    field_count: 5
  - name: borrower
    field_count: 45
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 5
---

# Commercial — Revenue Based Finance — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 68 |  |
| `asset_modification` | 5 |  |
| `borrower` | 45 |  |
| `calculated` | 8 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Unique identifier of the loan within the database, as reported by the Origina… |  | ✓ |
| Originator Name | string | Originator name related to the specific loan. |  |  |
| Reporting Date | date | Snapshot / cut-off date to which all figures in this record refer. |  | ✓ |
| Issue Date | date | Date on which the loan was issued. |  | ✓ |
| Pool Addition Date | date | Date when the loan has been transferred to the SPV or pledged. |  |  |
| Loan Currency | string | Unique identifier for the currency in which the amount is denominated. |  |  |
| Loan Amount | amount | Total amount of the loan as of Issue Date (including undrawn portion, if any). |  |  |
| Purchased Principal | amount | Total loan principal amount purchased by the SPV or pledged by the Borrower. |  | ✓ |
| Loan Price | percentage | Price at which the loan was acquired into the securitization pool, expressed … |  |  |
| Upfront Fees | amount | Fees charged at loan origination, typically one-time and paid by the borrower. |  |  |
| Loan Current Balance | amount | Unpaid principal balance as of the Reporting Date — remaining amount of the l… |  | ✓ |
| Accrued Interest Amount | amount | Total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interest At Pool Addition Date | amount | Interest accrued but not yet paid when the loan entered the securitisation pool. |  |  |
| Revenue Share Percentage | percentage | Agreed percentage of the borrower's revenue that is used to repay the investm… |  |  |
| Cap Multiplier | double | Contractual multiplier used to calculate the repayment cap (e.g. 1.3× means t… |  |  |
| Repayment Cap Amount | amount | Maximum amount the borrower is obligated to repay, calculated as issue amount… |  |  |
| Min Monthly Payment | amount | Minimum payment applied — serves as a floor that protects the lender if reven… |  |  |
| Max Monthly Payment | amount | Maximum payment applied — serves as an optional ceiling for borrower predicta… |  |  |
| Sales Reporting Frequency | string | How often the borrower is required to report revenue (e.g. monthly, quarterly). | ✓ | ✓ |
| Sales Reported Period Start | date | Start date of the revenue reporting period. |  |  |
| Sales Reported Period End | date | End date of the revenue reporting period. |  |  |
| Repayment Cap Reached Flag | boolean | Indicates whether the repayment cap has been reached on this loan. | ✓ |  |
| Implied Effective Rate | percentage | Implied annualised effective rate based on the cap multiplier and actual repa… |  |  |
| Loan Purpose | string | Purpose of the loan as per defined list of values. | ✓ |  |
| Amortisation Method | string | Method used to repay the loan (e.g. annuity, bullet, linear). | ✓ |  |
| Payment Frequency | string | Scheduled frequency of principal payments. | ✓ |  |
| Original Term | double | Total length of the loan from origination to maturity. |  |  |
| Estimated Remaining Term | integer | The number of months between the Current Maturity Date and the Reporting Date. |  |  |
| First Payment Date | date | Date the borrower made or is scheduled to make the first loan payment. |  |  |
| Last Payment Date | date | Most recent payment date recorded before reporting or default. |  |  |
| Projected Payoff Date | date | Original maturity date. |  |  |
| Current Payoff Date | date | Current maturity date as of the Reporting Date. |  |  |
| Closing Date | date | Date on which the investment was closed (repaid, prepaid, written-off, declar… |  |  |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed / repaid. | ✓ | ✓ |
| Installment Amount | amount | Scheduled payment amount combining principal and other fees. |  |  |
| Installment Capital Amount | amount | Scheduled principal (capital) portion of the expected revenue. |  | ✓ |
| Installment Capital Amount Realized | amount | Actual principal received from the borrower in the reporting period, based on… |  |  |
| Performance Status | string | Performance status of the loan based on transaction-specific contractual defi… | ✓ |  |
| Performance Status Contractual | string | Performance status based strictly on contractual payment obligations, without… | ✓ |  |
| RBF Status | string | Terminal repayment / resolution status of the loan. | ✓ |  |
| Days In Delay | integer | Days past due — indicating the days of delay on any expected cash flow, calcu… |  |  |
| Arrears Balance | amount | Total overdue amount on the loan, including both principal, interest, and fees. |  |  |
| Arrears Balance Capital | amount | Portion of the arrears that relates specifically to overdue principal (capita… |  |  |
| Interest In Delay | amount | Total amount of interest that has not been paid by its respective due dates. |  |  |
| First Delay Date | date | Earliest date on which the loan first entered a delinquent / delayed status. |  |  |
| Last Delay Date | date | Most recent date on which the loan was observed in a delinquent / delayed sta… |  |  |
| Default Flag | boolean | Indicator showing whether the loan is in default. | ✓ |  |
| Default Date | date | Date the loan was classified as in default. |  |  |
| Amount Default Date Principal | amount | Unpaid principal amount at charge-off date as per contractual definition. |  |  |
| Write Off Date | date | Date on which the loan was recorded as a loss. |  |  |
| Write Off Amount | amount | Total cumulative amount recorded as loss. |  |  |
| Write Off Principal Amount | amount | Principal component of the total write-off amount. |  |  |
| Interest Charge Off Amount | amount | Due and unpaid interest amount at charge-off date as per contractual definition. |  |  |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |
| Gross Recovered Amount | amount | Total gross proceeds recovered before deducting recovery costs and expenses. |  |  |
| Net Recovered Amount | amount | Total amount repaid post-default, net of collection costs. |  |  |
| Recovery Collected Amount | amount | Total cash collected through recovery activities in the current reporting per… |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Recovery Date | date | Date of the most recent recovery payment or collection. |  | ✓ |
| Principal Prepayment | amount | Cumulative principal amount prepaid (including all payments made before the c… |  |  |
| Prepayment Fee | amount | Fee charged to the borrower for repaying the loan early. |  |  |
| Prepaid Date | date | For loans prepaid, the date on which the loan has been paid in full. |  |  |
| Date Of Repurchase | date | Date on which the loan was repurchased. |  |  |
| Repurchase Amount | amount | The amount that the originator or seller agrees to pay to buy back a loan fro… |  |  |
| Loan Rating | string | The credit rating assigned to the loan or borrower (e.g. BBB, Ba2). |  |  |
| Loan Rating Date | date | The date when the rating was issued or last updated. |  |  |
| Loan Rating Source | string | The agency or internal model that provided the rating (e.g. Moody's, internal… |  |  |
| Loan Rating Rank | integer | Indicates the priority or reliability of the rating when multiple ratings exi… |  |  |

### `asset_modification`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan Modified Flag | boolean | Indicates whether the loan has been modified. | ✓ |  |
| Modified Date | date | Date when the modification was implemented. |  |  |
| Modified Type | string | Type of modification applied to the loan. | ✓ |  |
| Modification Reason | string | Reason for the change (e.g. borrower hardship, restructuring, COVID-related). |  |  |
| Modification End Date | date | End date of the modification period, if temporary. |  |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | Unique identifier of the borrower within the database. |  |  |
| Company Group ID | string | Identifier for the company group the entity belongs to. |  |  |
| Company Tax Code | string | Company's national tax identification code. |  |  |
| Company Name | string | Registered legal name of the company. |  |  |
| Company Country | string | Country where the company is legally registered. |  |  |
| Company Region | string | Geographical region of the company's registration. |  |  |
| Province | string | Province or local administrative area of the company. |  |  |
| Company Founding Date | date | Date when the company was legally established. |  |  |
| Company Legal Form | string | Legal structure of the company (e.g. LLC, S.A., GmbH). |  |  |
| Company N Employees | integer | Number of employees working for the company. |  |  |
| Company Address Code | string | Code representing the company's address (postal or internal). |  |  |
| Company Website | string | URL of the company's official website. |  |  |
| Company Type | string | General classification of the company (e.g. parent, subsidiary). |  |  |
| Enterprise Size | string | Size category of the enterprise (e.g. micro, SME, large). | ✓ | ✓ |
| Company Sector Code | string | Code indicating the sector / industry the company operates in. |  |  |
| Insurer Name | string | Name of the insurance company covering the business. |  |  |
| Insurance Score | string | Credit or risk score assigned by the insurer. |  | ✓ |
| Is Sole Proprietorship | boolean | Indicates if the company is a sole proprietorship. | ✓ |  |
| Company Risk Score | string | Quantitative measure of the company's overall risk. |  | ✓ |
| Company Risk Score Source | string | Source that provided the risk score. |  |  |
| Company Risk Score Update Date | date | Date when the risk score was last updated. |  |  |
| Company PD | double | Probability of default for the company. |  |  |
| Company PD Source | string | Source that provided the probability of default. |  |  |
| Company PD Update Date | date | Date when the PD was last updated. |  |  |
| Company LGD | double | Loss Given Default — expected loss if the company defaults. |  |  |
| Company LGD Source | string | Source of the LGD estimate. |  |  |
| Company LGD Update Date | date | Date when the LGD was last updated. |  |  |
| Company EL | double | Expected loss for the company (based on PD and LGD). |  |  |
| Sales | double | Total revenue from goods or services sold. |  | ✓ |
| Total Sales Per Period | double | Gross revenue reported by the borrower for a given period (typically monthly … |  |  |
| Net Profit | double | Company's profit after all expenses and taxes. |  |  |
| Total Debt | double | Total outstanding debt obligations of the company. |  |  |
| Enterprise Value | double | Total value of the company (market cap + debt − cash). |  |  |
| Free Cash Flow | double | Cash generated by the company after capital expenditures. |  |  |
| Date Of Financials | date | Date of the most recent financial statement. |  |  |
| Annual Recurring Revenue | double | Revenue from recurring sources on an annual basis. |  |  |
| Liquidity | double | Company's ability to meet short-term obligations. |  |  |
| Interest Coverage | double | Ratio of EBIT to interest expenses. |  |  |
| Debt Coverage | double | Company's ability to cover total debt from operating income. |  |  |
| Total Turnover | double | Total revenue or sales over a period. |  |  |
| Total Debt To EBITDA | double | Ratio of total debt to EBITDA — measures leverage. |  |  |
| Senior Debt To EBITDA | double | Ratio of senior debt to EBITDA — focuses on senior obligations. |  |  |
| LTM EBITDA | double | EBITDA over the last twelve months. |  |  |
| Total Assets | double | Total assets owned by the company. |  |  |
| EBITDA | double | Earnings before interest, taxes, depreciation, and amortization. |  |  |

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
| Loan ID | string | uid value that uniquely identifies the loan within the originator’s database. |  | ✓ |
| CF Reference Date | date | date when the borrower made the payment. |  |  |
| Type | string | type of cash flow as per defined list of values | ✓ | ✓ |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
| Effective Amount | amount | paid amount at the reference date. |  |  |
