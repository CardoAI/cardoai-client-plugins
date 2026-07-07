---
title: Consumer — Entity Model
main: consumer
---

# Consumer — Entity model

## Standard entities

| Entity | Role | Notes |
|--------|------|-------|
| `investments` | Loan-level records — primary asset table | Source data may use `investmens` (typo); treat as synonymous |
| `borrower` | Individual obligor attributes | Absent for some subs where borrower data is pool-level only |
| `collateral` | Asset securing the loan | Populated for secured subs (Auto Loans, Home Improvement); absent for unsecured |
| `cash_flows` | Payment and recovery events | Key enum: `Type` ∈ General Repayment, Principal, Interest, Fee, Prepayment, Recovery |
| `calculated` | System-derived fields | MOB markers, cohort assignments; read-only |

## Join keys

Verified against the per-sub `data-model.md` field dictionary:

- `investments.Loan ID` ↔ `cash_flows.Loan ID`

### Conceptual relationships (not present as foreign keys in the field dictionary)

The data model does not expose a foreign-key column on `investments` for these
joins — the relevant ID column lives only on the other entity. The relationship
is real in the platform but cannot be expressed as a column-to-column join from
this catalog alone. **Verify the actual join path against the live transaction
schema before composing a query that crosses these entities.**

- `investments` ↔ `borrower` — `Borrower ID` exists on `borrower`; the link from
  `investments` is platform-internal (likely via `Loan ID` lookup).
- `investments` ↔ `collateral` *(Auto Loans only)* — `Vehicle ID` exists on
  `collateral`; the link from `investments` is platform-internal.

## Sub-classes

| Sub | Secured? | Collateral | CF Det. | Sim Fit | Key differentiator |
|-----|----------|------------|---------|---------|--------------------|
| Auto Loans | ✓ | Vehicle | YES | YES | LTV, vehicle category, odometer |
| Credit Cards | — | — | NO | PARTIAL | Revolving; MPR not CPR; master-trust pool dynamics |
| Unsecured Personal Loans | — | — | YES | YES | No collateral; recovery near zero |
| Point-of-Sale Loans | — | — | YES | YES | Merchant-funded; short tenor |
| Home Improvement | — | UCC / property lien | YES | YES | Contractor-originated; 5–20 yr |
| Device Payment Plan | — | — | YES | YES | Carrier-linked; cancellation = churn proxy |
| Student Loans | — | — | PARTIAL | PARTIAL | IDR / deferment paths; FFELP guarantee; income-driven CF |
| Buy Now Pay Later | — | — | YES | YES | Very short duration; Pay-in-4 has no interest; CPR less meaningful |

## Cross-sub conventions

- **FICO bands**: 300–579 / 580–669 / 670–739 / 740–799 / 800–850.
- **Loss curves** use Months on Book (MOB), not calendar months.
- **Delinquency** is tracked by DPD bucket (see `_global/conventions.md`).
- **Funding cashflow types** are excluded from collection KPIs.
