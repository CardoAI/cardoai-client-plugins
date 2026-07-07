---
title: Commercial — Revenue Based Finance
tier: sub:commercial/revenue-based-finance
kpi_count: 19
inherits_from:
  - commercial/common/kpis
---

# Commercial — Revenue Based Finance

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
Cumulative Gross Recoveries = Sum of all Gross Recovery Amounts

Cumulative Recovery Rate = Cumulative Gross Recoveries / Total Charge Off Amount
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
Periodic Gross Recoveries = Sum of Gross Recoveries

Periodic Recovery Rate = Periodic Gross Recoveries / Previous Outstanding Charge Off Balance
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

Recovery Rate = Cumulative Gross Recoveries / Total Charge Off Principal for that Issue Date Cohort
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

### Borrower Name
_Category: Stratification_

**Purpose**

Identifies the largest borrower exposures within the pool by name, allowing monitoring of single-name concentration risk. Large exposures to a single company can create outsized losses if that borrower defaults.

**Computation**

```
Group by: Reporting Date, Borrower Name

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
UPB = Sum of Principal Outstanding; 
Face Value = Sum of Face Values. 

Weight % = Number of Contracts / Total Contracts for the Reporting Date.
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

### Installment Capital Amount
_Category: Stratification_

**Purpose**

Distributes the pool by the installment capital amount each borrower owes. Shows the absolute debt service burden on borrowers and feeds into cash flow forecasting for the deal waterfall.

**Computation**

```
Group by: Reporting Date, Installment Capital Amount

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

Distributes the pool by insurer-assigned risk score bands. Provides an independent third-party credit quality view that can be benchmarked against originator underwriting. A divergence between the two signals potential underestimation of credit risk in the pool.

**Computation**

```
Group by: Reporting Date, Insurance Score Band. 
Metrics: 
Total Loans = Count of Loan IDs; 
Open Loans = Count of Loan IDs where Is Closed = False; 
UPB = Sum of Loan Current Balances; 
Purchased Principal = Sum of Purchased Principal Amounts. 

Weight % = Number of Loans / Total Loans for the Reporting Date.
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

### Sales Reporting Frequency
_Category: Stratification_

**Purpose**

Distributes the pool by how often borrowers report revenue. Since RBF repayments are tied to reported revenue, less frequent reporting (e.g. quarterly) creates information lag risk — the lender detects revenue declines later and has less time to react.

**Computation**

```
Group by: Reporting Date, Sales Reporting Frequency. 

Metrics: 
Total Loans = Count of Loan IDs; 
Open Loans = Count of Loan IDs where Is Closed = False; 
UPB = Sum of Loan Current Balances; 
Purchased Principal = Sum of Purchased Principal Amounts. 

Weight % = Number of Loans / Total Loans for the Reporting Date.
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
