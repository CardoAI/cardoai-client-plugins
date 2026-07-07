---
title: Cre — Common KPIs
tier: main:cre
kpi_count: 7
inherits_from:
---

# Cre — Common KPIs

> Inherits from: _global/kpis. Override: child KPI with same `### name` wins.

## Other

### Current LTV (Mark-to-Market)
_Category: Credit Risk_

**Purpose**

Updated LTV using current appraised value versus current outstanding debt.

**Computation**

```
Current LTV = Total Outstanding Debt / Current Valuation Amount.
```

### Current NOI
_Category: Performance_

**Purpose**

Annualised net operating income after operating expenses, before debt service, CapEx, depreciation, and amortisation.

**Computation**

```
Current NOI = Annualised Revenue − Annualised OpEx.
```

### DSCR – Debt Service Coverage Ratio
_Category: Credit Risk_

**Purpose**

Property's ability to cover total debt service from net operating income.

**Computation**

```
DSCR = Current NOI / Annual Debt Service.
```

### Debt Yield
_Category: Credit Risk_

**Purpose**

Net operating income as a percentage of total outstanding loan balance. Rate-independent credit metric.

**Computation**

```
Debt Yield = Current NOI / Outstanding Loan Balance × 100.
```

### ICR – Interest Coverage Ratio
_Category: Credit Risk_

**Purpose**

Property's ability to cover interest expense alone from net operating income.

**Computation**

```
ICR = Current NOI / Annual Interest Expense.
```

### LTV – Loan-to-Value
_Category: Credit Risk_

**Purpose**

Ratio of total outstanding debt to current appraised property value.

**Computation**

```
LTV = Total Outstanding Debt / Appraised Value.
```

### Stabilized NOI
_Category: Performance_

**Purpose**

Projected annualised NOI at full lease stabilisation, assuming market rents and normal vacancy.

**Computation**

```
Used to underwrite exit value and measure lease-up progress vs current_noi.
```
