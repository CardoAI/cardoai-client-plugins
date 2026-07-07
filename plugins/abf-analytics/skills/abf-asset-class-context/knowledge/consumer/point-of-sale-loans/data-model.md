---
title: Consumer — Point Of Sale Loans — Data Model
main: consumer
sub: point-of-sale-loans
entities:
  - name: investments
    field_count: 43
  - name: calculated
    field_count: 7
  - name: merchant
    field_count: 25
  - name: order
    field_count: 26
  - name: order item
    field_count: 14
  - name: Payment
    field_count: 22
  - name: Underwriting
    field_count: 16
  - name: cash_flows
    field_count: 4
---

# Consumer — Point Of Sale Loans — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `investments` | 43 |  |
| `calculated` | 7 |  |
| `merchant` | 25 |  |
| `order` | 26 |  |
| `order item` | 14 |  |
| `Payment` | 22 |  |
| `Underwriting` | 16 |  |
| `cash_flows` | 4 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `cash_flows.Loan ID` ↔ `investments.Loan ID`

## Field dictionary

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Uid value that uniquely identifies the loan within the originator's database. |  | ✓ |
| channel | string | Origination channel (Online, In‑store, Mobile App, Marketplace, Broker). |  |  |
| BNPL Plan Type | string | Pay‑in‑4, Short‑term Installment, Long‑term Installment, Revolving, Other. |  |  |
| Installment Count | integer | Number of installments scheduled by the plan. |  |  |
| Installment Frequency | string | Weekly, Biweekly, Monthly, Other. |  |  |
| First Due Date | date | First scheduled repayment due date. |  |  |
| Grace Period Days | integer | Days after due date before late fees accrue. |  |  |
| Promotion Type | string | Deferred Interest, Zero APR, Reduced APR, No Payments, Rebate, None. |  |  |
| Promotion Start Date | date | Promotion start date. |  |  |
| Promotion End Date | date | Promotion end date. |  |  |
| Deferred Interest Flag | boolean | Interest accrues but is deferred during promo period. |  |  |
| Deferred Interest Accrued | double | Interest accrued during promo period but not yet billed. |  |  |
| Promotional Subsidy Amount | double | Absolute subsidy amount applied to financing. |  |  |
| Promotional Subsidy Source | string | Source of subsidy (Merchant, Manufacturer, Distributor, Other). |  |  |
| Loan Adjustment Due To Return Amount | double | Adjustment to loan principal due to returns/refunds. |  |  |
| Recourse Type | string | None, Merchant Full Buyback, Partial Recourse, Early‑Pay Chargeback Window. |  |  |
| Chargeback Window Days | integer | Days after funding during which loan can be charged back to merchant. |  |  |
| Autopay Enrolled Flag | boolean | Whether borrower is enrolled in automatic payments. |  |  |
| Payment Method | string | ACH, Debit Card, Credit Card, Wallet, Bank Transfer. |  |  |
| Purchase Date | date | Date of loan transfer to the SPV or pledge to the lender. |  |  |
| Accrued Interests At Pool Addition Date | amount | Accrued interest on the loan at the date it was added to the pool. |  |  |
| Original Balance | amount | The total nominal (par) value of the loan at the issue date. |  | ✓ |
| Performance Status | string | Status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| Performance Status Contractual | string | Status of the loan performance based on transaction specific contractual defi… | ✓ |  |
| Repayment Status | string | Type of repayment status as per defined list. | ✓ |  |
| Is Closed | boolean | Flag indicating whether the loan account has been fully closed/repaid. | ✓ |  |
| Maturity Date | date | Current loan maturity date. |  | ✓ |
| Maturity Date Original | date | Maturity date at origination, before any modification intervened. |  |  |
| Closing Date | date | Date on which the loan is considered closed, with no further collection actio… |  |  |
| Prepaid Date | date | Date on which the loan was fully or partially prepaid ahead of schedule. |  |  |
| Periodical Prepaid Amount | amount | Amount prepaid during the current reporting period. |  |  |
| Prepaid Amount | amount | Total amount paid to fully close the outstanding balance of the loan. |  |  |
| Interest In Delay | amount | Total amount of interest that has not been paid on due dates. |  |  |
| Principal In Delay | amount | Total amount of principal that has not been paid on due dates. |  |  |
| Sale Date | date | date on which the loan was repurchased or sold |  |  |
| Sale Price | amount | loan sale or repurchase price as % of par |  |  |
| Write Off Amount | amount | Total amount written off against the loan (principal + accrued interest + fees). |  |  |
| Write Off Date | date | Date on which the write-off was recorded. |  |  |
| Write Off Principal Amount | amount | Principal component of the total write-off amount. |  |  |
| Gross Recovered Amount | amount | Total recovered amount, as of the reporting date. |  | ✓ |
| Net Recovered Amount | amount | Total amount repaid post-default, net of collection costs. |  |  |
| Recovery Date | date | Date on which the most recent recovery payment or collection was received. |  | ✓ |
| Loss Given Default | percentage | Estimated percentage of exposure expected to be lost in the event of default,… |  |  |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| MOB Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| MOB CGL | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| MOB Net Loss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| Remaining Term Months | integer | Number of months remaining until the current maturity date. |  |  |
| Loan Term | integer | Total contractual term of the loan expressed in months from origination to sc… |  | ✓ |
| MOB Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |

### `merchant`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Merchant ID | string | Unique identifier for the originating merchant. |  |  |
| Merchant Legal Name | string | Legal name of the merchant. |  |  |
| Merchant Trade Name | string | Doing‑business‑as name of the merchant. |  |  |
| Merchant Category Code | string | Card network MCC (4‑digit) for the merchant. |  |  |
| Merchant Industry | string | High‑level industry segment (Retail, Services, Healthcare, Travel, Other). |  |  |
| Merchant Website | string | Primary website URL. |  |  |
| Merchant City | string | Merchant city for the store or headquarters. |  |  |
| Merchant State | string | Merchant state/province. |  |  |
| Merchant Country | string | Merchant country. |  |  |
| Merchant Onboarding Date | date | Date merchant was approved to originate POS loans. |  |  |
| Merchant Status | string | Active, Suspended, Terminated, Under Review. |  |  |
| Merchant Risk Tier | string | Internal risk tier/classification for the merchant. |  |  |
| Merchant Score | double | Internal numeric risk/quality score for the merchant. |  |  |
| Pos Provider | string | POS platform used by the merchant (Square, Clover, Shopify POS, Lightspeed, O… |  |  |
| Store ID | string | Identifier for the physical store where the sale occurred (if applicable). |  |  |
| Terminal ID | string | Identifier of POS terminal used for the transaction (if applicable). |  |  |
| Payment Processor | string | Processor/acquirer facilitating card payments (Adyen, Stripe, Worldpay, etc.). |  |  |
| Merchant Discount Rate | percentage | Merchant Discount Rate (MDR) for POS financing. |  |  |
| Merchant Subsidy Rate | percentage | Rate of APR buy‑down funded by merchant/manufacturer. |  |  |
| Merchant Repaument Due to Chargeback Amount | double | Amount merchant repaid due to chargeback/return. |  |  |
| Merchant Reserve Percent | percentage | Percentage of settlement held in reserve against risk. |  |  |
| Merchant Reserve Amount | double | Absolute amount held in reserve. |  |  |
| Reserve Release Date | date | Date reserve released/reconciled. |  |  |
| Settlement Frequency | string | Daily, Weekly, Twice Weekly, Other. |  |  |
| Settlement Hold Flag | boolean | Whether settlements are currently on hold. |  |  |

### `order`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Order ID | string | Unique identifier of the POS order associated with the loan. |  |  |
| Order Date | date | Date/time when the order was placed. | ✓ |  |
| Order Channel | string | Web, Mobile App, In‑store, Call Center, Social, Other. |  |  |
| Currency | string | Order currency. |  |  |
| Items Count | integer | Number of items (lines) in the order. |  | ✓ |
| Order Gross Amount | double | Gross order amount before discounts and taxes. |  |  |
| Discount Amount | double | Total discounts/coupons applied to the order. |  |  |
| Coupon Code | string | Coupon or promotion code used at checkout. |  |  |
| Tax Amount | double | Total tax amount for the order. |  |  |
| Shipping Amount | double | Shipping/delivery fees for the order. |  | ✓ |
| Gift Card Amount Applied | double | Portion of order paid by gift card/store credit. |  |  |
| Down Payment Amount | double | Customer down payment at checkout (cash/card). |  |  |
| Order Net Amount | double | Net amount after discounts, taxes, shipping, and down payment, used to determ… |  |  |
| Return Policy Days | integer | Merchant return window in days. |  |  |
| Order Status | string | Open, Fulfilled, Partially Fulfilled, Cancelled, Returned, Refunded. |  |  |
| Delivery Method | string | Ship to Home, In‑Store Pickup (BOPIS), Curbside, In‑store Service, Digital Go… |  |  |
| Delivery Estimated Date | date | Estimated delivery/fulfillment date. |  |  |
| Delivery Actual Date | date | Actual delivery/fulfillment date. |  |  |
| Delivery Status | string | Not Shipped, In Transit, Delivered, Service Rendered, Failed, Partial. |  |  |
| Partial Fulfillment Flag | boolean | True if order was fulfilled in multiple shipments/visits. |  |  |
| Return Flag | boolean | True if any portion of the order was returned. |  |  |
| Return Date | date | Date of return. |  |  |
| Return Reason Code | string | Reason code for return (Damaged, Not As Described, Size, Defect, Service Issu… |  |  |
| Refund Amount Total | double | Total refunded amount to the consumer. |  |  |
| Partial Refund Flag | boolean | True if refund was partial. |  |  |
| Refund Method | string | Refunded to Card, Wallet, Store Credit, Bank, Other. |  |  |

### `order item`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Line Item ID | string | Identifier of the order line item. |  |  |
| Sku | string | Merchant SKU or product code. |  |  |
| Product Name | string | Display name of the item/service sold. |  |  |
| Product Category | string | Category of item (Electronics, Apparel, Furniture, Health, Travel, Services, … |  | ✓ |
| Unit Price | double | Unit price excluding tax. |  |  |
| Quantity | double | Quantity purchased. |  |  |
| Extended Price | double | Unit price × quantity (before discounts/tax). |  |  |
| Line Discount Amount | double | Discounts applied to the line item. |  |  |
| Line Tax Amount | double | Tax applied to the line item. |  |  |
| Serial Number | string | Product serial/IMEI (if applicable). |  |  |
| Warranty Flag | boolean | Whether an extended warranty or service plan was purchased. |  |  |
| Digital Goods Flag | boolean | True if digital/non‑deliverable good. |  |  |
| Subscription Flag | boolean | True if item is a recurring subscription. |  |  |
| Refundable Flag | boolean | Whether the item is eligible for return/refund. |  |  |

### `Payment`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Auth ID | string | Identifier of POS terminal used for the transaction (if applicable). |  |  |
| Auth Date | date | Processor/acquirer facilitating card payments (Adyen, Stripe, Worldpay, etc.). |  |  |
| Auth Amount | double | Unique identifier of the POS order associated with the loan. |  |  |
| Capture Date | date | Date/time when the order was placed. |  |  |
| Capture Amount | double | Web, Mobile App, In‑store, Call Center, Social, Other. |  |  |
| Settlement Date | date | Order currency. |  |  |
| Settlement Amount | double | Number of items (lines) in the order. |  |  |
| Settlement Batch ID | string | Gross order amount before discounts and taxes. |  |  |
| Processing Fee Amount | double | Total discounts/coupons applied to the order. |  |  |
| Interchange Fee Amount | double | Coupon or promotion code used at checkout. |  |  |
| chargeback_flag | boolean | Indicates a card network chargeback/dispute occurred. |  |  |
| chargeback_date | date | Date chargeback was received. |  |  |
| chargeback_reason_code | string | Network reason code (e.g., Visa/FI codes). |  |  |
| chargeback_amount | double | Chargeback amount. |  |  |
| representment_outcome | string | Won, Lost, Partial, Pending. |  |  |
| dispute_open_date | date | Date consumer dispute opened. |  |  |
| dispute_close_date | date | Date dispute closed. |  |  |
| card_network | string | Visa, Mastercard, Amex, Discover, Other. |  |  |
| card_token_id | string | Tokenized card identifier (no PAN). |  |  |
| card_last4 | string | Last 4 digits of the card (if applicable). |  |  |
| card_bin | string | First 6–8 digits of the card (tokenized/redacted per policy). |  |  |
| wallet_type | string | Apple Pay, Google Pay, PayPal, Other. |  |  |

### `Underwriting`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| fraud_score | double | Fraud risk score from the decisioning/fraud provider. |  |  |
| fraud_risk_level | string | Low, Medium, High, Critical. |  |  |
| idv_method | string | Identity verification method (OTP, KBA, Document, eID, None). |  |  |
| idv_passed_flag | boolean | True if identity verification passed. |  |  |
| device_fingerprint_id | string | Hashed device/browser identifier captured at checkout. |  |  |
| ip_address | string | IP address recorded at checkout (tokenized/stored per policy). |  |  |
| avs_result | string | Address Verification Service result code. |  |  |
| cvv_result | string | Card verification value result code. |  |  |
| velocity_check_flag | boolean | Whether velocity/consistency checks triggered. |  |  |
| sanctions_screen_passed_flag | boolean | True if sanctions/PEP screening passed. |  |  |
| credit_pull_type | string | None, Soft, Hard. |  |  |
| credit_bureau | string | Experian, Equifax, TransUnion, Other. |  |  |
| approval_status | string | Approved, Declined, Pended, Cancelled. |  |  |
| decision_date | date | Date/time of final credit decision. |  |  |
| decision_engine_version | string | Version/identifier of decisioning model used. |  |  |
| decision_reason_codes | string | Comma‑separated reason codes for decision/adverse action. |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Loan ID | string | Uid value that uniquely identifies the loan within the originator's database. |  | ✓ |
| Cash Flow Subtype Expected | string | Subtype label for cash‑flow details (Merchant Discount, Processor Fee, Interc… |  |  |
| Cash Flow Subtype Realized | string | Subtype label for cash‑flow details (Merchant Discount, Processor Fee, Interc… |  |  |
| CF Reporting Date | date | Cut-off date to which all figures and statuses in this record refer. |  |  |
