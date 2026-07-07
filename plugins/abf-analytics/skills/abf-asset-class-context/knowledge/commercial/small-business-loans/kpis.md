---
title: Commercial — Small Business Loans
tier: sub:commercial/small-business-loans
kpi_count: 21
inherits_from:
  - commercial/common/kpis
---

# Commercial — Small Business Loans

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

Distributes the pool by interest rate charged. Higher APR loans generate more income but typically carry higher credit risk, so the APR distribution reflects the risk-return balance of the pool.

**Computation**

```
Group by: Reporting Date, APR Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
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
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Company Name
_Category: Stratification_

**Purpose**

Identifies the largest borrower exposures within the pool by name, allowing monitoring of single-name concentration risk. Large exposures to a single company can create outsized losses if that borrower defaults.

**Computation**

```
Group by: Reporting Date, Company Name

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = UPB / Total UPB for the Reporting Date
```

### Company Risk Score
_Category: Stratification_

**Purpose**

Distributes the pool across obligor risk score bands. Shows the full credit quality spectrum of the pool and whether it is migrating toward higher-risk bands over time which is an early warning of future default deterioration before it appears in DPD or CGL metrics.

**Computation**

```
Group by: Reporting Date, Company Risk Score Band. 

Metrics: 
Total Contracts = Count of Contract IDs; 
Open Contracts = Count of Contract IDs where Is Closed = False; 
UPB Outstanding = Sum of Principal Outstanding; 
Face Value = Sum of Face Values. 

Weight % = Number of Contracts / Total Contracts for the Reporting Date.
```

### Company Sector
_Category: Stratification_

**Purpose**

Splits the pool by the sector or purpose of each loan. Identifies if the portfolio is overly concentrated in a single industry, which could create correlated risk if that sector experiences stress.

**Computation**

```
Group by: Reporting Date, Company Sector Code

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Company Type Distribution
_Category: Stratification_

**Purpose**

Breaks the pool down by the legal or structural classification of the borrowing entity (e.g. Parent, Subsidiary, Standalone). Helps identify whether credit risk is concentrated in entities that depend on a parent for cash flows or guarantees.

**Computation**

```
Group by: Reporting Date, Company Type

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Enterprise Size
_Category: Stratification_

**Purpose**

Distributes the pool across enterprise size categories (Micro, Small, Medium, Large). Smaller businesses typically carry higher default risk and lower recovery rates, so the size mix directly affects expected loss assumptions.

**Computation**

```
Group by: Reporting Date, Enterprise Size

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Geography Distribution
_Category: Stratification_

**Purpose**

Splits the pool by State. Flags geographic concentration that could expose the portfolio to localised economic shocks or differences in legal enforcement across jurisdictions.

**Computation**

```
Group by: Reporting Date, State

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Insurance Score
_Category: Stratification_

**Purpose**

Distributes the pool by the credit or risk score assigned by the insurer covering each borrower. Where government or private guarantee schemes are in place, the insurance score reflects an independent risk assessment that can be benchmarked against the originator's own underwriting view.

**Computation**

```
Group by: Reporting Date, Insurance Score Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Original Balance
_Category: Stratification_

**Purpose**

Distributes the pool by the size of each loan at origination. A pool of many small loans is well-diversified; a pool with a few very large loans carries higher single-borrower concentration risk.

**Computation**

```
Group by: Reporting Date, Original Balance Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
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
  • UPB = Sum of UPBs
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
  • UPB = Sum of UPBs
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
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Scheduled Payment per Month
_Category: Stratification_

**Purpose**

Distributes the pool by the monthly payment amount each borrower owes. Shows the absolute debt service burden on borrowers and feeds into cash flow forecasting for the deal waterfall.

**Computation**

```
Group by: Reporting Date, Contractual Payment Amount Current Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPBs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### UPB
_Category: Stratification_

**Purpose**

Distributes open loans by their remaining outstanding balance. Reflects how the pool is amortising in practice and whether any loans are paying down more slowly than their contractual schedule suggests.

**Computation**

```
Group by: Reporting Date, UPB Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```
