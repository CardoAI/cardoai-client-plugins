---
title: Consumer — Credit Cards
tier: sub:consumer/credit-cards
kpi_count: 12
inherits_from:
  - consumer/common/kpis
---

# Consumer — Credit Cards

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
  • UPB = Sum of UPB
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
  • Total accounts = Count of account IDs
  • Open accounts = Count of account IDs where account is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of accounts / Total accounts for the Reporting Date
```

### Credit Limit
_Category: Stratification_

**Purpose**

Splits the portfolio by the credit limit on each card to analyze exposure by available credit. This helps identify concentrations of high or low credit limits, assess risk distribution, and understand potential loss or utilization patterns across different credit tiers.

**Computation**

```
Group by: Reporting Date, Credit Limit

Metrics:
  • Total accounts = Count of account IDs
  • Open accounts = Count of account IDs where account is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of accounts / Total accounts for the Reporting Date
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

### Utilization
_Category: Stratification_

**Purpose**

Splits the portfolio by the utilization rate of each credit card account to analyze exposure by balance-to-limit ratio. This helps identify concentrations of highly leveraged or underleveraged accounts, assess credit risk distribution, and understand revolving behavior and payment patterns across different utilization tiers.

**Computation**

```
Group by: Reporting Date, Utilization

Metrics:
  • Total accounts = Count of account IDs
  • Open accounts = Count of account IDs where account is not Closed
  • UPB = Sum of UPB
  • Purchased Principal = Sum of Purchased Principal Amounts

Weight % = Number of accounts / Total accounts for the Reporting Date
```
