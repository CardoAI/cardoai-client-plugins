# Concentration Risk Analysis

Methodology for geographic, FICO, obligor, and sector concentration. Branches by asset class.

## Asset-class routing

Read `catalog.asset_class.main` from `{asset_class_catalog}`:

**Consumer / lending** (`main = "consumer"`)
→ FICO-banded analysis applies. Proceed with the full Analyze steps below.

**Commercial, CRE, or Energy & Infrastructure** (`main ≠ "consumer"`)
→ FICO is not relevant. Pivot to obligor and sector concentration only:
  1. **Obligor concentration** — flag any single obligor with >5% of portfolio balance. Flag top-3 obligor concentration >15%.
  2. **Sector / industry concentration** — flag any single sector >20% of portfolio balance.
  Skip the FICO distribution analysis entirely. Do not reference FICO bands in the output.

**No catalog loaded** → proceed with the consumer analysis; note that FICO banding assumes a consumer asset class.

## Retrieve

- Balance by state.
- FICO distribution (count and/or balance).

## Analyze

1. **Geographic concentration** — flag any single state with >10% of portfolio balance. Flag top-3 state concentration >30%.
2. **FICO distribution** — identify the dominant FICO band (largest share) and classify:
   - Prime: >740
   - Near-prime: 670-740
   - Sub-prime: <670

   Flag if >50% of portfolio sits in sub-prime.

## Format

- Top 3-5 states narrative with exact percentages.
- FICO dominant band narrative with exact percentage and classification.
- Call out any flagged thresholds explicitly ("single-state concentration exceeds the 10% threshold").

## Example phrasing

- "Top 3 states account for 47% of balance — CA 22.3%, TX 14.1%, FL 10.6%. CA alone breaches the 10% single-state concentration threshold."
- "The 651-700 FICO bucket holds 63% of the portfolio, placing the concentration firmly in near-prime."

## Default visual

If visuals are enabled (see `../../../abf-gateway/knowledge/reference/visuals-playbook.md`):
- **Horizontal bar chart** — top 10 states by balance share, with 10% threshold line.
- **Donut chart** — FICO distribution (prime / near-prime / sub-prime bands) — consumer asset classes only.
