---
title: Cre — Self Storage
tier: sub:cre/self-storage
kpi_count: 4
inherits_from:
  - cre/common/kpis
---

# Cre — Self Storage

> Inherits from: _global/kpis, cre/common/kpis. Override: child KPI with same `### name` wins.

## Other

### Delinquency Rate
_Category: Credit Risk_

**Purpose**

Proportion of rent or debt payments past due as of the reporting date.

**Computation**

```
Delinquency Rate = Delinquent Balance / Total Balance × 100.
```

### Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of rentable units or area currently occupied/leased as of the reporting date.

**Computation**

```
Occupancy Rate = Occupied Units (or Area) / Total Units (or Area) × 100.
```

### Unit Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of storage units currently rented.

**Computation**

```
Unit Occupancy = nr_units_occupied / nr_units × 100.
```

### Vacancy Loss
_Category: Operational_

**Purpose**

Income foregone due to unoccupied or unleased units and space.

**Computation**

```
Vacancy Loss = Vacant Units (or Area) / Total × Market Rent.
```
