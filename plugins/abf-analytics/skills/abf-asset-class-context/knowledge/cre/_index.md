---
title: CRE — Entity Model
main: cre
---

# CRE — Entity model

## Standard entities

| Entity | Role | Notes |
|--------|------|-------|
| `Liability` | Debt tranche / loan record | One row per loan; carries rate, maturity, outstanding balance |
| `Property` | Real estate asset securing the debt | Valuation, location, status, condition |
| `Rent` | Tenant lease records | Occupancy, contracted rent, lease expiry *(Office, Industrial, Retail, Residential, Self-Storage)* |

## CRE Addendum entities (always load for CRE)

| Entity | Role |
|--------|------|
| `Project` | Construction / development project lifecycle |
| `Milestone` | Project milestone events |
| `Realized Cash Flow` | Actual cash disbursed / received against the project |
| `Expected Cash Flow` | Forecast cash schedule for the project |

## Key difference from Consumer / Commercial

CRE has **no `borrower`** and **no `investments` (loan tape)** entity. The loan
is a `Liability` against one or more `Property` records. Cash flow analysis is
at the property-income level (rent, NOI, occupancy), not at the loan-amortisation
level. Standard CPR / CDR / vintage loss analytics **do not apply** — use DSCR,
LTV, NOI, Occupancy, and RevPAR instead.

## Join keys

Verified against per-sub `data-model.md` field dictionaries. **Source data uses
`Property Id` (lowercase `d`)** — preserve that casing in queries.

- `Liability.Property Id` ↔ `Property.Property Id`
- `Property.Property Id` ↔ `Rent.Property Id`  *(Office, Industrial, Retail,
  Residential, Self-Storage)*
- `Property.Property Id` ↔ `Project.Property Id` *(CRE Addendum — when project
  data present)*

## Sub-classes

| Sub | CF Det. | Sim Fit | Cash flow driver | Key KPIs |
|-----|---------|---------|-----------------|----------|
| Condominium | NO | NO | Unit sales (sell-out) | Sell-out rate, absorption; no recurring NOI during development |
| Hospitality | PARTIAL | PARTIAL | Room revenue (RevPAR) | ADR, Occupancy Rate, RevPAR, Rooms Sold |
| Industrial | PARTIAL | PARTIAL | Long-term tenant leases | Occupancy, WALE, rent per sqm |
| Office | PARTIAL | PARTIAL | Tenant leases (rollover risk) | Occupancy, DSCR, WALE; post-COVID vacancy headwinds |
| Residential | PARTIAL | PARTIAL | Rental income | Occupancy, in-place rent vs market, NOI margin |
| Retail | PARTIAL | PARTIAL | Base rent + % rent | Tenant sales, anchor footfall, vacancy loss |
| Self-Storage | PARTIAL | PARTIAL | Short-term monthly storage | Occupancy, rate per unit, high turnover |
| Data Center | YES | YES | Long-term hyperscaler leases | Power capacity, lease-up, contracted WALE |

## Cross-sub conventions

- **DSCR**, **LTV**, **ICR**, **Debt Yield** are universal CRE credit metrics
  (see `cre/common/kpis.md`).
- **NOI** is the primary performance indicator; always annualise before computing ratios.
- **Stabilised NOI** is the underwriting anchor; **Current NOI** tracks progress.
