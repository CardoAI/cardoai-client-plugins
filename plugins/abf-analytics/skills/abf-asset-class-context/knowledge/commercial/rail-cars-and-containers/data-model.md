---
title: Commercial — Rail Cars And Containers — Data Model
main: commercial
sub: rail-cars-and-containers
entities:
  - name: asset
    field_count: 30
  - name: regulatory
    field_count: 10
  - name: investments
    field_count: 21
  - name: calculated
    field_count: 8
  - name: lease
    field_count: 17
  - name: depot
    field_count: 2
  - name: lessee
    field_count: 3
  - name: operations
    field_count: 20
  - name: appraisal
    field_count: 9
  - name: maintenance
    field_count: 13
  - name: insurance
    field_count: 2
  - name: security interest
    field_count: 3
  - name: cash_flows
    field_count: 5
---

# Commercial — Rail Cars And Containers — Data Model

## Entities

| Entity | Fields | Notes |
|--------|--------|-------|
| `asset` | 30 |  |
| `regulatory` | 10 |  |
| `investments` | 21 |  |
| `calculated` | 8 |  |
| `lease` | 17 |  |
| `depot` | 2 |  |
| `lessee` | 3 |  |
| `operations` | 20 |  |
| `appraisal` | 9 |  |
| `maintenance` | 13 |  |
| `insurance` | 2 |  |
| `security interest` | 3 |  |
| `cash_flows` | 5 |  |

## Join keys

Fields shared across entities — likely foreign-key relationships:

- `asset.Asset ID` ↔ `cash_flows.Asset ID`
- `appraisal.Insured Value` ↔ `insurance.Insured Value`

## Field dictionary

### `asset`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset ID | string | Unique identifier of the loan / financing agreement within the originator's d… |  | ✓ |
| Asset Type | string | Railcar, Intermodal Container, Chassis, Other. |  | ✓ |
| Owner Entity ID | string | Identifier of the asset owner/lessor. |  |  |
| Owner Reporting Marks | string | AAR reporting marks for railcars (e.g., TTX, BNSF). |  |  |
| Railcar Number | string | Railcar number (paired with reporting marks). |  |  |
| Umler ID | string | Railinc/Umler equipment ID (if available). |  |  |
| Aar Mechanical Designation | string | AAR mechanical type code (e.g., XM, TILX tank types, etc.). |  |  |
| Railcar Type | string | Box, Tank, Covered Hopper, Open Hopper, Flat, Gondola, Intermodal Well, Auto … |  |  |
| Builder | string | Manufacturer/builder of railcar or container. |  |  |
| Model | string | Model or configuration (e.g., 53' well car, 60' boxcar). |  |  |
| Build Year | integer | Year the asset was manufactured. |  |  |
| Refurbishment Year | integer | Most recent major refurbishment/overhaul year, if any. |  |  |
| Container Number | string | ISO container number (Owner code + serial + check digit). |  |  |
| Container Owner Code | string | Owner/operator code (e.g., MSCU, MAEU, CXRU). |  |  |
| Iso Size Type Code | string | ISO 6346 size/type code (e.g., 22G1, 45R1). |  |  |
| container size FT | integer | Nominal container length in feet (20, 40, 45, 48, 53). |  |  |
| Container Height FT | double | Container height in feet (8.6, 9.6 for high-cube, etc.). |  |  |
| Container Type | string | Dry, Reefer, Tank, Flat Rack, Open Top, Platform, Bulk, Other. |  |  |
| Container Material | string | Primary material (Steel, Aluminum, Composite). |  |  |
| Interior Length MM | double | Interior length (mm). |  |  |
| Interior width MM | double | Interior width (mm). |  |  |
| Interior Height MM | double | Interior height (mm). |  |  |
| Door Width MM | double | Container/railcar door width (mm), if applicable. |  |  |
| Door Height MM | double | Container/railcar door height (mm), if applicable. |  |  |
| Tare Weight KG | double | Asset tare weight (kg). |  |  |
| Max Gross Weight KG | double | Maximum gross weight (kg). |  |  |
| Payload Capacity KG | double | Maximum payload capacity (kg). |  |  |
| Volume Capacity CBM | double | Cargo volume capacity (cubic meters), if applicable. |  |  |
| Gross Rail Load KG | double | Railcar Gross Rail Load capacity (kg), if applicable. |  |  |
| Load Limit KG | double | Railcar load limit (kg). |  |  |

### `regulatory`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| CSC Plate Number | string | CSC safety approval plate number (containers). |  |  |
| CSC Approval Date | date | Date of CSC approval issue. |  |  |
| CSC Next Inspection Due Date | date | Next CSC periodic examination due date. |  |  |
| ACEP Program Flag | boolean | True if the container is enrolled in the ACEP continuous examination programme. | ✓ |  |
| ACEP Number | string | ACEP programme number / identifier. |  |  |
| AAR Pool ID | string | AAR / TTX pool identifier if the asset is a pooled asset. |  |  |
| Hazmat Approved Flag | boolean | Whether the asset is approved for hazardous materials transport. | ✓ |  |
| Hazmat UN Number | string | UN number of hazardous commodity when applicable. |  |  |
| Hazmat Class | string | Hazard class / division (IMDG / DOT). |  |  |
| Regulatory Compliance Status | string | Current regulatory compliance classification. | ✓ | ✓ |

### `investments`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Event Of Default Flag | boolean | Indicates if an Event of Default has occurred. |  |  |
| Event Of Default Date | date | Date Event of Default occurred. |  |  |
| Repossessed Date | date | Date asset was repossessed (if applicable). |  |  |
| Storage Fees Cumulated | double | Cumulative storage/depot fees incurred. |  |  |
| Remarketing Costs Cumulated | double | Cumulative remarketing costs incurred. |  |  |
| Sale Date | date | Date asset was sold/disposed. |  |  |
| Sale Price | double | Net proceeds from asset sale. |  |  |
| Issue Amount | amount | Total loan / facility amount at origination, including any undrawn commitment. |  | ✓ |
| Pool Addition Date | date | Date on which the asset was added to the securitisation or funding pool. |  |  |
| Purchased Principal | amount | Total principal amount purchased by the SPV or pledged by the borrower. |  | ✓ |
| UPB | amount | Unpaid principal balance as of the Reporting Date, excluding accrued interest… |  | ✓ |
| Accrued Interest | amount | Interest accrued on the outstanding balance but not yet collected as of the r… |  |  |
| Accrued Interest At Pool Addition Date | amount | Interest accrued but not yet paid when the loan entered the securitisation pool. |  |  |
| Original Maturity Date | date | Original contractual maturity date at origination, before any modification. |  |  |
| Maturity Date | date | Current contractual maturity date as of the Reporting Date. |  | ✓ |
| First Payment Date | date | Date the borrower made or is scheduled to make the first loan payment. |  |  |
| Last Payment Date | date | Date of the most recent payment received from the borrower. |  |  |
| Closing Date | date | Date on which the investment was closed (repaid, prepaid, written-off, or dec… |  |  |
| Performance Status | string | Current performance classification of the asset. | ✓ |  |
| Repayment Status | string | Terminal repayment / resolution status of the loan. | ✓ |  |
| DPD | integer | Days past due — days of delay on any expected cash flow, calculated based on … |  | ✓ |

### `calculated`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Mob Prepayment | integer | Months on books at which a prepayment event occurred. |  |  |
| Mob Cgl | integer | Months on books at which the asset first experienced a credit loss event (cha… |  |  |
| Mob Netloss | integer | Months on books used as the reference point for net loss calculations. |  |  |
| Remaining Term (months) | integer | Number of months remaining until the current maturity date. |  |  |
| asset Term | integer | Total contractual term of the asset expressed in months from origination to s… |  |  |
| Mob Recovery | integer | Months on books at which a recovery collection event was recorded. |  |  |
| Weighted Timing | integer | Weighted average timing metric used in cash flow modelling (e.g. weighted ave… |  |  |
| Asset Age (months) | integer | Age of the asset expressed in whole months elapsed since the issue date. |  |  |

### `lease`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Lease ID | string | Unique identifier for the lease agreement. |  |  |
| Lease Type | string | Classification of the lease structure. | ✓ | ✓ |
| Lease Start Date | date | Lease commencement date. |  |  |
| Lease End Date | date | Scheduled lease end date. |  |  |
| Off Hire Date | date | Date the asset went off-hire / was returned. |  |  |
| Rent Currency | string | Currency for lease rentals. |  |  |
| Rent Amount Periodic | amount | Base rent due per period in the lease currency. |  |  |
| Rent Payment Frequency | string | Frequency of rental payments. | ✓ |  |
| Per Diem Rate Amount | amount | Per diem usage rate for containers / railcars. |  |  |
| Free Days Allowance | integer | Number of free days before detention / demurrage charges apply. |  |  |
| Detention Rate Per Day | amount | Charge per day for late return / off-hire (detention). |  |  |
| Demurrage Rate Per Day | amount | Charge per day for equipment held at terminal / depot (demurrage). |  |  |
| Mileage Rate Per Mile | amount | Mileage revenue / charge per mile for railcars, if applicable. |  |  |
| Maintenance Responsibility | string | Party responsible for maintenance and repair costs under the lease. | ✓ |  |
| Return Condition Summary | string | Summary of return / off-hire condition requirements under the lease. |  |  |
| Utilisation Rate | percentage | Percentage of time the asset is on-hire / revenue-generating over the reporti… |  |  |
| Weighted Average Remaining Lease Term | integer | Weighted average remaining lease term across all active leases on the asset, … |  |  |

### `depot`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| On Hire Depot Location | string | Depot/terminal at on‑hire. |  |  |
| Off Hire Depot Location | string | Depot/terminal at off‑hire. |  |  |

### `lessee`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Lessee ID | string | Unique identifier for the lessee. |  |  |
| Lessee Legal Name | string | Legal name of the lessee / operator / shipper. |  |  |
| Lessee Country | string | Country of the lessee. |  |  |

### `operations`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset Status | string | Current operational status of the asset. | ✓ |  |
| Last Known Latitude | double | Last known latitude of the asset. |  |  |
| Last Known Longitude | double | Last known longitude of the asset. |  |  |
| Last Position Timestamp | date | Timestamp of the last position update. |  |  |
| Tracking Provider | string | Telematics / AEI / RFID / GPS provider or data source. |  |  |
| Last Station Code | string | Last reported rail station / terminal code, if available. |  |  |
| Train ID | string | Train identifier when associated with a specific move. |  |  |
| Waybill Number | string | Rail waybill number for the current or last move. |  |  |
| Interchange Railroad | string | Railroad carrier at last interchange. |  |  |
| Interchange Date | date | Date of the last interchange. |  |  |
| Loaded Flag | boolean | True if the asset is currently loaded. | ✓ |  |
| Commodity Description | string | Description of the commodity / cargo, if known. |  |  |
| Origin Location | string | Origin depot / terminal / station for the current or last move. |  |  |
| Destination Location | string | Destination depot / terminal / station for the current or last move. |  |  |
| Departure Date | date | Departure date for the current or last move. |  |  |
| Arrival Estimated Date | date | Estimated arrival date for the current or last move. |  |  |
| Arrival Actual Date | date | Actual arrival date for the current or last move. |  |  |
| YTD Mileage KM | double | Year-to-date mileage in kilometres for railcars. |  |  |
| Lifetime Mileage KM | double | Cumulative lifetime mileage in kilometres for railcars. |  |  |
| Lifts YTD | integer | Number of lift-on / lift-off events year-to-date (containers). |  |  |

### `appraisal`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Appraised Value Current Market | amount | Current market value estimate of the asset as of the appraisal date. |  |  |
| Residual Value At Lease End | amount | Assumed residual value of the asset at the scheduled lease end date. |  |  |
| Insured Value | amount | Insured value of the asset as per the current insurance policy. |  |  |
| Scrap Value Estimate | amount | Estimated scrap value based on material content and current market rates. |  |  |
| Appraisal Date | date | Date of the latest formal appraisal or valuation of the asset. |  |  |
| Appraisal Date | date | Date of latest appraisal/valuation. |  |  |
| Appraised Value Current Market | double | Current market value estimate. |  |  |
| Residual Value At Lease End | double | Assumed residual value at scheduled lease end. |  |  |
| Scrap Value Estimate | double | Estimated scrap value based on steel/aluminum content/market. |  |  |

### `maintenance`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Last Inspection Date | date | Date of last inspection (AAR/CSC). | ✓ |  |
| Next Inspection Due Date | date | Next scheduled inspection due date. | ✓ |  |
| Maintenance Status | string | Up‑to‑date, Due Soon, Overdue, In Shop. |  |  |
| Repair Event ID | string | Identifier of last repair event. |  |  |
| Repair Date | date | Date of last repair. | ✓ |  |
| Repair Category | string | Running Repair, Heavy Shop, Damage, Wreck, Cosmetic, Other. |  | ✓ |
| Repair Cost Amount | double | Cost of last repair. |  | ✓ |
| Damage Code | string | Standard damage/condition code if used (IICL/AAR). |  |  |
| Condition Grade | string | For containers: IICL, Cargo Worthy, Wind & Water Tight, As‑Is. |  | ✓ |
| Air Brake Test Date | date | Date of last Single Car Air Brake Test (railcars), if tracked. |  |  |
| Wheelset Last Service Date | date | Date of last wheelset service/replacement (railcars). |  |  |
| Reefer Setpoint c | double | Reefer setpoint temperature (°C), if applicable. |  |  |
| Reefer Running Hours | double | Cumulative reefer running hours. |  |  |

### `insurance`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Insured Value | double | Insured value of the asset. |  |  |
| Insurance Expiration Date | date | Insurance expiration date. |  |  |

### `security interest`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Security Interest Type | string | UCC Filing, Mortgage/Charge, Pledge of Shares, Assignment of Leases/Insurances. |  |  |
| Security Registration Reference | string | Jurisdictional registration reference number. |  |  |
| Security Registration Date | date | Date of security interest registration. |  |  |

### `cash_flows`

| Field | Type | Description | Enum? | Required for KPI |
|-------|------|-------------|-------|-----------------|
| Asset ID | string | uid value that uniquely identifies the asset within the originator’s database. |  | ✓ |
| CF Reference Date | date | date when the borrower made the payment. |  |  |
| Type | string | type of cash flow as per defined list of values | ✓ | ✓ |
| Expected Amount | amount | Contractually scheduled payment amount due on the payment date. |  | ✓ |
| Effective Amount | amount | paid amount at the reference date. |  |  |
