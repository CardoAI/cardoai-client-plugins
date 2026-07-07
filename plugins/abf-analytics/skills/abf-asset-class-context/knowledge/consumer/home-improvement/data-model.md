---
title: Consumer — Home Improvement — Data Model
main: consumer
sub: home-improvement
entities:
  - name: investments
    field_count: 59
  - name: borrower
    field_count: 20
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 5
  - name: collateral
    field_count: 54
---

# Consumer — Home Improvement — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 59 |  |
| `borrower` | 20 |  |
| `calculated` | 8 |  |
| `cash_flows` | 5 |  |
| `collateral` | 54 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Unique identifier for the loan within the originator or servicer system. |  | ✓ |
| Reporting Date | date | Snapshot/cut-off date to which all figures in this record refer. |  | ✓ |
| Originator | string | name of the originator of the loan. |  | ✓ |
| Issue Date | date | date on which the loan was issued. |  | ✓ |
| Purchased Principal | amount | total nominal amount of the loan that has been purchased or pledged, as of th… |  | ✓ |
| Currency ISO | string | standardized ISO, three-letter currency code representing the currency of the… |  |  |
| Financing Purpose | string | type of financing purpose as per defined list values: | ✓ |  |
| Purchase Date | date | date of loan transfer to the SPV or pledge to the lender |  |  |
| Purchase Price | amount | Price paid to acquire the loan, typically expressed as a percentage of par or… |  |  |
| UPB | amount | outstanding principal balance, remaining amount of the loan that has not yet … |  | ✓ |
| Apr | percentage | Annual Percentage Rate the all-in annualised cost of the loan including inter… |  |  |
| Performance Status | string | status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| dpd | integer | number of days by which a scheduled or expected payment is overdue. |  |  |
| Maturity Date | date | current loan maturity date. |  | ✓ |
| Original Maturity Date | date | maturity date at origination, before any modification intervened. |  |  |
| Closing Date | date | date on which the loan is considered closed, with no further collection actio… |  |  |
| Repayment Status | string | type of repayment status as per defined list. | ✓ |  |
| Current Interest Rate | double | value of the interest rate applicable to the loan, whether fixed or floating,… |  |  |
| Interest Rate Type | string | interest rate type as per defined list of values. Default value: Fixed Rate | ✓ |  |
| Amortization Type | string | amortization type as per defined list of values. Default value: Fixed Payment | ✓ |  |
| Day Count Convention | string | day count convention as per defined list of values: | ✓ |  |
| Accrued Interest Amount | amount | total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interests At Pool Addition Date | amount | Accrued interest on the loan at the date it was added to the pool. |  |  |
| Interest In Delay | amount | total amount of interest that has not been paid by its respective due dates. |  |  |
| Principal In Delay | amount | total amount of principal that has not been paid by its respective due dates. |  |  |
| Next Payment Date | date | date, as of the reporting date, on which the borrower’s next contractual paym… |  |  |
| Contractual Payment Amount Current | amount | scheduled recurring amount the borrower must pay under the loan agreement, in… |  | ✓ |
| Contractual Payment Amount Original | amount | scheduled recurring amount the borrower must pay under the loan agreement, in… |  |  |
| Last Delay Date | date | latest date in which the loan was in delay. |  |  |
| First Delay Date | date | date on which the borrower first failed to pay the amount due as expected. |  |  |
| Prepaid Date | date | date of the last cash flow in case of borrower prepayment. |  |  |
| Prepaid Amount | amount | total amount paid to fully close the outstanding balance of the loan. |  |  |
| Principal Installment Frequency | string | scheduled frequency of the principal amount payment as per defined list of va… | ✓ |  |
| Interest Installment Frequency | string | scheduled frequency of interest payments as per defined list of values. Defau… | ✓ |  |
| Charge Off Date | date | date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Principal Charge Off Amount | amount | unpaid principal amount at default date as per contractual definition. |  |  |
| Interest Charge Off Amount | amount | due and unpaid interest amount at default date as per contractual definition. |  |  |
| Charge Off Reason |  | description or details of the loan that has been charged-off. |  |  |
| Recovery Collected Amount | amount | Total cash amount collected through recovery activities (legal proceedings, c… |  |  |
| Gross Recovered Amount | amount | total recovered amount, as of the reporting date. |  | ✓ |
| Net Recovered Amount | amount | total amount repaid post-default, net of collection costs. |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Hardship Amount | amount | loan current principal balance amount currently under a hardship arrangement,… |  |  |
| Hardship First Payment Date | date | date when the borrower's first payment under the hardship arrangement was sch… |  |  |
| Hardship Flag | boolean | flag that indicates whether the loan is currently under a hardship arrangement. | ✓ |  |
| Hardship Last Payment Date | date | the date when the most recent payment was made under the hardship arrangement. |  |  |
| Country | string | Full country name of the borrower's primary residential address. |  |  |
| State | string | Region, state, or province of the borrower's primary residential address. |  | ✓ |
| Original Balance | amount | the total nominal (face) value of the loan at the issue date. |  | ✓ |
| Loss Given Default | percentage | borrower’s expected loss in the event of default, measured as of the reportin… |  |  |
| Loss Amount | amount | total charge-off amount, net of recoveries, inclusive of both principal and i… |  | ✓ |
| Loss Date | date | Indicates the date the loss was recorded and the asset was written off. |  | ✓ |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Remaining Term (Days) | integer | Number of calendar days remaining until the current maturity date. |  |  |
| Remaining Term (Years) | integer | Number of years remaining until the current maturity date (fractional). |  |  |
| Asset Age (Days) | integer | Number of calendar days elapsed since the loan's issue date. |  |  |
| Asset Age (Years) | integer | Number of years elapsed since the loan's issue date (fractional). |  |  |
| Seller Merchant Code | string | Broad economic sector code classifying the borrower's industry or occupation … |  | ✓ |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed/repaid. | ✓ |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | uid type value unique identifier for the borrower within the database |  |  |
| Pti | percentage | Payment-to-Income ratio: borrower's scheduled loan payment divided by verifie… |  |  |
| Bankruptcy Chapter | string | Chapter of bankruptcy filed by the borrower (e.g. Chapter 7, Chapter 13) wher… |  |  |
| Bankruptcy Date | date | Date on which the borrower filed for bankruptcy protection. |  |  |
| Bankruptcy Flag | boolean | Boolean indicator of whether the borrower has filed for bankruptcy. | ✓ |  |
| Bankruptcy Status | string | Current status of the bankruptcy proceeding (e.g. Filed, Active, Discharged, … | ✓ |  |
| Primary Income Type | string | Nature of the borrower's primary income source (e.g. Salary, Self-Employed, P… | ✓ |  |
| Primary Income Amount | amount | Verified annual gross income from the borrower's primary income source. |  |  |
| Original Pti | percentage | Payment-to-Income ratio calculated at origination using the original loan pay… |  |  |
| Dti | percentage | Debt-to-Income ratio: borrower's total monthly debt obligations divided by gr… |  |  |
| Original Dti | percentage | Debt-to-Income ratio as calculated at the time of loan origination. |  |  |
| Employer Name | string | Name of the borrower's primary employer. |  |  |
| Employment Duration | string | Length of time the borrower has been employed with the current employer (in m… |  |  |
| Employment Status | string | Borrower's employment status at origination or as of reporting date (e.g. Ful… | ✓ |  |
| Employment Title | string | Job title or occupation of the borrower. |  |  |
| Original Fico Score | integer | Borrower's FICO credit score at the time of loan origination. |  |  |
| Originator Identifier | string | Unique code or ID assigned to the originating institution within the platform. |  |  |
| Originator Score | integer | Internal credit score assigned by the originator as of the reporting date. |  |  |
| Originator Score Original | integer | Internal credit score assigned by the originator at the time of origination. |  |  |
| Borrower Id | string | Unique identifier for the borrower entity within the originator or servicer s… |  |  |

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
| Type | string | type of cash flow as per defined list of values. | ✓ | ✓ |
| Effective Amount | amount | paid amount at the reference date. |  |  |
| Expected Amount | amount | Total amount expected to be paid by the borrower on the scheduled due date. |  | ✓ |

### `collateral`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Property ID | string | Unique identifier for the property associated with the loan. |  |  |
| Property Description | string | Free-text description of the property including any relevant characteristics … |  |  |
| Property Address | string | Full street address of the property being improved. |  |  |
| Zip Code | string | Postal or ZIP code of the property. Used for geographic stratification and re… |  |  |
| Latitude | double | Geographic latitude coordinate of the property. Enables spatial analysis and … |  |  |
| longitude | double | Geographic longitude coordinate of the property. Used alongside latitude for … |  |  |
| Housing Type | string | Classification of the dwelling type being improved. Affects collateral value … |  | ✓ |
| Property Type | string | Legal or structural classification of the property. Affects the lender's enfo… |  | ✓ |
| Ownership Type | string | How the borrower holds legal title to the property. Joint or shared ownership… |  | ✓ |
| Occupancy Status | string | Whether the borrower occupies the property as their primary home, a secondary… |  | ✓ |
| Nr Units | integer | Number of individual units within the property (relevant for multi-unit or mi… |  |  |
| area unit | string | Unit of measurement used for all area fields (e.g. square metres or square fe… |  |  |
| Residential Area | double | Total floor area of the property designated for residential use, expressed in… |  |  |
| Occupied Area | double | Floor area of the property that is currently occupied or in active use. |  |  |
| external_area | double | Area of external spaces forming part of the property (e.g. garden, terrace, p… |  |  |
| commercial_area | double | Floor area designated for commercial use within a mixed-use property. Relevan… |  |  |
| total_surface | double | Total combined surface area of the property across all uses and spaces. |  |  |
| rooms | integer | Total number of rooms in the property excluding bathrooms and utility spaces. |  |  |
| beds | integer | Number of bedrooms in the property. Used as a proxy for property size and mar… |  |  |
| baths | integer | Number of bathrooms in the property. |  |  |
| year_built | integer | Year in which the property was originally constructed. Older properties may c… |  |  |
| re_asset_status | string | Current operational or lifecycle status of the property asset. Tracks whether… |  |  |
| interior_level | string | Grade or scope of the interior improvement being financed. Higher-grade proje… |  |  |
| property_condition | string | Overall physical condition of the property at the time of loan origination or… |  |  |
| renovation_starting_date | date | Date on which the renovation or improvement project commenced. Used to track … |  |  |
| capex_current | double | Capital expenditure incurred on the renovation project to date at the reporti… |  |  |
| estimated_capex | double | Total projected capital expenditure for the renovation project as estimated a… |  |  |
| renovation_complete_date | date | Actual or expected date on which the renovation project is completed. Delays … |  |  |
| contractor_contact_name | string | Name of the primary contractor responsible for carrying out the renovation wo… |  |  |
| project_category | string | High-level category describing the type of improvement being undertaken. |  |  |
| project_scope_description | string | Free-text description of the renovation project scope, including works to be … |  |  |
| ucc_filing_date | date | Date on which a Uniform Commercial Code financing statement was filed against… |  |  |
| ucc_release_date | date | Date on which the UCC lien was released or terminated following repayment or … |  |  |
| mechanic_lien_filed_flag | boolean | Indicates whether a mechanic's or contractor's lien has been filed against th… |  |  |
| lien_waiver_received_date | date | Date on which a lien waiver was received from the contractor, releasing any c… |  |  |
| permit_number | string | Reference number of the building or renovation permit issued by the relevant … |  |  |
| permit_issue_date | date | Date on which the building permit was issued. Work commenced before permit is… |  |  |
| permit_final_signoff_date | date | Date on which the local authority issued final sign-off confirming the works … |  |  |
| inspection_required_flag | boolean | Indicates whether a formal inspection by the lender or a third party is requi… |  |  |
| inspection_status | string | Current status of the required property or project inspection. |  |  |
| inspection_last_date | date | Date of the most recent inspection carried out on the property or renovation … |  |  |
| contractor_warranty_term_months | integer | Duration in months of the warranty provided by the contractor on the complete… |  |  |
| contractor_warranty_provider | string | Name of the entity providing the contractor warranty. May be the contractor d… |  |  |
| tax_credit_eligible_flag | boolean | Indicates whether the renovation project qualifies for a government tax credi… |  |  |
| tax_credit_program | string | Name or reference of the tax credit programme under which the borrower is cla… |  |  |
| tax_credit_amount_expected | double | Expected tax credit amount the borrower anticipates receiving upon project co… |  |  |
| tax_credit_amount_received | double | Actual tax credit amount received by the borrower. Compared against the expec… |  |  |
| utility_rebate_amount | double | Cash rebate received from a utility provider in connection with energy effici… |  |  |
| insurance_claim_flag | boolean | Indicates whether an insurance claim has been filed in connection with the pr… |  |  |
| insurance_claim_amount | double | Amount claimed or received under an insurance policy in connection with the p… |  |  |
| valuation_amount | double | Assessed market value of the property at the date of valuation. Used for LTV … |  |  |
| valuation_date | date | Date on which the property valuation was carried out. Valuations older than 1… |  |  |
| valuation_method | string | Methodology used to arrive at the property valuation. |  |  |
| valuation_provider | string | Name of the firm or individual that carried out the property valuation. |  |  |
