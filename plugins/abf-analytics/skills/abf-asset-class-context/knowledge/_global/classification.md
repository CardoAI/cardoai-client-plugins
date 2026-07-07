---
title: Asset-Class Classification — Resolution Algorithm
tier: global
---

# Asset-Class Classification

How to map a transaction's `asset_class` string (from `list_transactions`) to
the correct `{main, sub}` knowledge files.

## Resolution order

Work through steps 1–4 in order. Stop at the first match.

### Step 1 — Exact match

Normalise the platform string:

1. Strip leading/trailing whitespace and collapse internal whitespace.
2. **Enum-name normalisation (defensive).** If the string is entirely `UPPER_SNAKE_CASE`
   (all-caps with underscores, no spaces), convert it to title-case label form
   before lookup: replace underscores with spaces and title-case each word
   (e.g. `AUTO_LOANS` → `Auto Loans`, `CRE_HOSPITALITY` → `Cre Hospitality`).
   Then try the verbatim lookup. If the title-case conversion still doesn't hit
   a map key exactly, continue to Step 2 — the synonym and fuzzy steps will
   catch it. *Note: the platform's actual production format for `asset_class` has
   not been confirmed; this step is a defensive fallback in case the backend
   emits enum names rather than display labels.*

Look up the normalised string in `lib/asset-class-map.json` → `mappings`. Map
keys use mixed case ("Auto Loans", "CRE Hospitality", "Buy Now Pay Later") to
match the platform-emitted `asset_class` string. If a verbatim lookup fails,
fall through to Step 2; do not lowercase the input and retry on the keys.

### Step 2 — Synonym match

Check the platform string against each entry's `synonyms` list in
`asset-class-map.json` (case-insensitive).

One synonym match → resolved to that entry.

Multiple synonym matches → surface candidates to analyst:
> "The transaction's asset class `{S}` matches multiple catalog entries:
> {list}. Which one applies?"

### Step 3 — Fuzzy match

Apply token-set similarity (Levenshtein ≤ 2, or token-set ratio ≥ 0.85)
against the map keys and synonyms.

One strong candidate → resolved with a disclosure:
> "I matched `{S}` to `{display_name}` (best fit). Let me know if a
> different asset class applies."

Multiple candidates or confidence < threshold → surface to analyst.

### Step 4 — Entity-shape heuristic (last resort)

If steps 1–3 all fail: inspect the transaction's available analytics or
filterable columns and compare the entity vocabulary against the per-main
`_index.md` entity manifests.

| Evidence | Likely `main` |
|----------|---------------|
| Entities include `Liability`, `Property`, `Rent` | `cre` |
| Entities include `Liability`, `Property`, `Lease` | `energy-infrastructure` |
| Entities include `investments`, `companies` | `commercial` |
| Entities include `investments`, `borrower`, `collateral` | `consumer` |

Use this as a confidence hint only — never as the sole classifier.

### Step 5 — Unresolved fallback

If all steps fail, load `_global/` files only and disclose:
> "Backend reports asset class `{S}` — not in my catalog. I'll apply
> generic ABF analysis. If you know the asset class (Auto Loans,
> Hospitality, …), tell me and I'll load the right knowledge."

## When to re-run resolution

- A new transaction is loaded (different `transaction_id`).
- Analyst explicitly names a different asset class mid-session.
- Backend returns a different `asset_class` value for the same transaction.

Do NOT re-run resolution for repeated queries on the same active transaction.

## Cache key

`(transaction_id, sub_slug)` — or `sub_slug` alone when no transaction is
active (analyst named the class directly).
