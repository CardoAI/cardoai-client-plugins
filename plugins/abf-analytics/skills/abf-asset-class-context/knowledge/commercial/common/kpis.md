---
title: Commercial — Common KPIs
tier: main:commercial
kpi_count: 15
inherits_from:
---

# Commercial — Common KPIs

> Inherits from: _global/kpis. Override: child KPI with same `### name` wins.

## Risk Metrics

### CDR
_Category: Risk Metric_

**Purpose**

Annualises the periodic charge off rate so performance can be compared across deals regardless of their age or reporting frequency. Used to monitor whether the pool is within agreed credit performance thresholds.

**Computation**

```
CDR = 1 − (1 − Monthly Charge Off Rate) ^ 12

Where:
Monthly Charge Off Rate = (Cumulative CGL − Previous Cumulative CGL) / Previous Non-Charge off Principal Amount

If Previous Non-Charge off Principal Amount is null or zero, CDR = null
```

### Cashflow Type
_Category: Risk Metric_

**Purpose**

Breaks the collection comparison down by type (principal, interest, fees, penalties). Pinpoints whether a shortfall is coming from borrowers not repaying principal (credit issue) or interest (rate or forbearance issue).

**Computation**

```
Scope: Exclude funding cashflow types; group by Payment Date and Cashflow Type

For each Payment Date × Cashflow Type:
  • Periodic Expected by Type = Sum of Expected Amounts
  • Periodic Realized by Type = Sum of Realized Amounts
  • Cumulative Expected by Type = Running Sum of Expected Amounts
  • Cumulative Realized by Type = Running Sum of Realized Amounts
```

### Collections
_Category: Risk Metric_

**Purpose**

Compares total cash received from the pool against what was contractually expected, excluding funding flows. The starting point for understanding whether the pool is delivering on its payment obligations.

**Computation**

```
Scope: Exclude funding cashflow types; include only payment dates up to latest sync date

Group by Payment Date:
  • Expected Amount = Sum of Expected Amounts
  • Realized Amount = Sum of Realized (Effective) Amounts
```

### Cumulative CGL
_Category: Risk Metric_

**Purpose**

Total gross charge off since pool inception as a share of the original balance. The benchmark figure used to assess whether actual credit losses are tracking within the envelope assumed when the deal was structured.

**Computation**

```
Cumulative CGL = Sum of all Charged Off Principal up to Reporting Date

Cumulative CGL Rate = Cumulative CGL / Original Balance
```

### Cumulative Cashflows
_Category: Risk Metric_

**Purpose**

Running total of expected versus actual collections since pool inception. Answers whether the pool has, in aggregate, generated the cash it was supposed to — smoothing out individual period noise.

**Computation**

```
Scope: Exclude funding cashflow types; include payment dates up to latest sync date

Running total by Payment Date:
  • Cumulative Expected = Running Sum of Expected Amounts
  • Cumulative Realized = Running Sum of Realized (Effective) Amounts
```

### Cumulative Net Loss
_Category: Risk Metric_

**Purpose**

Total irreversible principal losses since pool inception as a share of the original balance. The definitive measure of economic loss and the key input for sizing credit protection in the deal.

**Computation**

```
Cumulative Net Loss = Sum of all Loss Amounts up to Reporting Date

Cumulative Net Loss Rate = Cumulative Net Loss / Previous Non-Charge Of Principal
```

### Cumulative Prepayment
_Category: Risk Metric_

**Purpose**

Tracks the total early repayments since the deal started as a share of the original pool. The key check for whether the portfolio is paying down faster than assumed at inception.

**Computation**

```
Cumulative Prepayment = Sum of all Prepaid Principal Amounts up to Reporting Date

Cumulative Prepayment Rate = Cumulative Prepayment / Original Balance
```

### Delinquency
_Category: Risk Metric_

**Purpose**

Shows the share of the pool that is past due, split by how late payments are. Because loans must become delinquent before charging off, this is the earliest warning signal for future credit losses.

**Computation**

```
DPD Bucket Balance = Sum of UPB for Loans within each Days Past Due range:
  • 1–29 DPD
  • 30–59 DPD
  • 60–89 DPD
  • 90–119 DPD
  • 120–149 DPD
  • 150–180 DPD
  • 180+ DPD

DPD Bucket Rate = Bucket Balance / Total UPB for the Period
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

### Periodic Cashflows
_Category: Risk Metric_

**Purpose**

Period-by-period view of expected versus actual cash collected. Identifies whether a shortfall is a one-off timing issue or the beginning of a broader collection problem.

**Computation**

```
Scope: Exclude funding cashflow types; include payment dates up to latest sync date

For each Payment Date:
  • Periodic Expected = Sum of Expected Amounts
  • Periodic Realized = Sum of Realized (Effective) Amounts
```

### Periodic Net Loss
_Category: Risk Metric_

**Purpose**

Principal permanently written off in each period after all recovery attempts. Shows whether loss crystallisation is speeding up — a sign that cure rates or recoveries are weaker than expected.

**Computation**

```
Periodic Net Loss = Cumulative Net Loss − Previous Cumulative Net Loss

Periodic Net Loss Rate = (Cumulative Net Loss − Previous Cumulative Net Loss) / Previous Non-Charge Off Principal
```

### Periodic Prepayment
_Category: Risk Metric_

**Purpose**

Shows how much principal borrowers repaid early in a given period and how fast that is relative to the performing balance. Useful for spotting sudden changes in borrower behaviour that could shorten the portfolio's life and reduce interest income.

**Computation**

```
Periodic Prepayment = Cumulative Prepayment − Previous Cumulative Prepayment

Periodic Prepayment Rate = (Cumulative Prepayment − Previous Cumulative Prepayment) / (Previous UPB − Contractual Payment Amount Current)
```

### Recovery Timing
_Category: Risk Metric_

**Purpose**

Calculates the average time, weighted by charged off principal, between a loan charging off and cash being recovered. A longer recovery lag reduces the present value of those cash flows and increases the real cost of credit loss.

**Computation**

```
Calculated Timing = Sum of (Months from Charge Off to Recovery × Charge Off Principal Amount)

Weighted Average Timing = Calculated Timing / Total Charge Off Principal Amount
```

### Vintage CGL
_Category: Risk Metric_

**Purpose**

Tracks how charge off build up over time for each origination cohort. Identifies whether losses are front-loaded (origination quality issue) or back-loaded (macro or seasoning effect).

**Computation**

```
Months on Book (MOB) = Ceiling of Days between Issue Date and Charge off Date / 30.5

CGL Rate = Charged Off Principal Amount / Total Original Balance for that Issue Date Cohort
```

### Vintage Net Loss
_Category: Risk Metric_

**Purpose**

Compares ultimate loss curves across origination cohorts. The gap between a cohort's gross charge off and net losses reflects how effectively recoveries are being extracted from that group.

**Computation**

```
Months on Book (MOB) = Ceiling of Days between Issue Date and Loss Date / 30.5

Loss Ratio = Loss Amount / Total Original Balance for that Issue Date Cohort
```
