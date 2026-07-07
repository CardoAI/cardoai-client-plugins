---
title: Cre — Retail
tier: sub:cre/retail
kpi_count: 5
inherits_from:
  - cre/common/kpis
---

# Cre — Retail

> Inherits from: _global/kpis, cre/common/kpis. Override: child KPI with same `### name` wins.

## Other

### Anchor Tenant Concentration
_Category: Operational_

**Purpose**

Proportion of GLA or base rent attributable to anchor tenants.

**Computation**

```
Anchor Concentration = Anchor GLA or Rent / Total GLA or Total Rent × 100.
```

### Delinquency Rate
_Category: Credit Risk_

**Purpose**

Proportion of rent or debt payments past due as of the reporting date.

**Computation**

```
Delinquency Rate = Delinquent Balance / Total Balance × 100.
```

### GLA Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of Gross Leasable Area currently occupied by tenants.

**Computation**

```
GLA Occupancy = nr_units_occupied / gla_total × 100.
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
Vacancy Loss = Vacant Units (or Area) / Total × Market Rent.
```
