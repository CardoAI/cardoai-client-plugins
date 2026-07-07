---
title: Commercial — Entity Model
main: commercial
---

# Commercial — Entity model

## Standard entities

| Entity | Role | Notes |
|--------|------|-------|
| `investments` | Asset / facility records — primary table | Loans, invoices, facilities depending on sub |
| `companies` | Corporate obligor / counterparty | Replaces `borrower` from consumer; company-level attributes |
| `calculated` | System-derived fields | MOB, duration, derived ratios |
| `cash_flows` | Payment and settlement events | Key enum: `Type` ∈ General Repayment, Principal, Interest, Fee, Prepayment, Recovery |

## Key difference from Consumer

Most commercial subs treat obligors as corporates via `companies`. **Exception:**
some subs (notably Corporate Loans) also carry a `borrower` entity with
personal-credit fields (FICO, DTI, employment status) for the underlying obligor
— consult the per-sub `data-model.md` to confirm which entities are present.
For pure-corporate subs (Trade Finance, Inventory Finance, etc.), use
`companies.Revenue`, `companies.Sector`, or `companies.Rating` rather than
borrower fields.

## Join keys

Per-sub `data-model.md` is the authority — primary-key columns and the matching
column on `cash_flows` are **not uniform across subs**. The primary key on
`investments` varies by sub (`Loan ID` for loan-shaped subs; `Trade ID` for
Trade Finance; etc.), and the join column on `cash_flows` may be the same key,
a different identifier, or `Payment Date` against `investments.Payment Date`.
**Always read the per-sub `data-model.md` §Join keys section before composing a
cross-entity query** — do not assume the investments primary key is repeated on
`cash_flows`.

### Conceptual relationships (not present as foreign keys in the field dictionary)

`Company ID` exists on the `companies` entity but is **not exposed as a column on
`investments`** in the field dictionary. The investments-to-companies link is
platform-internal. **Verify the actual join path against the live transaction
schema before composing a cross-entity query.**

- `investments` ↔ `companies` — corporate obligor lookup; column on `investments`
  side is platform-internal.

## Sub-classes

| Sub | CF Det. | Sim Fit | Tenure type | Key dynamic |
|-----|---------|---------|-------------|-------------|
| Corporate Loans | PARTIAL | YES | Term + revolver | Floating rate; balloon maturity |
| Trade Finance | PARTIAL | PARTIAL | Short-term (30–180d) | Self-liquidating; DSO primary metric |
| Inventory Finance | NO | PARTIAL | Revolving / borrowing-base | No fixed amortisation; eligible-asset driven |
| Leasing Finance | PARTIAL | PARTIAL | Periodic + RV | Residual value risk at term |
| Rail Cars & Containers | PARTIAL | PARTIAL | Operating lease | Utilisation rate; re-lease risk |
| Small Business Loans | YES | YES | Amortising | SBA guarantee split (guaranteed vs unguaranteed) |
| Equipment Finance | YES | YES | Amortising / lease | Asset-class-specific severity curves |
| Revenue Based Finance | NO | PARTIAL | Revenue-paced | No fixed schedule; repayment tied to revenue |
| Ecommerce Finance | NO | PARTIAL | Sales-paced | Same as RBF; sales-velocity model |

## Cross-sub conventions

- **Delinquency** measured at facility level, not borrower level.
- **Collections** tracked per invoice / payment date for Trade Finance.
- **Vintage analysis** uses facility origination date as cohort anchor.
