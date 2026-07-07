---
title: Energy-Infrastructure — Cell Tower
tier: sub:energy-infrastructure/cell-tower
kpi_count: 9
inherits_from:
  - energy-infrastructure/common/kpis
---

# Energy-Infrastructure — Cell Tower

> Inherits from: _global/kpis, energy-infrastructure/common/kpis. Override: child KPI with same `### name` wins.

## Other

### Current NOI
_Category: Performance_

**Purpose**

Annualised net operating income across the tower portfolio after operating expenses, before debt service and CapEx.

**Computation**

```
Current NOI = Sum of Noi Site across all active Property records.
```

### DSCR – Debt Service Coverage Ratio
_Category: Credit Risk_

**Purpose**

Portfolio's ability to cover total debt service from net operating income.

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

### Delinquency Rate
_Category: Credit Risk_

**Purpose**

Proportion of lease payments past due as of the reporting date.

**Computation**

```
Delinquency Rate = Σ Arrears Amount / Σ Annual Lease Payment × 100. Computed from Dpd and Arrears Amount on Lease entity.
```

### ICR – Interest Coverage Ratio
_Category: Credit Risk_

**Purpose**

Portfolio's ability to cover interest expense alone from net operating income.

**Computation**

```
ICR = Current NOI / Annual Interest Expense.
```

### LTV – Loan-to-Value
_Category: Credit Risk_

**Purpose**

Ratio of total outstanding debt to current appraised portfolio value.

**Computation**

```
LTV = Total Outstanding Debt / Appraised Value.
```

### Lease Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of tower sites with at least one active paying tenant as of the reporting date.

**Computation**

```
Occupancy Rate = Sites with Active Tenants Per Tower ≥ 1 / Total Sites × 100.
```

### Tenancy Ratio
_Category: Operational_

**Purpose**

Average number of active paying tenants per tower across the portfolio. Core cell tower revenue efficiency metric.

**Computation**

```
Tenancy Ratio = Total Active Leases / Total Tower Sites
```

### Weighted Average Remaining Lease Term (WALT)
_Category: Operational_

**Purpose**

Revenue-weighted average remaining lease term across all active leases. Measures duration of contracted cash flow.

**Computation**

```
WALT = Σ (Annual Lease Payment × Remaining Lease Term) / Σ Annual Lease Payment.
```
