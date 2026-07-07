---
title: Commercial — Equipment Finance — Data Model
main: commercial
sub: equipment-finance
entities:
  - name: investments
    field_count: 55
  - name: ppc_milestones
    field_count: 8
  - name: equipment
    field_count: 29
  - name: borrower
    field_count: 18
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 5
---

# Commercial — Equipment Finance — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 55 |  |
| `ppc_milestones` | 8 |  |
| `equipment` | 29 |  |
| `borrower` | 18 |  |
| `calculated` | 8 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `equipment.Contract ID` ↔ `investments.Contract ID` ↔ `ppc_milestones.Contract ID`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Contract ID | string | Unique identifier for the equipment lease or loan, as reported by the Origina… |  | ✓ |
| Originator Custom ID | string | Custom internal identifier used by the originator. |  |  |
| Originator Name | string | Legal name of the entity that originated the financing. |  |  |
| Reporting Date | date | Snapshot / cut-off date to which all figures in this record refer. |  | ✓ |
| Contract Issue Date | date | Date the contract was issued. |  |  |
| Contract Start Date | date | Contract start date. |  |  |
| Contract End Date | date | Contract maturity or end date. |  |  |
| Pool Addition Date | date | Date on which the contract was added to the securitisation or funding pool. |  |  |
| Contract Currency | string | Currency in which the contract is denominated. |  |  |
| Face Value | amount | Original or face value of the asset under contract. |  | ✓ |
| Principal Outstanding | amount | Current principal balance of the contract, varying in calculation depending o… |  | ✓ |
| Accrued Interest Amount | amount | Total interest accrued on the contract up to the reporting date but not yet p… |  |  |
| Accrued Interest At Pool Addition Date | amount | Interest accrued but not yet paid when the contract entered the securitisatio… |  |  |
| Equipment Contract Type | string | Type of contract. | ✓ |  |
| Asset Category | string | Classification of the asset. | ✓ |  |
| Repayment Structure | string | Repayment structure of the contract. | ✓ |  |
| Installment Frequency | string | Scheduled frequency of principal payments. | ✓ |  |
| Payment Plan | string | Structured schedule of payment amounts and due dates. |  |  |
| Seller Name | string | Company selling or assigning the asset. |  | ✓ |
| Actual Return | amount | Actual return received from the asset. |  |  |
| Current Term | integer | The number of months between the Current Maturity Date and the Reporting Date. |  |  |
| Original Term Reported | integer | The number of months between the Current Maturity Date and the Issue Date. |  |  |
| Has Balloon Payment | boolean | Indicates if a balloon payment is required. | ✓ |  |
| Balloon Payment Value | amount | Amount of the balloon payment, if any. |  |  |
| Purchase Terms | string | Price for which the lessee can purchase the equipment at end of term. |  |  |
| Guarantee Class | string | Type of guarantee involved. | ✓ |  |
| TRAC End Value | amount | Residual value assumed in a TRAC lease. |  |  |
| PPC Terms | string | Flag indicating whether the PPC contract was converted into a lease by borrow… |  |  |
| Payment Status | string | Status of the account performance based on transaction-specific contractual d… |  |  |
| Status | string | Performance status of the loan based on transaction-specific contractual defi… | ✓ |  |
| Repayment Status | string | Terminal repayment / resolution status of the contract. | ✓ |  |
| PD | string | Credit quality grade assigned to the loan. |  |  |
| PD Days | integer | Days past due — days of delay on any expected cash flow, calculated based on … |  |  |
| Interest In Delay | amount | Total amount of interest that has not been paid by its respective due dates. |  |  |
| Principal In Delay | amount | Total amount of principal that has not been paid by its respective due dates. |  |  |
| Arrears Balance | amount | Total overdue amount on the contract, including both principal and interest. |  |  |
| First Delay Date | date | Earliest date on which the contract first entered a delinquent / delayed status. |  |  |
| Last Delay Date | date | Most recent date on which the contract was observed in a delinquent / delayed… |  |  |
| Last Payment Date | date | Date of the most recent payment received from the debtor. |  |  |
| Is Closed | boolean | Flag indicating whether the contract has been fully closed / repaid. | ✓ | ✓ |
| Prepaid Date | date | Date on which the contract was paid in full ahead of schedule. |  |  |
| Principal Prepayment | amount | Cumulative principal amount prepaid ahead of the contractual schedule. |  |  |
| Prepayment Fee | amount | Fee charged to the debtor for repaying the contract early. |  |  |
| Charge Off Date | date | Date on which the contract is declared in default or charged off according to… |  | ✓ |
| Principal Charge Off Amount | amount | Unpaid principal amount at charge-off date as per contractual definition. |  |  |
| Interest Charge Off Amount | amount | Due and unpaid interest amount at charge-off date as per contractual definition. |  |  |
| Write Off Date | date | Date on which the contract was recorded as a loss. |  |  |
| Write Off Amount | amount | Total cumulative amount recorded as loss (principal + accrued interest + fees). |  |  |
| Write Off Principal Amount | amount | Principal component of the total write-off amount. |  |  |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |
| Gross Recovered Amount | amount | Total gross proceeds recovered before deducting recovery and remarketing costs. |  |  |
| Net Recovered Amount | amount | Net recovery amount after deducting all collection, legal, and remarketing co… |  |  |
| Recovery Collected Amount | amount | Total cash collected through recovery activities in the current reporting per… |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Recovery Date | date | Date of the most recent recovery payment or collection. |  | ✓ |

### `ppc_milestones`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| PPC MS ID | string | Unique identifier of the milestone for PPC. |  |  |
| Contract ID | string | Contract identifier linking the milestone to the parent contract. |  | ✓ |
| Perc Milestone | percentage | Percent completion associated with the milestone for PPC. |  |  |
| Expected Date | date | Expected date of completion for the milestone for PPC. |  |  |
| Actual Date | date | Effective date of completion for the milestone for PPC. |  |  |
| P Comp | percentage | Percent completion of the equipment for PPC. |  |  |
| Amount Due | amount | Payment expected at the milestone for PPC. |  |  |
| Milestone Status | string | Completion status of the milestone. | ✓ |  |

### `equipment`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Equipment ID | string | Unique identifier of the equipment within the database, as reported by the Or… |  |  |
| Contract ID | string | Contract identifier linking the equipment record to the parent financing cont… |  | ✓ |
| Manufacturer Name | string | Original Equipment Manufacturer name. |  |  |
| Manufacturer Serial | string | Unique manufacturer-assigned identifier (e.g. serial number). |  |  |
| Equipment Description | string | Free-text description of the equipment. |  |  |
| Equipment Category | string | Broad category of equipment (e.g. aircraft, marine). |  | ✓ |
| Equipment Sub Category | string | Category detail (e.g. fixed-wing, helicopter). |  |  |
| Equipment Condition | string | Current condition of the asset. | ✓ |  |
| Year Manufactured | string | Year the equipment was manufactured. |  |  |
| Purchase Price | amount | Original purchase price of the asset. |  |  |
| Purchase Currency | string | Currency used for the purchase. |  |  |
| Equipment Location | string | Physical location or site where the equipment is held. |  |  |
| Hours Operated | double | Cumulative hours the asset has been operated. |  |  |
| Latest Appraised Value | amount | Most recent appraised value of the asset. |  | ✓ |
| Appraisal Date | date | Date on which the latest appraisal was conducted. |  |  |
| Initial Residual Value | amount | Estimated residual value at the start of the contract. |  |  |
| Updated Residual Value | amount | Updated residual value based on current appraisal or condition. |  |  |
| Guaranteed End Value | string | Guaranteed residual value to be paid at the end of the lease term. |  |  |
| Unguaranteed End Value | string | Portion of the asset's value not guaranteed by the obligor at the end of the … |  |  |
| LTV Ratio | percentage | Loan-to-value ratio calculated as current principal outstanding divided by la… |  |  |
| Maintenance State | string | Current status of the asset's maintenance. | ✓ |  |
| Last Inspection Date | date | Date of the most recent physical inspection. |  |  |
| Next Inspection Due Date | date | Next scheduled inspection or maintenance due date. |  |  |
| Insurance Provider | string | Insurance provider with whom the asset is currently insured. |  | ✓ |
| Insurance Policy Number | string | Reference number of the insurance policy covering the asset. |  |  |
| Insurance Coverage Amount | amount | Insured value of the asset under the current policy. |  |  |
| Insurance Expiration Date | date | Expiry date of the current insurance policy. |  |  |
| Asset Age Years | integer | Age of the equipment in years as of the reporting date, derived from year of … |  |  |
| Remaining Useful Life Years | integer | Estimated remaining useful life of the equipment in years. Key input for resi… |  |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Debtor Company ID | string | Company that is the primary debtor. |  |  |
| Debtor Individual ID | string | Individual that is the debtor, if applicable. |  |  |
| Debtor Legal Name | string | Registered legal name of the debtor company or full name of the individual de… |  |  |
| Debtor Country | string | Country where the debtor is legally registered or resident. |  |  |
| Debtor Sector Code | string | Industry or economic activity code representing the debtor's primary sector (… |  |  |
| Enterprise Size | string | Size category of the enterprise (e.g. micro, SME, large). | ✓ | ✓ |
| Probability Of Default | percentage | Likelihood that the debtor will default within 12 months on its obligations, … |  |  |
| Probability Of Default Source | string | Source / provider of the probability of default. |  |  |
| Rating Current | string | Credit rating assigned to the debtor by an external provider, as of the repor… |  |  |
| Rating Source | string | Name of the entity providing the rating. |  |  |
| Total Assets | amount | Total value of everything the debtor owns, as of the most recent balance shee… |  |  |
| Total Debt | amount | Total amount of all short-term and long-term debts the debtor owes, as of the… |  |  |
| LTM EBITDA | amount | Earnings Before Interest, Taxes, Depreciation, and Amortization for the last … |  |  |
| Total Debt To EBITDA | percentage | Leverage ratio comparing total debt to EBITDA — indicates the debtor's abilit… |  |  |
| Date Of Financials | date | Date corresponding to the most recent financial data. |  |  |
| Bankruptcy Flag | boolean | Flag indicating if the debtor is currently in bankruptcy. | ✓ |  |
| Bankruptcy Date | date | Reference date of the bankruptcy event. |  |  |
| Bankruptcy Status | string | Bankruptcy status of the debtor. | ✓ |  |

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
