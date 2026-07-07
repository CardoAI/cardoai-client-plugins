---
title: Consumer — Home Improvement
tier: sub:consumer/home-improvement
kpi_count: 23
inherits_from:
  - consumer/common/kpis
---

# Consumer — Home Improvement

> Inherits from: _global/kpis, consumer/common/kpis. Override: child KPI with same `### name` wins.

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

### Delta
_Category: Risk Metric_

**Purpose**

The difference between actual and expected collections, both for the current period and cumulatively. A persistent negative delta means the pool is consistently underdelivering against its contractual cash flow schedule.

**Computation**

```
Periodic Delta = Periodic Realized − Periodic Expected

Cumulative Delta = Cumulative Realized − Cumulative Expected
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
  • Current Principal Balance = Sum of Current Principal Balances
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
  • Current Principal Balance = Sum of Current Principal Balances
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Annual Debtor Income
_Category: Stratification_

**Purpose**

Distributes the pool by borrower income band. Provides a sense of the borrower base's financial resilience and helps assess how sensitive the pool is to economic downturns or wage pressures.

**Computation**

```
Group by: Reporting Date, Primary Income Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • Current Principal Balance = Sum of Current Principal Balances
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Fico
_Category: Stratification_

**Purpose**

Distributes the pool by credit score band. Tracks whether the borrower credit quality profile is shifting over time relative to what was underwritten at deal close.

**Computation**

```
Group by: Reporting Date, FICO Score Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
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

### Housing Type
_Category: Stratification_

**Purpose**

Splits the pool by the type of dwelling being improved (e.g. detached house, semi-detached, terraced, flat). Different housing types carry different collateral values and improvement cost profiles, which affects both loan sizing adequacy and the likelihood the improvement adds value to the underlying asset.

**Computation**

```
Group by: Reporting Date, Housing Type

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Interior Level
_Category: Stratification_

**Purpose**

Splits the pool by the scope or grade of the improvement work being financed (e.g. basic refurbishment, mid-range renovation, premium fit-out). Higher-grade projects tend to carry larger loan balances and longer completion timelines, increasing the risk of cost overruns or project abandonment — both of which can impair the borrower's ability to repay.

**Computation**

```
Group by: Reporting Date, Interior Level

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Merchant Distribution
_Category: Stratification_

**Purpose**

Splits the pool by the sector or purpose of each loan. Identifies if the portfolio is overly concentrated in a single industry, which could create correlated risk if that sector experiences stress.

**Computation**

```
Group by: Reporting Date, Seller Merchant Code

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Occupancy Status
_Category: Stratification_

**Purpose**

Distributes the pool by whether the borrower occupies the property as a primary residence, secondary home or rental. Owner-occupiers typically have stronger repayment incentives as the property is their home; buy-to-let or vacant properties carry higher default and recovery risk.

**Computation**

```
Group by: Reporting Date, Occupancy Status

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
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
  • UPB = Sum of UPB
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

### Ownership Type
_Category: Stratification_

**Purpose**

Splits the pool by how the borrower holds title to the property (e.g. sole owner, joint ownership, shared ownership). Ownership structure affects the lender's ability to enforce against the asset, joint or shared ownership arrangements introduce additional legal complexity that can slow recovery timelines and reduce net proceeds.

**Computation**

```
Group by: Reporting Date, Ownership Type

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### PTI
_Category: Stratification_

**Purpose**

Distributes the pool by how much of a borrower's income goes toward their loan payment. Higher PTI concentrations mean the pool is more exposed if borrowers experience an income shock.

**Computation**

```
Group by: Reporting Date, PTI Band

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Property Type
_Category: Stratification_

**Purpose**

Distributes the pool by the structural classification of the property (e.g. freehold, leasehold, new build). Property type affects the legal enforcement position of the lender and the resale liquidity of the underlying asset, both of which are relevant to recovery assumptions in a default scenario.

**Computation**

```
Group by: Reporting Date, Property Type

Metrics:
  • Total Loans = Count of Loan IDs
  • Open Loans = Count of Loan IDs where Loan is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of Loans / Total Loans for the Reporting Date
```

### Re-status
_Category: Stratification_

**Purpose**

Tracks the share of loans that have been modified, restructured or placed into a special status (e.g. forbearance, payment holiday, renegotiated terms). A growing re-status concentration signals that a portion of the pool is under financial stress and has been treated outside its original contractual terms, which affects both cash flow timing and ultimate loss expectations.

**Computation**

```
Group by: Reporting Date, Re-status
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

### Scheduled Payment per Month
_Category: Stratification_

**Purpose**

Distributes the pool by the monthly payment amount each borrower owes. Shows the absolute debt service burden on borrowers and feeds into cash flow forecasting for the deal waterfall.

**Computation**

```
Group by: Reporting Date, Scheduled Payment Amount Band

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
