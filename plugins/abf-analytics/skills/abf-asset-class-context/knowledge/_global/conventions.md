---
title: ABF Data Conventions
tier: global
---

# ABF Data Conventions

Shared conventions used across all asset classes.

## Format types

| `format_type` | Semantics |
|---------------|-----------|
| `string` | Free text or enum value |
| `date` | ISO 8601 calendar date (YYYY-MM-DD) |
| `amount` | Monetary value; currency from transaction context |
| `percentage` | Decimal 0.0–1.0 unless the field notes state otherwise |
| `integer` | Count or whole-number measure |
| `boolean` | True or False |

## Cash flow type semantics

`cash_flows.Type` is an enum:

| Value | Meaning |
|-------|---------|
| `General Repayment` | Catch-all repayment not otherwise classified |
| `Principal Repayment` | Pure principal paydown |
| `Interest` | Interest payment |
| `Fee` | Service, late, or origination fee |
| `Prepayment` | Early full or partial principal repayment |
| `Recovery` | Cash received on a previously charged-off balance |

**Funding flows** (advance, draw-down) are excluded from periodic-collection KPIs. KPI computation strings that say "Scope: Exclude funding cashflow types" use this exclusion.

## Date and period semantics

- **Reporting Date** — All snapshot/static fields are "as of" this date.
- **Latest sync date** — Upper bound for cumulative cashflow KPIs. Prevents including future-dated rows.
- **Months on Book (MOB)** — `ceiling((event_date − issue_date) / 30.5)`. Used in vintage curve x-axes.
- **Cohort** — Grouped by `Issue Date` truncated to month or quarter, depending on pool size.

## Null / missing value conventions

- A field present in the entity but not populated for a record is `null`.
- KPI computations that check "if Previous X is null or zero, result = null" should be taken literally — return null rather than zero to avoid distorting rates.

## Delinquency buckets (consumer standard)

| Bucket label | DPD range |
|---|---|
| Current | 0 |
| 1–29 DPD | 1–29 |
| 30–59 DPD | 30–59 |
| 60–89 DPD | 60–89 |
| 90–119 DPD | 90–119 |
| 120–149 DPD | 120–149 |
| 150–180 DPD | 150–180 |
| 180+ DPD | > 180 |
