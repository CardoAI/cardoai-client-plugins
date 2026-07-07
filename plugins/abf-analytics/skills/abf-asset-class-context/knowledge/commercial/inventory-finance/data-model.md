---
title: Commercial — Inventory Finance — Data Model
main: commercial
sub: inventory-finance
entities:
  - name: investments
    field_count: 71
  - name: asset_modification_event
    field_count: 5
  - name: collaterals
    field_count: 37
  - name: calculated
    field_count: 9
  - name: companies
    field_count: 44
  - name: cash_flows
    field_count: 5
---

# Commercial — Inventory Finance — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 71 |  |
| `asset_modification_event` | 5 |  |
| `collaterals` | 37 |  |
| `calculated` | 9 |  |
| `companies` | 44 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `collaterals.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Unique identifier of the loan within the database, as reported by the Origina… |  | ✓ |
| Originator Name | string | Originator name related to the specific loan. |  | ✓ |
| Reporting Date | date | Snapshot / cut-off date to which all figures in this record refer. |  | ✓ |
| Issue Date | date | Date on which the loan was issued. |  | ✓ |
| Pool Addition Date | date | Date when the loan has been transferred to the SPV or pledged. |  |  |
| Loan Amount | amount | Total amount of the loan as of Issue Date (including undrawn portion, if any). |  |  |
| Purchased Principal | amount | Total loan principal amount purchased by the SPV or pledged by the Borrower. |  | ✓ |
| Loan Currency | string | Unique identifier for the currency in which the amount is denominated. |  |  |
| Loan Price | amount | Price at which the loan was acquired into the securitization pool, expressed … |  |  |
| Upfront Fees | amount | Fees charged at loan origination, typically one-time and paid by the borrower. |  |  |
| Is Secured | boolean | Indicates whether a loan is secured or not. | ✓ |  |
| Loan Current Balance | amount | Unpaid principal balance as of the Reporting Date — remaining amount of the l… |  |  |
| Accrued Interest | amount | Accrued interest up to the current date. |  |  |
| Accrued Interests At Pool Addition Date | amount | Interest accrued but not yet paid when the loan entered the securitization pool. |  |  |
| Performance Status | string | Current performance classification of the asset. | ✓ |  |
| Loan Status | string | Terminal repayment / resolution status of the loan. | ✓ |  |
| Repayment Status | string | Type of loan repayment status. | ✓ |  |
| Days In Delay | integer | Days past due, indicating the days of delay on any expected cash flow. Calcul… |  |  |
| Arrears Balance | amount | Total overdue amount on the loan, including both principal and interest. |  |  |
| Arrears Balance Capital | amount | Portion of the arrears that relates specifically to overdue principal (capita… |  |  |
| Arrears Balance Interest | amount | Portion of the arrears that relates specifically to overdue interest payments. |  |  |
| First Delay Date | date | Earliest date on which the loan first entered a delinquent / delayed status. |  |  |
| Last Delay Date | date | Most recent date on which the loan was observed in a delinquent / delayed sta… |  |  |
| Loan Interest Rate Exp | percentage | The expected interest rate on the loan as per the contract at origination. |  |  |
| Loan Interest Rate Act | percentage | The actual interest rate currently being applied to the loan. |  |  |
| Interest Rate Type | string | The type of interest rate applied to the loan. | ✓ |  |
| Current Interest Rate Index | string | The name of the reference rate (e.g. EURIBOR, LIBOR, SOFR) used to calculate … | ✓ |  |
| Current Interest Rate Index Tenor | string | The duration of the interest rate index (e.g. 1M, 3M, 6M), indicating how oft… | ✓ |  |
| Index Valuation Date | date | The date when the interest rate index was last set or observed for rate calcu… |  |  |
| Current Index | percentage | The most recent value of the interest rate index used in calculating the loan… |  |  |
| Current Interest Rate Margin | percentage | The fixed margin (spread) added to the reference index to determine the total… |  |  |
| Interest Rate Floor | percentage | The minimum interest rate that can be applied to the loan, regardless of how … |  |  |
| Interest Rate Cap | percentage | The maximum interest rate that can be applied to the loan, regardless of how … |  |  |
| Amortisation Method | string | Method used to repay the loan (e.g. annuity, bullet, linear). | ✓ |  |
| Payment Frequency | string | Scheduled frequency of principal payments. | ✓ |  |
| Interest Frequency | string | How often interest payments are due (e.g. monthly, quarterly). | ✓ |  |
| First Payment Date | date | Date the borrower made or is scheduled to make the first loan payment. |  |  |
| Last Payment Date | date | Most recent payment date recorded before reporting or default. |  |  |
| Installment Amount | amount | Scheduled payment amount combining both interest and principal. |  |  |
| Installment Interest Amount | amount | Scheduled interest portion of the regular installment. |  |  |
| Installment Capital Amount | amount | Scheduled principal (capital) portion of the regular installment. |  |  |
| Installment Interest Amount Realized | amount | Actual interest received from the borrower in the reporting period. |  |  |
| Installment Capital Amount Realized | amount | Actual principal received from the borrower in the reporting period. |  |  |
| Original Term | integer | Total length of the loan from origination to maturity, expressed in months. |  |  |
| Remaining Term | integer | The number of months between the Current Maturity Date and the Reporting Date. |  | ✓ |
| Original Maturity Date Of The Loan | date | Original maturity date. |  |  |
| Maturity Date Of The Loan | date | Current maturity date as of the Reporting Date. |  |  |
| Closing Date | date | Date on which the investment was closed (repaid, prepaid, written-off, declar… |  |  |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed / repaid. | ✓ |  |
| Principal Prepayment | amount | Cumulative principal amount prepaid (includes all payments made before the co… |  |  |
| Prepayment Fee | amount | Fee charged to the borrower for repaying the loan early. |  |  |
| Prepaid Date | date | For loans prepaid, the date on which the loan has been paid in full. |  |  |
| Default Flag | boolean | Indicator showing whether the loan is in default. | ✓ |  |
| Default Date | date | Date the loan was classified as in default. |  |  |
| Amount Default Date Principal | amount | Unpaid principal amount at charge-off date as per contractual definition. |  |  |
| Amount Default Date Interest | amount | Due and unpaid interest amount at charge-off date as per contractual definition. |  |  |
| Accrued Int Default Date | amount | Interest accrued but unpaid as of the default date. |  |  |
| Write Off Date | date | Date on which the loan was recorded as a loss. |  |  |
| Write Off Amount | amount | Total cumulative amount recorded as loss. |  |  |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Gross Recovered Amount | amount | Total gross proceeds recovered before deducting recovery costs and expenses. |  | ✓ |
| Net Recovered Amount | amount | Net recovery amount credited to the asset after deducting all collection and … |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Date Of Repurchase | date | Date on which the loan was repurchased. |  |  |
| Repurchase Amount | amount | The amount that the originator or seller agrees to pay to buy back a loan fro… |  |  |
| Loan Rating | string | The credit rating assigned to the loan or borrower (e.g. BBB, Ba2). |  |  |
| Loan Rating Date | date | The date when the rating was issued or last updated. |  |  |
| Loan Rating Source | string | The agency or internal model that provided the rating (e.g. Moody's, internal… |  |  |
| Loan Rating Rank | integer | Indicates the priority or reliability of the rating when multiple ratings exi… |  |  |

### `asset_modification_event`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan Modified Flag | boolean | Indicates whether the loan has been modified. | ✓ |  |
| Modified Date | date | Date when the modification was implemented. |  |  |
| Modified Type | string | Type of modification applied to the loan. | ✓ |  |
| Modification Reason | string | Reason for the change (e.g. borrower hardship, restructuring, COVID-related). |  |  |
| Modification End Date | date | End date of the modification period, if temporary. |  |  |

### `collaterals`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Collateral Identifier | string | Unique ID assigned to the specific collateral asset. |  |  |
| Loan ID | string | ID linking the collateral to its associated loan. |  | ✓ |
| Collateral Type | string | Nature of the collateral (e.g. vehicle, equipment, food). |  |  |
| Geographic Region Collateral | string | Region or location where the collateral is situated. |  |  |
| Country | string | Country where the collateral is located. |  |  |
| State | string | State where the collateral is located. |  | ✓ |
| City | string | City where the collateral is located. |  |  |
| Collateral Currency | string | Currency in which the collateral values and sale are reported. |  |  |
| Original Valuation Amount | amount | Initial value of the collateral at loan origination or acquisition. |  |  |
| Original Valuation Method | string | Method used for the original valuation (e.g. appraisal, market comparison). |  |  |
| Original Valuation Date | date | Date when the original valuation was performed. |  |  |
| Current Valuation Amount | amount | Latest appraised or market value of the collateral. |  |  |
| Current Valuation Method | string | Method used for the current valuation (e.g. appraisal, market comparison). |  |  |
| Current Valuation Date | date | Date of the most recent valuation. |  |  |
| LTV Ratio | percentage | Loan-to-value ratio calculated as current loan balance divided by current col… |  |  |
| Date Of Sale | date | Date when the collateral was sold, if applicable. |  |  |
| Sale Price | amount | Price at which the collateral was sold, if sold. |  |  |
| Notes | string | Any additional relevant information or remarks about the collateral. |  |  |
| Product SKU | string | SKU or product identifier of the inventory item. |  |  |
| Description | string | Description of the product or item type. |  |  |
| Category | string | Broader category of the inventory (e.g. perishable, seasonal, durable, fragile). | ✓ | ✓ |
| Quantity | integer | Total number of units in inventory. |  |  |
| Unit Of Measure | string | Unit of measurement (e.g. kg, liters, units, pallets). |  |  |
| Purchase Date | date | Date when the collateral was purchased, manufactured, or added to the inventory. |  |  |
| Expiration Date | date | Expiration date of the inventory, if applicable (e.g. food, cosmetics). |  |  |
| Storage Location Type | string | Type of storage (e.g. warehouse, bonded warehouse, 3PL, seller-owned). | ✓ |  |
| Storage Provider | string | Name of the company or party storing the inventory. |  |  |
| Storage Conditions | string | Special storage requirements (e.g. temperature-controlled, humidity-controlled). |  |  |
| Turnover Ratio | double | Inventory turnover ratio for this product, if tracked. |  |  |
| Days On Hand | integer | Estimated number of days the current inventory stock will last based on the t… |  |  |
| Third Party Verification | boolean | Indicates if a third-party audit or inspection has verified the inventory. | ✓ |  |
| Last Physical Inspection Date | date | Date of the last physical inventory check. |  |  |
| Next Inspection Due | date | Next scheduled inspection date. |  |  |
| Concentration Risk Flag | boolean | Flag indicating whether a single inventory item or category represents more t… | ✓ |  |
| Insurance Coverage Flag | boolean | Indicates if the inventory is insured. | ✓ |  |
| Insurance Policy Number | string | Reference to the insurance policy covering the inventory. |  |  |
| Insurance Provider | string | Insurance company covering the asset. |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset Age Months | integer | Age of the loan expressed in whole months elapsed since the issue date. |  |  |
| Asset Age Days | integer | Number of calendar days elapsed since the loan's issue date. |  |  |
| Asset Term | integer | Total contractual term of the loan expressed in months from origination to sc… |  |  |
| Remaining Term Months | integer | Number of months remaining until the current maturity date. |  |  |
| MOB Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| MOB CGL | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| MOB Net Loss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| MOB Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |

### `companies`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Company ID | string | Unique identifier for the borrower within the database. |  |  |
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
| Enterprise Size | string | Size category of the enterprise (e.g. micro, SME, large). |  |  |
| Company Sector Code | string | Code indicating the sector / industry the company operates in. |  |  |
| Insurer Name | string | Name of the insurance company covering the business. |  |  |
| Insurance Score | string | Credit or risk score assigned by the insurer. |  |  |
| Is Sole Proprietorship | boolean | Indicates if the company is a sole proprietorship. | ✓ |  |
| Company Risk Score | string | Quantitative measure of the company's overall risk. |  |  |
| Company Risk Score Source | string | Source that provided the risk score. |  |  |
| Company Risk Score Update Date | date | Date when the risk score was last updated. |  |  |
| Company PD | double | Probability of default for the company. |  |  |
| Company PD Source | string | Source that provided the probability of default. |  |  |
| Company PD Update Date | date | Date when the PD was last updated. |  |  |
| Company LGD | double | Loss Given Default — expected loss if the company defaults. |  |  |
| Company LGD Source | string | Source of the LGD estimate. |  |  |
| Company LGD Update Date | date | Date when the LGD was last updated. |  |  |
| Company EL | double | Expected loss for the company (based on PD and LGD). |  |  |
| Sales | double | Total revenue from goods or services sold. |  |  |
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
| Total Assets | double | Total assets owned by the company. |  | ✓ |
| EBITDA | double | Earnings before interest, taxes, depreciation, and amortization. |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | uid value that uniquely identifies the loan within the originator’s database. |  | ✓ |
| CF Reference Date | date | date when the borrower made the payment. |  |  |
| Type | string | type of cash flow as per defined list of values | ✓ | ✓ |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
| Effective Amount | amount | paid amount at the reference date. |  |  |
