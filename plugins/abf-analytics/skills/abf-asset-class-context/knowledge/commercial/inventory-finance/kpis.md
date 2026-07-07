---
title: Commercial — Inventory Finance
tier: sub:commercial/inventory-finance
kpi_count: 19
inherits_from:
  - commercial/common/kpis
---

# Commercial — Inventory Finance

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

Shows how old the loans in the pool are, in months since origination. Useful because default risk typically peaks in the early months of a loan's life, so understanding pool seasoning helps anticipate when losses are most likely to emerge.

**Computation**

```
Group by: Reporting Date, Loan Age Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • Current Principal Balance = Sum of Current Principal Balances
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Asset Type Distribution
_Category: Stratification_

**Purpose**

Splits the portfolio by the type of financed inventory (e.g. Vehicles, Electronics, Machinery, Consumer Goods, Agricultural Equipment). Different inventory types carry materially different liquidation values, turn rates, and loss severities in the event of dealer default, making asset type the primary collateral risk stratification in inventory finance.

**Computation**

```
Group by: Reporting Date, Asset Type / Product Category

Metrics:
Total Units = Count of asset IDs
Open Units = Count of asset IDs where asset is not Closed
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Units / Total Units for the Reporting Date
```

### Collateral Type
_Category: Stratification_

**Purpose**

Splits the pool by the type of financed asset (e.g. Railcar, Intermodal Container, Chassis). Different collateral types carry materially different depreciation profiles, re-lease demand, residual values, and regulatory requirements, making collateral type the primary risk stratification for this asset class.

**Computation**

```
Group by: Reporting Date, Asset Type
Metrics:

Total Assets = Count of Asset IDs
Open Assets = Count of Asset IDs where Asset is not Closed
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Company Name
_Category: Stratification_

**Purpose**

Shows how the pool is split across lessees by asset count and balance. Flags concentration in a single lessee and supports performance comparison when credit quality or operational reliability differs between counterparties. A single lessee returning assets en masse can sharply reduce utilisation and pool cash flows.

**Computation**

```
Group by: Reporting Date, Lessee Legal Name
Metrics:

Total Assets = Count of Asset IDs
Open Assets = Count of Asset IDs where Asset is not Closed
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

### Insurance Score
_Category: Stratification_

**Purpose**

Distributes the pool by the insured value coverage ratio of each asset, measured as insured value relative to current appraised market value. Under-insured assets expose the pool to unrecovered losses in the event of damage, total loss, or theft. A declining coverage ratio signals that insurance has not kept pace with asset valuations.

**Computation**

```
Insurance Coverage Ratio (%) = Insured Value / Appraised Value Current Market × 100
Bands: Below 80% | 80–90% | 90–100% | 100–110% | Above 110%
Group by: Reporting Date, Insurance Coverage Band
Metrics:

Total Assets = Count of Asset IDs
Open Assets = Count of Asset IDs where Asset is not Closed
UPB = Sum of UPB
Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Assets / Total Assets for the Reporting Date
```

### Inventory Turn Rate
_Category: Stratification_

**Purpose**

Measures how quickly financed inventory units are being sold and the corresponding loan repaid. A declining inventory turn rate signals that dealers are holding stock longer than expected, increasing the risk of aged inventory, forced discounting, and ultimately floorplan default. It is the most operationally specific metric for inventory finance.

**Computation**

```
Inventory Turn Rate = Number of Units Sold and Repaid in Period / Average Units Financed in Period
Group by: Reporting Date, Originator Name

Metrics:
Units Repaid in Period = Count of Loan IDs with full repayment in period
Average Units Outstanding = (Opening Count + Closing Count) / 2
Turn Rate = Units Repaid / Average Units Outstanding
Annualized Turn Rate = Turn Rate × (12 / Period Length in Months)
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
