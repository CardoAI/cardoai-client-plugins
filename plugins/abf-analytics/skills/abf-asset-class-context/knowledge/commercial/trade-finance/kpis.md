---
title: Commercial — Trade Finance
tier: sub:commercial/trade-finance
kpi_count: 15
inherits_from:
  - commercial/common/kpis
---

# Commercial — Trade Finance

> Inherits from: _global/kpis, commercial/common/kpis. Override: child KPI with same `### name` wins.

## Risk Metrics

### Cumulative Recovery
_Category: Risk Metric_

**Purpose**

Total cash recovered from charged off assets as a share of total charge offs, the empirical recovery rate of the pool. Together with gross charge off, this determines the actual economic loss suffered.

**Computation**

```
Cumulative Gross Recoveries Amount = Sum of all Recovery Amounts Collected up to Reporting Date

Cumulative Recovery Rate = Cumulative Gross Recovered Amount / Total Charge Off Amount
```

### DSO
_Category: Risk Metric_

**Purpose**

Measures the average number of days it takes debtors to pay their invoices, as of the reporting date. A rising DSO signals deteriorating debtor payment behavior or a shift toward longer-tenor invoices in the portfolio, while a declining DSO indicates improving collection efficiency. It is the primary metric for trade receivables portfolios, allowing investors to monitor debtor payment patterns and benchmark collection performance.

**Computation**

```
Group by: Reporting Date
Metrics:

Outstanding Receivables = Sum of UPB
Total Invoice Amount = Sum of Trade Receivable Amounts in the period
Number of Days = Number of calendar days in the reporting period
DSO = (Outstanding Receivables / Total Invoice Amount) × Number of Days in Period
Best Possible DSO = (Sum of UPB where Days in Delay = 0 / Total Invoice Amount) × Number of Days in Period
Delinquent DSO = DSO − Best Possible DSO
```

### Periodic CGL
_Category: Risk Metric_

**Purpose**

Measures the fresh defaults hitting the pool in each reporting period. A rising periodic default rate is typically the first sign that credit quality is deteriorating and that future losses will be higher.

**Computation**

```
Periodic CGL = Cumulative CGL − Previous Cumulative CGL

Periodic CGL Rate = (Cumulative CGL − Previous Cumulative CGL) / Previous Non-Default Principal Amount
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

Compares prepayment curves across origination cohorts at the same asset age. Reveals whether a prepayment spike is isolated to a specific booking period or is a wider portfolio trend.

**Computation**

```
Months on Book (MOB) = Ceiling of Days between Issue Date and Prepayment Date / 30.5

Prepayment Ratio = Prepaid Principal Amount / Total Issue Amount for that Issue Date Cohort
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

### APR
_Category: Stratification_

**Purpose**

Distributes the pool by interest rate charged. Higher APR assets generate more income but typically carry higher credit risk, so the APR distribution reflects the risk-return balance of the pool.

**Computation**

```
Group by: Reporting Date, APR Band

Metrics:
  • Total assets = Count of asset IDs
  • Open assets = Count of asset IDs where asset is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Aging
_Category: Stratification_

**Purpose**

Shows how old the assets in the pool are, in months since origination. Useful because default risk typically peaks in the early months of a asset's life, so understanding pool seasoning helps anticipate when losses are most likely to emerge.

**Computation**

```
Group by: Reporting Date, Asset Age Band

Metrics:
  • Total assets = Count of asset IDs
  • Open assets = Count of asset IDs where asset is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Company Name
_Category: Stratification_

**Purpose**

Shows how the pool is split across lessees by asset count and balance. Flags concentration in a single lessee and supports performance comparison when credit quality or operational reliability differs between counterparties. A single lessee returning assets en masse can sharply reduce utilisation and pool cash flows.

**Computation**

```
Group by: Reporting Date, Company Name
Metrics:

Total Assets = Count of Asset IDs
Open Assets = Count of Asset IDs where Asset is not Closed
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Current Principal Balance
_Category: Stratification_

**Purpose**

Distributes open assets by their remaining outstanding balance. Reflects how the pool is amortising in practice and whether any assets are paying down more slowly than their contractual schedule suggests.

**Computation**

```
Group by: Reporting Date, Current Principal Balance Band

Metrics:
  • Total assets = Count of asset IDs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Geography Distribution
_Category: Stratification_

**Purpose**

Splits the pool by borrower state. Flags geographic concentration that could expose the portfolio to localised economic shocks or differences in legal enforcement across jurisdictions.

**Computation**

```
Group by: Reporting Date, State

Metrics:
  • Total assets = Count of asset IDs
  • Open assets = Count of asset IDs where asset is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
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

Shows how the pool is split by original asset length. Drives the expected duration and amortisation profile of the portfolio and influences how long the deal needs to remain open.

**Computation**

```
Asset Term (months) = Months between Issue Date and Maturity Date

Group by: Reporting Date, Asset Term

Metrics:
  • Total assets = Count of asset IDs
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Originator
_Category: Stratification_

**Purpose**

Shows how the pool is split across originators by asset count and balance. Flags concentration in a single originator and supports performance comparison when underwriting quality differs between originators.

**Computation**

```
Group by: Reporting Date, Originator Name

Metrics:
  • Total assets = Count of asset IDs
  • Open assets = Count of asset IDs where asset is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```

### Remaining Term to Maturity
_Category: Stratification_

**Purpose**

Distributes open assets by how much contractual life is left. Gives a live view of how quickly the portfolio is running down and whether new assets are needed to maintain the deal's target duration.

**Computation**

```
Remaining Term (months) = Remaining Term in Years × 12

Group by: Reporting Date, Remaining Term Band

Metrics:
  • Total assets = Count of asset IDs
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of assets / Total assets for the Reporting Date
```
