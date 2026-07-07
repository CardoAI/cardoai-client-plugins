---
title: Commercial — Trade Finance — Data Model
main: commercial
sub: trade-finance
entities:
  - name: investments
    field_count: 50
  - name: calculated
    field_count: 8
  - name: companies
    field_count: 44
  - name: cash_flows
    field_count: 6
---

# Commercial — Trade Finance — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 50 |  |
| `calculated` | 8 |  |
| `companies` | 44 |  |
| `cash_flows` | 6 |  |

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Trade ID | string | Unique Identification number of the trade |  |  |
| Debtor ID | string | Unique identifier of the debtor of the trade receivable |  |  |
| Seller ID | string | Unique identifier of the seller of the trade receivable. |  |  |
| Originator Name | string | Legal name of the entity that originated the asset. |  | ✓ |
| Reporting Date | date | Snapshot / cut-off date to which all figures in this record refer. |  | ✓ |
| Trade Receivable Date | date | Original trade receivable issue date. |  |  |
| Investment Date | date | Date on which the receivable was added to the SPV / Fund. |  |  |
| Invoice Currency | string | Original currency of the trade receivable (Please use the abbrevation in acco… |  |  |
| Trade Receivable Amount | amount | Face Value of trade receivable amount acquired by the Fund/SPV at investment … |  | ✓ |
| Purchase Amount | amount | Price paid to acquire the receivable (Amount financed) |  |  |
| Purchase Price | amount | price as % of the purchased principal amount paid to purchase the loan. |  |  |
| Outstanding Principal Amount | amount | Outstanding amount of the trade at reporting date |  |  |
| Due Date | date | Date when the receivable expires and payment is due |  |  |
| Extension Date | date | Extension date in case a new payment date has been agreed |  |  |
| APR | percentage | Expected Interest rate to be paid. |  | ✓ |
| Expected Net Return | amount | Total expected return to be paid. |  |  |
| Origination Fee Percentage | percentage | Fees charged at origination, typically one-time and paid by the borrower. |  |  |
| Performance Status | string | Current performance classification of the asset. | ✓ |  |
| DPD | integer | Number of calendar days the asset is past its contractual due date as of the … |  | ✓ |
| Trade Receivable Status | string | Terminal repayment / resolution status of the receivable. | ✓ |  |
| Is Prepaid | boolean | Indicates wether or not the receivable is prepaid. | ✓ |  |
| Prepaid Date | date | For receivables prepaid indicates the date on which the receivable has been p… |  |  |
| Closing Date | date | The date in which the investment was closed AND is not outstanding anymore (T… |  |  |
| Is Closed | boolean | Flag indicating whether the asset has been fully closed / repaid. | ✓ |  |
| Accrued Interest Amount | amount | total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interest At Pool Addition Date | amount | total accrued interest at the pool addition date |  |  |
| Interest In Delay | amount | total amount of interest that has not been repaid as of the most recent sched… |  |  |
| Principal In Delay | amount | total amount of principal that has not been paid by its respective due dates. |  |  |
| Last Delay Date | date | date of the most recent payment made by the trader. |  |  |
| First Delay Date | date | date on which the trader first failed to pay the amount due as expected. |  |  |
| Default Date | date | Date in which the trade receivable is classified as defaulted by the originator |  |  |
| Default Amount | amount | Amount (residual debt including interests and fees) at default date |  |  |
| Write Off Date | date | Date in which the loan is written off (date in which is registered the loss) |  |  |
| Write Off Amount | amount | Amount that has been written off by the originator |  |  |
| Date Of Repurchase | date | Date on which the loan was repurchased |  |  |
| Repurchase Amount | amount | The amount that the originator or seller agrees to pay to buy back a loan fro… |  |  |
| Loss Given Default | percentage | trader’s expected loss in the event of default, measured as of the reporting … |  |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Gross Recovered Amount | amount | Total gross proceeds recovered before deducting recovery costs and expenses. |  | ✓ |
| Net Recovered Amount | amount | Net recovery amount credited to the asset after deducting collection costs. |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Remaining Term Days | integer | Number of calendar days remaining until the current due / maturity date. |  |  |
| Remaining Term Years | integer | Number of years remaining until the current due / maturity date (fractional). |  |  |
| Asset Age Days | integer | Number of calendar days elapsed since the trade receivable date. |  |  |
| Asset Age Years | integer | Number of years elapsed since the trade receivable date (fractional). |  |  |
| Current Rating | string | The credit rating assigned to the loan or borrower (e.g., BBB, Ba2). |  |  |
| Rating Date | date | The date when the rating was issued or last updated. |  |  |
| Rating Source | string | The agency or internal model that provided the rating (e.g., Moody’s, interna… |  |  |
| Rating Rank | integer | Indicates the priority or reliability of the rating when multiple ratings exi… |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| MOB Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| MOB CGL | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| MOB Net Loss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| MOB Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Remaining Term Months | integer | Number of months remaining until the current due / maturity date. |  |  |
| Asset Term | integer | Total contractual term of the receivable expressed in months from origination… |  | ✓ |
| Asset Age Months | integer | Age of the receivable expressed in whole months elapsed since the trade recei… |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |

### `companies`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Company ID | string | Unique identifier for the company within the database. |  |  |
| Company Group ID | string | Identifier for the company group the entity belongs to. |  |  |
| Company Tax Code | string | Company's national tax identification code. |  |  |
| Company Name | string | Registered legal name of the company. |  | ✓ |
| Company Country | string | Country where the company is legally registered. |  |  |
| Company Region | string | Geographical region of the company’s registration. |  |  |
| Province | string | Province or local administrative area of the company. |  |  |
| Company Founding Date | date | Date when the company was legally established. |  |  |
| Company Legal Form | string | Legal structure of the company (e.g., LLC, S.A., GmbH). |  |  |
| Company N Employees | integer | Number of employees working for the company. |  |  |
| Company Address Code | string | Code representing the company’s address (postal or internal). |  |  |
| Company Website | string | URL of the company’s official website. |  |  |
| Company Type | string | General classification of the company (e.g., parent, subsidiary). |  |  |
| Enterprise Size | string | Size category of the enterprise (e.g., micro, SME, large). |  |  |
| Company Sector Code | string | Code indicating the sector/industry the company operates in. |  |  |
| Insurer Name | string | Name of the insurance company covering the business. |  |  |
| Insurance Score | string | Credit or risk score assigned by the insurer. |  |  |
| Is Sole Proprietorship | boolean | Indicates if the company is a sole proprietorship (yes/no). | ✓ |  |
| Company Risk Score | string | Quantitative measure of the company's overall risk. |  |  |
| Company Risk Score Source | string | Source that provided the risk score. |  |  |
| Company Risk Score Update Date | date | Date when the risk score was last updated. |  |  |
| Company PD | double | Probability of default for the company. |  |  |
| Company PD Source | string | Source that provided the probability of default. |  |  |
| Company PD Update Date | date | Date when the PD was last updated. |  |  |
| Company LGD | double | Loss Given Default – expected loss if the company defaults. |  |  |
| Company LGD Source | string | Source of the LGD estimate. |  |  |
| Company LGD Update Date | date | Date when the LGD was last updated. |  |  |
| Company EL | double | Expected loss for the company (based on PD and LGD). |  |  |
| Sales | double | Total revenue from goods or services sold. |  |  |
| Net Profit | double | Company’s profit after all expenses and taxes. |  |  |
| Total Debt | double | Total outstanding debt obligations of the company. |  |  |
| Enterprise Value | double | Total value of the company (market cap + debt - cash). |  |  |
| Free Cash Flow | double | Cash generated by the company after capital expenditures. |  |  |
| Date Of Financials | date | Date of the most recent financial statement. |  |  |
| Annual Recurring Revenue | double | Revenue from recurring sources on an annual basis. |  |  |
| Liquidity | double | Company's ability to meet short-term obligations. |  |  |
| Interest Coverage | double | Ratio of EBIT to interest expenses. |  |  |
| Debt Coverage | double | Company’s ability to cover total debt from operating income. |  |  |
| Total Turnover | double | Total revenue or sales over a period. |  |  |
| Total Debt To EBITDA | double | Ratio of total debt to EBITDA – measures leverage. |  |  |
| Senior Debt To EBITDA | double | Ratio of senior debt to EBITDA – focuses on senior obligations. |  |  |
| LTM EBITDA | double | EBITDA over the last twelve months. |  |  |
| Total Assets | double | Total assets owned by the company (likely meant as 'assets'). |  | ✓ |
| EBITDA | double | Earnings before interest, taxes, depreciation, and amortization. |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Invoice ID | string | Unique identifier of the invoice within the database, as reported by the orig… |  |  |
| Payment Date | date | Date when a payment is processed and recorded in the system. |  | ✓ |
| Cash Flow Type | string | Classification of the cash flow received. | ✓ |  |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date, in the origin… |  | ✓ |
| Realized Amount | amount | Actual cash amount received for the payment event, in the original currency. |  | ✓ |
| Currency | string | ISO 4217 abbreviation of the currency in which amounts are denominated (e.g. … |  |  |
