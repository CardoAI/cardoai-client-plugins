---
title: Commercial — Small Business Loans — Data Model
main: commercial
sub: small-business-loans
entities:
  - name: investments
    field_count: 71
  - name: asset_modification
    field_count: 5
  - name: borrower
    field_count: 55
  - name: calculated
    field_count: 8
  - name: cash_flows
    field_count: 5
---

# Commercial — Small Business Loans — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 71 |  |
| `asset_modification` | 5 |  |
| `borrower` | 55 |  |
| `calculated` | 8 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`
- `asset_modification.Modification End Date` ↔ `investments.Modification End Date`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | UID value that uniquely identifies the loan within the originator's database. |  | ✓ |
| Reference Date | date | Data cut-off date. |  |  |
| Issue Date | date | Date on which the loan was issued. |  | ✓ |
| Pool Addition Date | date | Date on which the loan was added to the securitisation or funding pool. |  |  |
| Purchase Date | date | Date of loan transfer to the SPV or pledge to the lender. |  |  |
| Expected Settlement Date | date | Expected loan settlement date. |  |  |
| Currency ISO | string | Standardized ISO three-letter currency code representing the currency of the … |  |  |
| Original Balance | amount | Total nominal (face) value of the loan at the issue date. |  | ✓ |
| Purchased Principal | amount | Total nominal amount of the loan that has been purchased or pledged, as of th… |  | ✓ |
| Purchase Price | percentage | Price as % of the purchased principal amount paid to purchase the loan. |  |  |
| UPB | amount | Outstanding principal balance — remaining amount of the loan that has not yet… |  | ✓ |
| Origination Fee Percentage | percentage | Percentage of the loan amount charged as a fee by the lender or originator at… |  |  |
| APR | percentage | Annual percentage rate — the yearly interest charged to borrowers or paid to … |  | ✓ |
| Current Interest Rate | percentage | Value of the interest rate applicable to the loan, whether fixed or floating,… |  |  |
| Current Interest Rate Margin | percentage | Value of interest rate margin (spread) for floating rates; for fixed rates, i… |  |  |
| Current Index | percentage | Current value of the index rate, which constitutes the floating component of … |  |  |
| Index Valuation Date | date | Reference date of the interest rate index. |  |  |
| Current Interest Rate Index Tenor | string | Type of interest rate tenor as per defined list of values. | ✓ |  |
| Current Interest Rate Index | string | Index to which the interest rate refers when it is variable / floating. | ✓ |  |
| Interest Rate Cap | percentage | Maximum interest rate that can be applied to a floating-rate financial instru… |  |  |
| Interest Rate Floor | percentage | Minimum interest rate that can be applied to a floating-rate financial instru… |  |  |
| Amortization Type | string | Amortization type as per defined list of values. | ✓ |  |
| Interest Installment Frequency | string | Scheduled frequency of interest payments. | ✓ |  |
| Payment Frequency | string | Scheduled frequency of principal repayments. | ✓ |  |
| Accrued Interest Amount | amount | Total interest accrued on the loan up to the reporting date but not yet payable. |  |  |
| Accrued Interest At Pool Addition Date | amount | Interest accrued but not yet paid when the loan entered the securitisation pool. |  |  |
| Balloon Amount | amount | Final lump sum payment due at the end of the asset term, if applicable. |  |  |
| Maturity Date Original | date | Maturity date at origination, before any modification intervened. |  |  |
| Maturity Date | date | Current loan maturity date. |  | ✓ |
| First Expected Payment Date | date | Scheduled date when the first payment is expected, as of the issue date. |  |  |
| Last Payment Date | date | Date of the most recent payment made by the borrower. |  |  |
| Closing Date | date | Date on which the loan is considered closed, with no further collection actio… |  |  |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed / repaid. | ✓ | ✓ |
| Performance Status | string | Status of the loan performance based on transaction-specific contractual defi… | ✓ |  |
| Performance Status Contractual | string | Performance status based strictly on contractual payment obligations, without… | ✓ |  |
| Repayment Status | string | Type of repayment status as per defined list. | ✓ |  |
| DPD | integer | Number of days by which a scheduled or expected payment is overdue. |  | ✓ |
| Interest In Delay | amount | Total amount of interest that has not been paid by its respective due dates. |  |  |
| Principal In Delay | amount | Total amount of principal that has not been paid by its respective due dates. |  |  |
| First Delay Date | date | Date on which the borrower first failed to pay the amount due as expected. |  |  |
| Last Delay Date | date | Latest date on which the loan was in delay. |  |  |
| Seniority | string | Position or rank of the financial asset in relation to other debts or claims … |  |  |
| Seniority Type | string | Classification or level of seniority assigned to the financial asset within t… | ✓ |  |
| Lien Type | string | Lien position of the loan or instrument in the capital structure. | ✓ |  |
| Deferred Flag | boolean | Flag indicating whether there is any deferred interest for the asset. | ✓ |  |
| Deferred Period | integer | Period in which interest is not paid and is accrued as deferred interest, sta… |  |  |
| Deferred Start Date | date | Date on which the loan began deferring interest. |  |  |
| Prepaid Date | date | Date of the last cash flow in case of borrower prepayment. |  |  |
| Prepaid Amount | amount | Total amount paid to fully close the outstanding balance of the loan. |  |  |
| Prepayment Fee | amount | Fee charged to the borrower for repaying the loan ahead of schedule. |  |  |
| Sale Date | date | Date when the loan was sold. |  |  |
| Sale Price | amount | Loan sale or repurchase price as % of par. |  |  |
| Charge Off Date | date | Date on which the loan is declared in default or charged off according to the… |  | ✓ |
| Principal Charge Off Amount | amount | Unpaid principal amount at default date as per contractual definition. |  |  |
| Interest Charge Off Amount | amount | Due and unpaid interest amount at default date as per contractual definition. |  |  |
| Write Off Date | date | Date on which the loan was recorded as a loss. |  |  |
| Write Off Amount | amount | Total cumulative amount recorded as loss (principal + accrued interest + fees). |  |  |
| Write Off Principal Amount | amount | Principal component of the total write-off amount. |  |  |
| Loss Date | date | Date on which the loss on the asset was recorded. |  | ✓ |
| Loss Amount | amount | Total loss amount, inclusive of both principal and interest. |  | ✓ |
| Loss Given Default | amount | Borrower's expected loss in the event of default, measured as of the reportin… |  |  |
| Gross Recovered Amount | amount | Total recovered amount as of the reporting date. |  | ✓ |
| Net Recovered Amount | amount | Total amount repaid post-default, net of collection costs. |  |  |
| Recovery Collected Amount | amount | Total cash collected through recovery activities (legal proceedings, collater… |  |  |
| Realized Recovery Collections | amount | Cash actually collected through recovery actions in the current reporting per… |  |  |
| Recovery Date | date | Date of the most recent recovery payment or collection. |  | ✓ |
| Date Of Repurchase | date | Date on which the loan was repurchased from the pool. |  |  |
| Repurchase Amount | amount | Amount paid by the originator or seller to buy back the loan from the pool, u… |  |  |
| Modification Date | date | Reporting date when the modification event occurred. |  |  |
| Modification End Date | date | Date when the modification event has concluded and the borrower has resumed t… |  |  |
| Modification Type | string | Type of modification applied to the loan. | ✓ |  |

### `asset_modification`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan Modified Flag | boolean | Indicates whether the loan has been modified. | ✓ |  |
| Modified Date | date | Date when the modification was implemented. |  |  |
| Modified Type | string | Type of modification applied to the loan. | ✓ |  |
| Modification Reason | string | Reason for the modification (e.g. borrower hardship, restructuring, COVID-rel… |  |  |
| Modification End Date | date | End date of the modification period, if temporary. |  |  |

### `borrower`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Borrower ID | string | UID type value unique identifier for the company borrower. |  |  |
| Group Identifier | string | UID type value unique identifier or number assigned to the company group. |  |  |
| Borrower Name | string | Legal name of the borrower. |  |  |
| VAT | string | Value added tax (VAT) number assigned to the company, used for tax identifica… |  |  |
| Geography ISO | string | Standardized geographic subdivision code representing the borrower's state, p… |  |  |
| Geography ISO Original | string | Standardized geographic subdivision code representing the borrower's state, p… |  |  |
| Zip Code | string | Postal code of the area where the company operates. |  |  |
| Address | string | Physical address of the enterprise, including street, city, state, and postal… |  |  |
| Sector Borrower ISO Original | string | Standardized industry or economic activity code representing the borrower's p… |  |  |
| Sector Borrower ISO Current | string | Standardized industry or economic activity code representing the borrower's p… |  |  |
| Founding Date | date | Date on which the enterprise was established or incorporated. |  |  |
| Number Of Employees | integer | Number of employees working for the company at year end. |  |  |
| Enterprise Size | string | Size category of the enterprise (e.g. micro, SME, large). | ✓ | ✓ |
| Legal Form | string | Legal structure of the company (e.g. LLC, S.A., GmbH, Sole Proprietor). |  |  |
| Date Of Financials | date | Date corresponding to the most recent financial data, typically the most rece… |  |  |
| Probability Of Default | percentage | Likelihood that the enterprise will default within 12 months on its debt obli… |  |  |
| Probability Of Default Source | string | Source / provider of the probability of default. |  |  |
| Rating Current | string | Credit rating assigned to the borrower by an external provider, as of the rep… |  |  |
| Rating Original | string | Credit rating assigned to the borrower by an external provider, as of the iss… |  |  |
| Rating Source | string | Name of the entity providing the rating. |  |  |
| Total Assets Original | amount | Total value of everything the enterprise owns (cash, investments, property, e… |  |  |
| Total Assets Current | amount | Total value of everything the enterprise owns (cash, investments, property, e… |  |  |
| Total Senior Debt Original | amount | Total amount of all senior debts the enterprise owes, as of the issue date. |  |  |
| Total Senior Debt Current | amount | Total amount of all senior debts the enterprise owes, as of the most recent b… |  |  |
| Total Debt Original | amount | Total amount of all short-term and long-term debts the enterprise owes, as of… |  |  |
| Total Debt Current | amount | Total amount of all short-term and long-term debts the enterprise owes, as of… |  |  |
| Liquidity Original | amount | Company's ability to cover short-term obligations, calculated as the sum of c… |  |  |
| Liquidity Current | amount | Company's ability to cover short-term obligations, calculated as the sum of c… |  |  |
| Free Cash Flow Current | amount | Amount of cash generated by the enterprise after accounting for capital expen… |  |  |
| LTM Sales Original | amount | Total revenue generated by the enterprise for the last 12 months, as of the l… |  |  |
| LTM Sales Current | amount | Total revenue generated by the enterprise for the last 12 months, as of the l… |  |  |
| LTM Annual Recurring Revenue Original | amount | Normalized yearly revenue expected from recurring subscription-based products… |  |  |
| LTM Annual Recurring Revenue Current | amount | Normalized yearly revenue expected from recurring subscription-based products… |  |  |
| LTM EBITDA Original | amount | Earnings Before Interest, Taxes, Depreciation, and Amortization for the last … |  |  |
| LTM EBITDA Current | amount | Earnings Before Interest, Taxes, Depreciation, and Amortization for the last … |  |  |
| LTM Net Profit Original | amount | Total profit of the enterprise after all expenses, taxes, and costs have been… |  |  |
| LTM Net Profit Current | amount | Total profit of the enterprise after all expenses, taxes, and costs have been… |  |  |
| Total Debt To EBITDA Original | percentage | Leverage ratio comparing total debt to EBITDA — indicates the company's abili… |  |  |
| Total Debt To EBITDA Current | percentage | Leverage ratio comparing total debt to EBITDA — indicates the company's abili… |  |  |
| Senior Debt To EBITDA Original | percentage | Leverage ratio comparing senior debt to EBITDA — indicates the company's abil… |  |  |
| Senior Debt To EBITDA Current | percentage | Leverage ratio comparing senior debt to EBITDA — indicates the company's abil… |  |  |
| Total Leverage Original | percentage | Leverage ratio comparing total debt to EBITDA — as of the issue date. |  |  |
| Total Leverage Current | percentage | Leverage ratio comparing total debt to EBITDA — based on date of financials. |  |  |
| Interest Coverage Original | percentage | Financial ratio measuring a company's ability to meet its interest obligation… |  |  |
| Interest Coverage Current | percentage | Financial ratio measuring a company's ability to meet its interest obligation… |  |  |
| DSCR Original | percentage | Debt service coverage ratio as of the facility origination date — measures th… |  |  |
| DSCR Current | percentage | Debt service coverage ratio as of the reporting date — measures the borrower'… |  |  |
| Bankruptcy Flag | boolean | Flag indicating if the borrower is currently in bankruptcy. | ✓ |  |
| Bankruptcy Date | date | Reference date of the bankruptcy event. |  |  |
| Bankruptcy Status | string | Bankruptcy status of the borrower. | ✓ |  |
| Guarantor Flag | boolean | Indicates whether a personal or corporate guarantor is in place for the loan.… | ✓ |  |
| Guarantor Type | string | Type of guarantee supporting the loan. | ✓ |  |
| Government Guarantee Flag | boolean | Indicates whether the loan benefits from a government-backed guarantee scheme… | ✓ |  |
| Government Guarantee Scheme | string | Name of the government guarantee scheme covering the loan (e.g. SBA 7(a), SBA… |  |  |
| Government Guarantee Percentage | percentage | Percentage of the outstanding loan balance covered by the government guarantee. |  |  |

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
| Loan ID | string | UID value that uniquely identifies the loan within the originator's database,… |  | ✓ |
| CF Reference Date | date | Date when the borrower made the payment. |  |  |
| Type | string | Type of cash flow as per defined list of values. | ✓ | ✓ |
| Effective Amount | amount | Paid amount at the reference date. |  |  |
| Expected Amount | amount | Total amount expected to be paid by the borrower on the scheduled due date. |  | ✓ |
