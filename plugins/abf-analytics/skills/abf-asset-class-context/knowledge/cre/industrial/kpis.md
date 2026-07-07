---
title: Cre — Industrial
tier: sub:cre/industrial
kpi_count: 3
inherits_from:
  - cre/common/kpis
---

# Cre — Industrial

> Inherits from: _global/kpis, cre/common/kpis. Override: child KPI with same `### name` wins.

## Other

### Delinquency Rate
_Category: Credit Risk_

**Purpose**

Proportion of rent or debt payments past due as of the reporting date.

**Computation**

```
Delinquency Rate = Delinquent Balance / Total Balance × 100. Computed from dpd and arrears_amount on Rent/Lease entity.
```

### Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of rentable units or area currently occupied/leased as of the reporting date.

**Computation**

```
Occupancy Rate = Occupied Units (or Area) / Total Units (or Area) × 100.
```

### Vacancy Loss
_Category: Operational_

**Purpose**

Income foregone due to unoccupied or unleased units and space.

**Computation**

```
Vacancy Loss = Vacant Units (or Area) / Total × Market Rent. Expressed as amount or % of gross potential rent.
```
