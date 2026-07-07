---
title: Cre — Data Center
tier: sub:cre/data-center
kpi_count: 4
inherits_from:
  - cre/common/kpis
---

# Cre — Data Center

> Inherits from: _global/kpis, cre/common/kpis. Override: child KPI with same `### name` wins.

## Other

### Critical Load Utilisation
_Category: Operational_

**Purpose**

Percentage of total installed critical IT power capacity (MW) currently contracted by tenants.

**Computation**

```
Critical Load Util = contracted_power_kw / (critical_load_mw × 1000) × 100.
```

### Delinquency Rate
_Category: Credit Risk_

**Purpose**

Proportion of lease payments past due as of the reporting date.

**Computation**

```
Delinquency Rate = Delinquent Balance / Total Contracted Rent × 100.
```

### Power Commitment Rate
_Category: Operational_

**Purpose**

Percentage of contracted power capacity actively deployed and consuming power.

**Computation**

```
Commitment Rate = committed_power_kw / contracted_power_kw × 100.
```

### Vacancy Loss
_Category: Operational_

**Purpose**

Revenue foregone due to uncommitted / unleased power capacity.

**Computation**

```
Vacancy Loss = (critical_load_mw × 1000 − contracted_power_kw) × Market Rate per kW.
```
