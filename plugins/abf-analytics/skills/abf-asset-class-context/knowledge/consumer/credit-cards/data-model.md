---
title: Consumer — Credit Cards — Data Model
main: consumer
sub: credit-cards
entities:
  - name: account
    field_count: 68
  - name: investments
    field_count: 1
  - name: cardholder
    field_count: 30
  - name: calculated
    field_count: 7
  - name: cash_flows
    field_count: 6
---

# Consumer — Credit Cards — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `account` | 68 |  |
| `investments` | 1 |  |
| `cardholder` | 30 |  |
| `calculated` | 7 |  |
| `cash_flows` | 6 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `account.Account ID` ↔ `cash_flows.Account ID`

## Field dictionary

### `account`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Account ID | string | uid value that uniquely identifies the account within the originator’s database. |  | ✓ |
| Open Date | date | date on which the account was opened. |  |  |
| Reporting Date | date | Snapshot/cut-off date to which all figures in this record refer. |  | ✓ |
| Credit Limit Original | amount | Maximum amount of credit available on the card as of the open date. |  |  |
| Credit Limit Current | amount | Maximum amount of credit available on the card as of the reference date. |  |  |
| Account Purchase Date | date | date of account transfer to the SPV or pledge to the lender |  |  |
| Unpaid Principal Amount | amount | Outstanding principal balance on the account as of the statement date, exclud… |  |  |
| Purchase Price | percentage | price as % of the purchased principal amount paid to purchase the account. |  |  |
| Unpaid Principal Interest Bearing Amount | amount | Principal amount that is actively collecting/accruing interest |  |  |
| Utilization | string | Utilization percentage of the Credit Limit |  | ✓ |
| Apr | percentage | annual percentage rate (apr) is the yearly interest charged to cardholders or… |  |  |
| Performance Status | string | status of the account performance based on transaction specific contractual d… | ✓ |  |
| DPD | integer | number of days by which a scheduled or expected payment is overdue. |  | ✓ |
| Closing Date | date | date on which the account is considered closed, with no further collection ac… |  |  |
| Repayment Status | string | type of repayment status as per defined list. | ✓ |  |
| Unpaid Purchase Principal Amount | amount | Remaining (unpaid) principal amount from purchases of the account that has no… |  |  |
| Unpaid Cash Advance Principal Amount | amount | Remaining (unpaid) principal amount from cash advances of the account that ha… |  |  |
| Unpaid Balance Transfer Principal Amount | amount | Remaining (unpaid) principal amount from balance transfer of the account that… |  |  |
| Statement Purchase Interest Amount | amount | Remaining interest amount from purchases of the account that has not yet been… |  |  |
| Statement Cash Advance Interest Amount | amount | Remaining interest amount from cash advances of the account that has not yet … |  |  |
| Statement Balance Transfer Balance Transfer Amount | amount | Remaining interest amount from balance transfers of the account that has not … |  |  |
| Statement Annual Fees | amount | Remaining annual fee amount on the account that has not yet been repaid |  |  |
| Statement Late Fees | amount | Remaining late fees on the account that have not yet been paid |  |  |
| Statement Other Fees | amount | All other fees on the account that have not yet been paid |  |  |
| Last Purchase Date | date | Date of the last purchase made by the Cardholder |  |  |
| Last Purchase Amount | amount | Amount of the last purchase made by the Cardholder |  |  |
| Interest Rate Type | string | interest rate type as per defined list of values. Default value: Fixed Rate |  |  |
| Current Interest Rate | percentage | value of the interest rate applicable to the account, whether fixed or floati… |  |  |
| Current Cash Advance Interest Rate | percentage | Applicable interest rate on cash advances |  |  |
| Current Balance Transfer Interest Rate | percentage | Applicable interest rate on a balance transfer |  |  |
| Day Count Convention | integer | day count convention as per defined list of values: | ✓ |  |
| Accrued Interest Amount | amount | total interest accrued on the account up to the reporting date but not yet pa… |  |  |
| Principal In Delay | amount | total amount of principal that has not been paid by its respective due dates. |  |  |
| Interest In Delay | amount | total amount of interest that has not been paid by its respective due dates. |  |  |
| Minimum Amount Due | amount | Minimum amount eligible for reimbursement by the cardholder --> Minimum  cont… |  |  |
| Installment Frequency | string | Scheduled frequency of principal payments. |  |  |
| Transassction Count Cycle | integer | Count of purchases made by the Cardholder in the most recent billing cycle |  |  |
| Transaction Amount Cycle | integer | The total amount of purchases by the Cardholder in the most recent billing cycle |  |  |
| Billing Cycle Length | integer | Number of days in an account’s billing cycle |  |  |
| Cycle End Date | date | End date of the most recent billing cycle |  |  |
| Transaction Count LTD | integer | Total number of purchases over the life of the account |  |  |
| Transaction amount LTD | amount | Total purchases amount - Volume Life to Date |  |  |
| Total Payment LTD | amount | Total number of payments over the life of the account |  |  |
| Last Delay Date | date | latest date in which the account was in delay |  |  |
| Last Payment Date | date | date of the most recent payment made by the cardholder. |  |  |
| Num CLI LTD | integer | Number of credit limit increases, lifetime to date |  |  |
| Autopay Flag | boolean | Flag that indicates whether the account is in auto-pay or not |  |  |
| Account Revoked Date | date | Data when the account was revoked |  |  |
| Account Revoked Status | string | Flag indicating whether the account is revoked or not |  |  |
| Fraud Status | string | Flag indicating whether the account is marked as fraudulent |  |  |
| Monthly Payment Rate | percentage | Percentage of the outstanding balance that paid in the last month. |  |  |
| Issuer | string | name of the originator of the account (or issuer of the credit card) |  |  |
| Sale Date | date | date on which the account was repurchased or sold |  |  |
| Sale Price | amount | account sale or repurchase price as % of par |  |  |
| Charge Off Date | date | date on which the account is declared in default or charged off according to … |  | ✓ |
| Charge Off Reason | string | description or details of the account that has been charged-off. |  |  |
| Principal Charge Off Amount | amount | unpaid principal amount at default date as per contractual definition |  |  |
| Interest Charge Off Amount | amount | due and unpaid interest amount at default date as per contractual definition |  |  |
| Gross Recovered Amount | amount | total recoverd amount, as of the reporting date.. |  | ✓ |
| Net Recovered Amount | amount | total amount repaid post-default, net of collection costs. |  |  |
| Loss Date | date | Indicates the date the loss was recorded and the asset was written off. |  | ✓ |
| Loss Amount | amount | total charge-off amount, net of recoveries, inclusive of both principal and i… |  | ✓ |
| Modification Date | date | reporting date when the modification event occurred |  |  |
| Modification End Date | date | date when the modification event has concluded and the cardholder has resumed… |  |  |
| Modification Details | string | additional details related to the event |  |  |
| Issuer Rating Original | string | rating or credit score of the loan assigned by the issuer as of the issue date |  |  |
| Issuer Rating | string | rating or credit score of the loan assigned by the issuer as of the statement… |  |  |
| Rating Source | string | name of the entity providing the rating. |  |  |

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Statement Date | date | data cut-off date (statement date) |  |  |

### `cardholder`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Cardholder ID | string | uid type value unique identifier for the cardholder within the database |  |  |
| Birth Year | string | cardholder's year of birth. |  |  |
| Gender | string | gender of the invididual as per defined list of values | ✓ |  |
| Zip Code | string | five digit zip code of the cardholder at application time. |  |  |
| Fico Score | string | FICO credit score of the cardholder, as of the reporting date. |  | ✓ |
| Cardholder accounts count | amount | no. of accounts of the cardholder |  |  |
| Original Fico Score | amount | Original FICO credit score of the cardholder. |  |  |
| Vantage Score Original | string | vantage credit score of the cardholder as of the issue date. |  |  |
| Vantage Score | boolean | vantage credit score of the cardholder, as of the reporting date. |  |  |
| Originator Score Original | date | credit score of the cardholder assigned by the originator as of the issue date |  |  |
| Geography Iso Original | string | standardized geographic subdivision code representing the cardholder’s state,… |  |  |
| Employment Status | percentage | employment status of the cardholder as per defined list of values. | ✓ |  |
| Employer Name | string | the name of the cardholder’s employer. |  |  |
| Employment Title | date | job title or position of the cardholder at origination |  |  |
| Employment Duration | boolean | employment duration of the cardholder in years. |  |  |
| DTI Original | string | original debt-to-income ratio, indicating the proportion of the cardholder's … |  |  |
| DTI Current | string | debt-to-income ratio, indicating the proportion of the cardholder's income us… |  |  |
| PTI Original | amount | original payment-to-income ratio, indicating the proportion of the cardholder… |  |  |
| PTI Current | integer | payment-to-income ratio, indicating the proportion of the cardholder's income… |  |  |
| Total Debt Original | percentage | total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Total Debt Current | percentage | total amount of all short-term and long-term debts the individual owes, as of… |  |  |
| Home Ownership | percentage | type of home ownership, as per defined list of values: | ✓ |  |
| Primary Income Type | string | primary income type of the cardholder as per defined list of values. | ✓ |  |
| Primary Income Amount | string | annual income of the cardholder derived from their primary source of earnings. |  |  |
| Deceased Flag | string | indicates whether the cardholder is deceased |  |  |
| Deceased Date | string | cardholder's deceased date |  |  |
| Bankruptcy Flag | integer | flag that indicates if the cardholder is in bankruptcy. |  |  |
| Bankruptcy Date | string | reference date of bankruptcy event. |  |  |
| Bankruptcy Status | integer | bankruptcy status of the cardholder, as per the defined list of values. | ✓ |  |
| Bankruptcy Chapter | integer | indicates the chapter of US bankruptcy law reference. |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Mob Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| Mob Cgl | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| Mob Netloss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| Remaining Term (months) | integer | Number of months remaining until the current maturity date. |  |  |
| Loan Term | integer | Total contractual term of the loan expressed in months from origination to sc… |  |  |
| Mob Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Account ID | string | Unique identifier for the account within the servicer/originator system. |  | ✓ |
| CF Reference Date | date | date when the cardholder made the payment. |  |  |
| Type | string | Type of cash flow as per defined list of values | ✓ | ✓ |
| Effective Amount | amount | Paid amount at the Reference Date. |  |  |
| Details | string | Date on which the cash payment was received or posted by the servicer. |  |  |
| Recovery Source | string | The origin of the cash flow recovered from the asset. |  |  |
