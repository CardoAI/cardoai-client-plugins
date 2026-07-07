---
title: Commercial — Ecommerce Finance — Data Model
main: commercial
sub: ecommerce-finance
entities:
  - name: investments
    field_count: 43
  - name: borrower
    field_count: 18
  - name: marketplace seller
    field_count: 7
  - name: marketplace
    field_count: 14
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 5
---

# Commercial — Ecommerce Finance — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 43 |  |
| `borrower` | 18 |  |
| `marketplace seller` | 7 |  |
| `marketplace` | 14 |  |
| `calculated` | 8 |  |
| `cash_flows` | 5 |  |

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Facility ID | string | Unique identifier of the loan within the database, as reported by the Originator |  |  |
| Reporting Date | date | Snapshot / cut-off date to which all figures in this record refer. |  | ✓ |
| Origination Date | date | Date on which the loan or facility was issued |  |  |
| Funded Amount | amount | Disbursed principak amount as of Issue Date (include undrawn portion, if any) |  |  |
| Currency | string | Unique identifier for the currency in which the amount is denominated. |  |  |
| Use Of Proceeds | string | Inventory purchase, marketing, etc. |  |  |
| Funding Purpose Detail | string | Explanation of funding purpose |  |  |
| Repayment Structure | string | Daily holdback %, revenue share %, fixed daily debit | ✓ |  |
| Daily Holdback Pct | percentage | If marketplace holdback model, in percentage |  |  |
| Minimum Daily Payment | amount | Floor payment |  |  |
| Installment Frequency | string | Scheduled frequency of payments. | ✓ |  |
| Expected Term Days | integer | Projected payoff horizon |  |  |
| Original Maturity Date | date | Original maturity date |  |  |
| Maturity Date | date | Current maturity date (as of the Reporting Date) |  | ✓ |
| Residual Term | integer | The number of months between the Current Maturity Date and the Reporting Date |  |  |
| Asset Age Months | integer | Age of the facility measured as the difference between the reporting date and… |  |  |
| Closing Date | date | Date in which the investment was closed (repaid, prepaid, written-off, declar… |  |  |
| Performance Status | string | Performance status of the loan based on transaction specific contractual defi… | ✓ |  |
| Repayment Status | string | Type of loan repayment status, as per defined listed of values:  - no_repayme… | ✓ |  |
| Is closed | boolean | Field that indicates if the loan is still open | ✓ | ✓ |
| DPD | integer | Day past due, indicating the days of delay on any expected cash flow (not on … |  | ✓ |
| Underwriting Score | string | The assigned credit rating (e.g., BBB, Ba2). |  |  |
| Payment Collector Entity | string | Entity responsible for collecting repayments (e.g., Stripe, HyperWallet, etc) |  |  |
| Prepaid Date | date | For loans prepaid indicates the date on which the loan has been paid in full |  |  |
| Prepaid Amount | amount | Cumulative principal amount prepaid (include all the payments done before the… |  |  |
| Default Date | date | The date when the loan has been declared charged-off |  |  |
| Loss Date | date | Date in which the loan was recorded as loss |  | ✓ |
| Loss Amount | amount | Total cumulative amount recorded as loss |  | ✓ |
| UPB | amount | Unpaid principal balance of the facility as of the reporting date, excluding … |  | ✓ |
| Current Interest Rate | percentage | Interest rate or factor rate applicable to the facility as of the reporting d… |  |  |
| APR | percentage | Annual Percentage Rate — the all-in annualised cost of the facility to the bo… |  | ✓ |
| Accrued Interest Amount | amount | Interest accrued on the outstanding balance but not yet collected as of the r… |  |  |
| Principal In Delay | amount | Cumulative principal amount that is overdue as of the reporting date. |  |  |
| Interest In Delay | amount | Cumulative interest amount that is overdue as of the reporting date. |  |  |
| Default Flag | boolean | Boolean indicator of whether the facility is currently classified as in default. | ✓ |  |
| Contractual Defaulted Principal Amount | amount | Outstanding principal balance at the date of contractual default. |  |  |
| Write Off Date | date | Date on which the facility balance was formally written off. |  |  |
| Write Off Amount | amount | Total cumulative amount written off against the facility balance to date. |  |  |
| Recovery Collected Amount | amount | Total cash collected through recovery activities on the defaulted facility. |  |  |
| Net Recovered Amount | amount | Net recovery amount after deducting all associated collection and legal costs. |  |  |
| Recovery Date | date | Date on which the most recent recovery payment was received. |  | ✓ |
| Loss Given Default | percentage | Estimated percentage of the exposure expected to be lost in the event of defa… |  |  |
| Is Closed | boolean | Boolean flag indicating whether the facility has been fully closed. | ✓ | ✓ |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | Unique identifier for the borrower within the database. |  |  |
| Company Group ID | string | Identifier for the company group the entity belongs to. |  |  |
| Company VAT | string | Company's VAT number / tax code used for tax purposes. |  |  |
| Company Name | string | Registered legal name of the company. |  |  |
| Company Country | string | Country where the company is legally registered. |  |  |
| Company Region | string | Geographical region of the company’s registration. |  |  |
| Company Founding Date | date | Date when the company was legally established. |  |  |
| Company Website | string | URL of the company’s official website. |  |  |
| Is Sole Proprietorship | boolean | Indicates if the company is a sole proprietorship (yes/no). | ✓ |  |
| Company Risk Score | string | Quantitative measure of the company's overall risk. |  | ✓ |
| Company Risk Score Source | string | Source that provided the risk score. |  |  |
| Company Risk Score Update Date | date | Date when the risk score was last updated. |  |  |
| Sales | amount | Total revenue from goods or services sold. |  |  |
| Net Profit | amount | Company’s profit after all expenses and taxes. |  |  |
| Total Debt | amount | Total outstanding debt obligations of the company. |  |  |
| Free Cash Flow | amount | Cash generated by the company after capital expenditures. |  |  |
| Annual Recurring Revenue | amount | Revenue from recurring sources on an annual basis. |  |  |
| EBITDA | amount | Earnings before interest, taxes, depreciation, and amortization. |  |  |

### `marketplace seller`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Product Return Rate Pct | percentage | Product return rate, expressed as a percentage of the total sales volume. |  |  |
| Order Defect Rate Pct | percentage | Order defect rate, expressed as a percentage of the total sales volume. |  |  |
| Late Shipment Rate Pct | percentage | Late shipment rate, expressed as a percentage of the total sales volume. |  |  |
| On Time Delivery Pct | percentage | On-time delivery rate, expressed as a percentage of the total sales volume. |  |  |
| Account Suspension Flag | boolean | Flag indicating if the Seller account has been suspended from the respective … |  |  |
| Repayment Source | boolean | Primary revenue channel funding repayments (e.g., Shopify, Amazon) |  |  |
| Seller Tenure | integer | Time active on the primary platform, in months |  |  |

### `marketplace`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Name | string | Human-readable name of the marketplace. |  | ✓ |
| Marketplace Type | string | B2C, "B2B", "DTC-enabler", etc. |  |  |
| Country | string | Country where the marketplace is based or operates. |  |  |
| Website | string | URL of the main marketplace platform. |  |  |
| Rating | string | Type of seller performance rating system (e.g., stars, feedback score). |  |  |
| Marketplace Seller ID | string | Unique system identifier for the seller. |  |  |
| Fee Structure | string | Summary or code for the fee model (e.g., 15% of GMV, flat monthly). |  |  |
| Payout Frequency | string | How often seller payments are processed (daily, weekly, etc.). |  |  |
| Buyer Protection Flag | boolean | Indicates if buyer protection programs are in place. |  |  |
| Return Policy Standard | string | Standard return window (e.g., 30 days). |  |  |
| Fulfillment Model | string | Marketplace fulfilled, "Seller fulfilled", "3PL", etc. |  |  |
| Avg Shipping Time | integer | Average delivery time for the platform (in days). |  |  |
| Fraud Detection | string | Name or code of fraud prevention engine used (if applicable). |  |  |
| Kyc Requirements | string | KYC/AML requirements imposed on sellers. |  |  |

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
