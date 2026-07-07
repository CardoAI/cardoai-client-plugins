---
title: Energy & Infrastructure — Entity Model
main: energy-infrastructure
---

# Energy & Infrastructure — Entity model

## Standard entities (Cell Tower)

| Entity | Role | Notes |
|--------|------|-------|
| `Liability` | Debt / loan record | Same structure as CRE Liability |
| `Property` | Tower site / physical asset | Location, ground-lease status, structural capacity |
| `Lease` | Tenant lease records | Anchor tenant + colocation amendments; escalators |

## Key characteristics

E&I is closest to CRE in structure (Liability / Property / Lease), not to
Consumer or Commercial. There is no `borrower` or `investments` loan-tape entity.

Cash flows are contract-driven: long-term tower leases with known escalators
make this asset class **CF Deterministic** (unlike CRE Office / Hospitality).

Standard CPR / CDR analytics do **not apply**. Focus on:
- Tenant rollover risk at lease expiry
- Colocation amendment economics (incremental tenants)
- Ground-lease cost vs tower revenue margin
- DSCR and debt yield (same KPIs as CRE common)

## Sub-classes

| Sub | CF Det. | Sim Fit | Key differentiator |
|-----|---------|---------|-------------------|
| Cell Tower | YES | YES | Long-term carrier leases with built-in escalators; hyperscaler demand tailwind |

## Cross-sub conventions

- **Lease escalators** are typically CPI-linked or fixed %; model them explicitly.
- **Colocation amendments** increase revenue per tower without increasing site cost.
- **Churn risk** = anchor tenant non-renewal; devastating because tower cash flow
  is anchor-tenant-dependent.
