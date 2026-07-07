---
title: Commercial — Rail Cars And Containers
tier: sub:commercial/rail-cars-and-containers
kpi_count: 20
inherits_from:
  - commercial/common/kpis
---

# Commercial — Rail Cars And Containers

> Inherits from: _global/kpis, commercial/common/kpis. Override: child KPI with same `### name` wins.

## Risk Metrics

### CPR
_Category: Risk Metric_

**Purpose**

Converts the monthly prepayment pace into an annualised rate so it can be compared consistently across deals and time periods. A rising CPR means the pool is shortening faster than planned.

**Computation**

```
CPR = 1 − (1 − Monthly Prepayment Rate) ^ 12

Where:
Monthly Prepayment Rate = (Cumulative Prepayment − Previous Cumulative Prepayment) / (Previous UPB − Contractual Payment Amount Current)

If Previous UPB is null or zero, CPR = null
```

### Cumulative Recovery
_Category: Risk Metric_

**Purpose**

Total cash recovered from charged off assets as a share of total charge offs, the empirical recovery rate of the pool. Together with gross charge off, this determines the actual economic loss suffered.

**Computation**

```
Cumulative Gross Recoveries Amount = Sum of all Recovery Amounts Collected up to Reporting Date

Cumulative Recovery Rate = Cumulative Gross Recovered Amount / Total Charge Off Amount
```

### Maintenance Cost Ratio
_Category: Risk Metric_

**Purpose**

Tracks total repair and maintenance spend as a percentage of rental income generated. Rising maintenance costs erode net cash flow and may signal ageing fleet issues or lessee misuse. Particularly important for older railcars and high-cycle containers.

**Computation**

```
Periodic Maintenance Cost = Sum of Repair Cost Amounts in Period
Periodic Rental Income = Sum of Realized Amounts where Cash Flow Subtype = Lease Rental or Per Diem
Maintenance Cost Ratio (%) = Periodic Maintenance Cost / Periodic Rental Income × 100

Group by: Reporting Date, Asset Type, Repair Category
```

### Periodic CGL
_Category: Risk Metric_

**Purpose**

Measures the fresh charge off hitting the pool in each reporting period. A rising periodic charge off rate is typically the first sign that credit quality is deteriorating and that future losses will be higher.

**Computation**

```
Periodic CGL = Cumulative CGL − Previous Cumulative CGL

Periodic CGL Rate = (Cumulative CGL − Previous Cumulative CGL) / Previous Non-Charge Off Principal Amount
```

### Periodic Recovery
_Category: Risk Metric_

**Purpose**

Cash collected from already-charged off borrowers in each period, measured against the outstanding charged off balance. Shows whether the collections and enforcement process is generating cash at a consistent pace.

**Computation**

```
Periodic Gross Recovered Amount = Sum of Recovery Amounts Collected in the Period

Periodic Recovery Rate = Periodic Gross Recovered Amount / Previous Outstanding Charge Off Balance
```

### Vintage Prepayment
_Category: Risk Metric_

**Purpose**

Compares prepayment curves across origination cohorts at the same loan age. Reveals whether a prepayment spike is isolated to a specific booking period or is a wider portfolio trend.

**Computation**

```
Months on Book (MOB) = Ceiling of Days between Issue Date and Prepayment Date / 30.5

Prepayment Ratio = Prepaid Principal Amount / Total Original Balance for that Issue Date Cohort
```

### Vintage Recovery
_Category: Risk Metric_

**Purpose**

Plots recovery cash flows against months since charge off for each cohort. Useful for understanding how long it takes to extract recoveries and whether that timeline is consistent across booking periods.

**Computation**

```
Months Since Charge Off = Ceiling of Days between Charge Off Date (or Recovery Date if no Charge Off Date) and Recovery Date / 30.5

Recovery Rate = Cumulative Gross Recovered Amount / Total Charge Off Principal for that Issue Date Cohort
```

## Stratifications

### Aging
_Category: Stratification_

**Purpose**

Shows how old the loans in the pool are, in months since origination. Useful because default risk typically peaks in the early months of a loan's life, so understanding pool seasoning helps anticipate when losses are most likely to emerge.

**Computation**

```
Group by: Reporting Date, Loan Age Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Condition Grade Distribution
_Category: Stratification_

**Purpose**

Distributes the pool by the physical condition grade of assets. Deteriorating condition grades signal higher maintenance spend ahead, lower re-lease rates, and reduced residual values. A shift toward As-Is or Wind & Water Tight grades is an early warning of fleet quality decline.

**Computation**

```
Group by: Reporting Date, Condition Grade

Metrics:
Total Assets = Count of Asset IDs
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts
Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Geography Distribution
_Category: Stratification_

**Purpose**

Splits the pool by state. Flags geographic concentration that could expose the portfolio to localised economic shocks or differences in legal enforcement across jurisdictions.

**Computation**

```
Group by: Reporting Date, State

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Lease Type
_Category: Stratification_

**Purpose**

Shows the split between operating leases, master leases, per diem, and trip leases. Different lease structures carry different revenue predictability and residual value risk profiles. Concentration in short-term or per diem leases increases re-leasing risk and cash flow volatility, while long-term leases provide more stable and predictable income to the pool.

**Computation**

```
Group by: Reporting Date, Lease Type
Metrics:

Total Assets = Count of Asset IDs
Open Assets = Count of Asset IDs where Asset is not Closed
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Lessee Industry Sector
_Category: Stratification_

**Purpose**

Splits the pool by the sector or purpose of each asset. Identifies if the portfolio is overly concentrated in a single industry, which could create correlated risk if that sector experiences stress.

**Computation**

```
Group by: Reporting Date, Lessee Industry Sector

Metrics:
  • Total assets = Count of asset IDs
  • Open assets = Count of asset IDs where asset is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Lessee Type
_Category: Stratification_

**Purpose**

Distributes the pool by the operational classification of the lessee (e.g. Railroad Operator, Shipping Line, Freight Forwarder, Industrial Shipper). Different lessee types operate under different demand cycles and credit dynamics. Concentration in a single lessee type creates correlated risk if that segment experiences an industry-wide downturn or regulatory disruption.

**Computation**

```
Group by: Reporting Date, Lessee Type
Metrics:

Total Assets = Count of Asset IDs
Open Assets = Count of Asset IDs where Asset is not Closed
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Original Balance
_Category: Stratification_

**Purpose**

Distributes the pool by the size of each asset at origination. A pool of many small assets is well-diversified; a pool with a few very large assets carries higher single-borrower concentration risk.

**Computation**

```
Group by: Reporting Date, Issue Amount Band

Metrics:
  • Total assets = Count of asset IDs
  • Open assets = Count of asset IDs where asset is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Original Term to Maturity
_Category: Stratification_

**Purpose**

Shows how the pool is split by original loan length. Drives the expected duration and amortisation profile of the portfolio and influences how long the deal needs to remain open.

**Computation**

```
Loan Term (months) = Months between Issue Date and Maturity Date

Group by: Reporting Date, Loan Term

Metrics:
  • Total Loans = Count of Loan IDs
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Originator
_Category: Stratification_

**Purpose**

Shows how the pool is split across originators by loan count and balance. Flags concentration in a single originator and supports performance comparison when underwriting quality differs between originators.

**Computation**

```
Group by: Reporting Date, Originator Name

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Regulatory Compliance Distribution
_Category: Stratification_

**Purpose**

Shows what share of assets are compliant, due for inspection, overdue, or restricted from service. Non-compliant or restricted assets cannot be placed on lease, creating forced off-lease drag and potential legal liability for the pool.

**Computation**

```
Group by: Reporting Date, Regulatory Compliance Status

Metrics:
Total Assets = Count of Asset IDs
UPB = Sum of UPB
Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Remaining Term to Maturity
_Category: Stratification_

**Purpose**

Distributes open loans by how much contractual life is left. Gives a live view of how quickly the portfolio is running down and whether new assets are needed to maintain the deal's target duration.

**Computation**

```
Remaining Term (months) = Remaining Term in Years × 12

Group by: Reporting Date, Remaining Term Band

Metrics:
  • Total Loans = Count of Loan IDs
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Scheduled Payment per Month
_Category: Stratification_

**Purpose**

Distributes the pool by the monthly payment amount each borrower owes. Shows the absolute debt service burden on borrowers and feeds into cash flow forecasting for the deal waterfall.

**Computation**

```
Group by: Reporting Date, Contractual Payment Amount Current

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### UPB
_Category: Stratification_

**Purpose**

Distributes open loans by their remaining outstanding balance. Reflects how the pool is amortising in practice and whether any loans are paying down more slowly than their contractual schedule suggests.

**Computation**

```
Group by: Reporting Date, UPB 

Metrics:
  • Total Loans = Count of Loan IDs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```
