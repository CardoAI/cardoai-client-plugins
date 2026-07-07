---
title: Cre — Hospitality
tier: sub:cre/hospitality
kpi_count: 6
inherits_from:
  - cre/common/kpis
---

# Cre — Hospitality

> Inherits from: _global/kpis, cre/common/kpis. Override: child KPI with same `### name` wins.

## Other

### ADR – Average Daily Rate
_Category: Operational_

**Purpose**

Average revenue earned per occupied room per day.

**Computation**

```
ADR = Total Room Revenue / Rooms Sold (nr_rooms_sold).
```

### Delinquency Rate
_Category: Credit Risk_

**Purpose**

Proportion of rent or debt payments past due as of the reporting date.

**Computation**

```
Delinquency Rate = Delinquent Balance / Total Balance × 100..
```

### Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of rentable units or area currently occupied/leased as of the reporting date.

**Computation**

```
Occupancy Rate = Occupied Units (or Area) / Total Units (or Area) × 100.
```

### RevPAR – Revenue Per Available Room
_Category: Operational_

**Purpose**

Revenue per available room: combines occupancy and ADR.

**Computation**

```
RevPAR = Total Room Revenue / Total Available Rooms = ADR × Occupancy.
```

### Rooms Occupancy Rate
_Category: Operational_

**Purpose**

Percentage of available hotel rooms occupied.

**Computation**

```
Room Occupancy = nr_rooms_sold / nr_rooms × 100.
```

### Vacancy Loss
_Category: Operational_

**Purpose**

Income foregone due to unoccupied or unleased units and space.

**Computation**

```
Vacancy Loss = Vacant Units (or Area) / Total × Market Rent.
```
