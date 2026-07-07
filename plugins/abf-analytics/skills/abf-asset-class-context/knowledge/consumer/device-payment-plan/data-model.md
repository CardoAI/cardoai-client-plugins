---
title: Consumer — Device Payment Plan — Data Model
main: consumer
sub: device-payment-plan
entities:
  - name: investments
    field_count: 19
  - name: subscription
    field_count: 34
  - name: borrower
    field_count: 12
  - name: equipment
    field_count: 20
  - name: calculated
    field_count: 7
  - name: cash_flows
    field_count: 8
---

# Consumer — Device Payment Plan — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 19 |  |
| `subscription` | 34 |  |
| `borrower` | 12 |  |
| `equipment` | 20 |  |
| `calculated` | 7 |  |
| `cash_flows` | 8 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Asset ID` ↔ `investments.Asset ID`
- `borrower.Borrower ID` ↔ `equipment.Borrower ID`
- `equipment.Currency` ↔ `subscription.Currency`
- `investments.Performance Status` ↔ `subscription.Performance Status`
- `investments.Status` ↔ `subscription.Status`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset ID | string | Unique identifier for the loan within the originator or servicer system. |  |  |
| Trade Date | date | Date on which the loan/asset was transferred to the SPV or pledged to the len… |  |  |
| Asset Funding | amount | Price paid by the Fund/SPV to acquire the asset (VAT/sales tax excluded). Rep… |  | ✓ |
| Days In Stock | integer | Number of days the asset remained in inventory before being deployed to a bor… |  | ✓ |
| Total Asset Revenue | amount | Sum of all subscription revenue and other revenue received over the lifetime … |  |  |
| Asset Market Value | amount | Most recent market valuation of the asset as of the reporting date. |  | ✓ |
| Report Date | date | Data cut-off date to which all investment-level figures in this record refer. |  |  |
| Current Asset Value | amount | Current carrying or assessed value of the asset as of the reporting date. |  |  |
| Asset Depreciation | amount | Depreciation expense at the asset level that reduces the carrying value of th… |  |  |
| Outstanding Balance | amount | Unpaid principal balance as of the reporting date — the remaining amount of t… |  |  |
| Maturity Date | date | Current contractual maturity date of the loan as of the reporting date. |  | ✓ |
| Number Of Bookings | integer | Number of times the asset has been rented out on subscription (count of disti… |  |  |
| Repayment Status | string | Current repayment classification of the loan. | ✓ |  |
| Performance Status | string | Current operational status of the asset within the portfolio. | ✓ |  |
| Status | boolean | Boolean flag indicating whether the loan is still open and active. | ✓ | ✓ |
| Is Sold | boolean | Boolean flag indicating whether the asset has been sold and is no longer unde… | ✓ |  |
| Asset Age | integer | Age of the loan measured as the difference between the pool cut-off date and … |  |  |
| Asset ROI | amount | Return on investment expressed as a percentage of the asset funding amount. |  |  |
| Total Asset Profit | amount | Return on investment expressed as an absolute monetary amount. |  |  |

### `subscription`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Rental Duration | integer | Contracted number of months of the subscription/renting period. |  |  |
| Rental Plan | string | Frequency at which the subscription payment is due (e.g. monthly, quarterly, … | ✓ |  |
| Rental Start Date | date | Subscription start date, typically coinciding with the asset delivery date. |  |  |
| Currency | string | ISO 4217 currency code in which the subscription is denominated. |  |  |
| Booking Amount | amount | Subscription price per period for the asset booking. Typically static but may… |  |  |
| Rental Current Duration | integer | Number of months elapsed from the subscription start date to the reporting date. |  |  |
| Rental Effective Duration | integer | Number of months elapsed from the subscription start date to the actual subsc… |  |  |
| Rental Remaining Duration | integer | Number of months remaining in the subscription based on the contracted durati… |  |  |
| Monthly Rental Amount | amount | Subscription inflows received in the reporting month, including first and rec… |  | ✓ |
| Other Rental Revenue | amount | Other asset inflows received in the reporting month, including asset sales pr… |  |  |
| Rental Monthly Due Amount | amount | Contractual amount due to be paid in the reporting month for the subscription. |  |  |
| Rental End Date | date | Date on which the subscription period expires. |  |  |
| Rental Monthly Amount | amount | Total subscribed amount due at the start date of the subscription plan. |  |  |
| UPB | amount | Unpaid principal balance as of the reporting date — the remaining subscriptio… |  | ✓ |
| Performance Status | string | Performance status of the subscription based on transaction-specific contract… | ✓ |  |
| DPD | integer | Days Past Due: number of days of delay on any expected cash flow (not on fina… |  | ✓ |
| Customer Type | string | Type of customer renting the device/asset. | ✓ |  |
| Customer Acquisition Channel | string | Channel through which the customer was acquired (e.g. Direct, Online, Partner… |  |  |
| Prepaid Date | date | Date on which the loan was fully or partially prepaid ahead of schedule. |  |  |
| Periodical Prepaid Amount | amount | Amount prepaid during the current reporting period. |  |  |
| Prepaid Principal Amount | amount | Cumulative principal amount that has been prepaid over the life of the loan. |  | ✓ |
| Is Prepaid | boolean | Boolean flag indicating whether the subscription was settled before the antic… | ✓ |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Gross Recovered Amount | amount | Total gross proceeds recovered before deducting recovery costs and expenses. |  | ✓ |
| Recovery Amount | amount | Net recovery amount credited to the loan after deducting collection costs. |  | ✓ |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Status | boolean | Boolean flag indicating whether the subscription is still open and active. | ✓ | ✓ |
| Last Payment Date | date | Date of the most recent repayment cash flow received on the subscription. |  |  |
| Contractual Default Principal | amount | Unpaid principal amount outstanding at the default date as per the contractua… |  |  |
| Contractual Default Interest | amount | Unpaid interest amount outstanding at the default date as per the contractual… |  |  |
| Default Amount | amount | Total default amount including residual debt, interest and fees outstanding a… |  |  |
| Charged Off Date | date | Date on which the loan/subscription balance was declared charged-off. |  |  |
| Loss Date | date | Date on which the loan was recorded as a loss in the system. |  | ✓ |
| Loss Amount | amount | Total cumulative amount recorded as loss on the subscription/loan. |  | ✓ |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | Unique identifier for the borrower within the database. |  |  |
| Borrower City | string | City where the borrower is located. |  |  |
| Borrower Country | string | Country where the borrower is located. |  |  |
| Postal Code | string | Postal or ZIP code of the borrower's location. |  |  |
| Employment | string | Employment status of the borrower. | ✓ |  |
| Primary Income | amount | Primary borrower annual income used to underwrite the exposure at origination… |  | ✓ |
| Primary Income Currency | string | ISO 4217 currency code in which the primary income is denominated. |  |  |
| Employment Title | string | Job title supplied by the borrower when applying for the financing. |  |  |
| DTI Current | percentage | Current debt-to-income ratio: total monthly debt obligations divided by gross… |  |  |
| DTI Original | percentage | Debt-to-income ratio as calculated at the time of origination. |  |  |
| Gender | string | Gender of the borrower. | ✓ |  |
| Birth Year | integer | Year of birth of the borrower. |  |  |

### `equipment`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Make | string | Brand or manufacturer of the device/asset (Original Equipment Manufacturer). |  |  |
| Make ID | string | Serial number or unique hardware identifier of the device. |  |  |
| Asset Condition | string | Condition of the asset at the moment of purchase. | ✓ | ✓ |
| Originator | string | Name or identifier of the entity that originated the transaction. |  | ✓ |
| Initial Asset Price | string | Original purchase price of the device/asset at acquisition. |  |  |
| Purchase Tax | amount | VAT or sales tax amount applied at the time of asset purchase. |  |  |
| Purchase Fee | amount | Other fees related to the acquisition of the asset included in its value (e.g… |  |  |
| Purchase Date | date | Date on which the asset was purchased. |  |  |
| Asset Type | string | Type or category of device/asset involved in the transaction (e.g. Smartphone… |  | ✓ |
| Borrower ID | string | Unique identifier for the borrower as reported by the originator, linking the… |  |  |
| Currency | string | ISO 4217 currency code in which the asset was purchased. |  |  |
| Asset Description | string | Free-text description of the asset (e.g. model name, specifications, colour). |  |  |
| Year Manufactured | integer | Year in which the asset was manufactured. |  | ✓ |
| Asset Sale Price | amount | Realised selling price of the asset net of any fees, applicable when the asse… |  |  |
| Sale Tax | amount | VAT or sales tax amount applied at the time of asset sale or disposal. |  |  |
| Sale Fees | amount | Other fees related to the sale of the asset included in the sale value (e.g. … |  |  |
| Sale Currency | string | ISO 4217 currency code in which the asset sale amount is denominated. |  |  |
| Sale Date | date | Date on which the asset was sold or disposed of, where applicable. |  |  |
| Asset Category | string | Main category group of the physical asset (e.g. Mobile, Computing, Audio-Visu… | ✓ | ✓ |
| Asset Subcategory | string | Detailed sub-category of the physical asset (e.g. Smartphone, Smartwatch, Lap… |  |  |

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
| Asset ID | string | Unique identifier for the loan or asset within the servicer/originator system. |  |  |
| Realized Amount | amount | Amount of the cash flow received. |  | ✓ |
| Cashflow Date | date | Date when the cash flow occurred. |  |  |
| CashFlow Type | string | Classification of the cash flow received (e.g. General Repayment, Principal R… | ✓ | ✓ |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
| Cashflow Recovery Source | string | If applicable, the source of recovered funds (e.g., collateral sale, guarante… |  |  |
| Cashflow Currency | string | Currency in which the cash flow was denominated. |  |  |
| Cash Flow Details | string | Additional information or notes related to the cash flow. |  |  |
