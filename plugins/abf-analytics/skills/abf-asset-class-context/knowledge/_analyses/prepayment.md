# Prepayment Vintage Analysis

Methodology for prepayment-by-cohort and prepayment-by-segment, SMM/CPR derivations, adverse selection, and composition drift projection.

## Applicability

Requires `catalog.profile.loan_sim_fit: YES` or `PARTIAL`. The report-runner's Discover-phase profile-flag suppression should have already gated this; if the analysis fires with `loan_sim_fit: NO`, surface and stop:

> "CPR/SMM prepayment modelling is not applicable for `{asset_class}` — the asset class does not follow a standard loan simulation model. If a bespoke prepayment proxy exists (e.g., Monthly Payment Rate for revolving pools), it will be named in the catalog's risk_metrics."

If `PARTIAL`: proceed, but note the caveat from `catalog.profile` in the output before presenting numbers.

## Retrieve

- Prepayment by cohort.
- Prepayment by segment (especially FICO).

## Analyze

1. **Cohort consistency** — do recent cohorts prepay at similar rates to older ones? Divergence suggests rate-environment shift or seasoning differences.
2. **Adverse selection** — cross-reference prepayment speeds by FICO. Higher-FICO buckets prepaying faster = adverse selection risk; the remaining pool degrades as the best credits leave.
3. **Derived speeds** — compute SMM and CPR per segment (formulas in `../../../abf-gateway/knowledge/reference/derived-metrics.md`):
   - Monthly SMM = 1 - (1 - CumPrepay)^(1/Term)
   - Annualized CPR = 1 - (1 - SMM)^12
4. **Composition drift projection** — given differential prepayment speeds, project each FICO bucket's share at t+3, t+6, t+9, t+12 months. Drift measured in basis points.

## Format

- Cohort consistency / divergence narrative.
- Adverse-selection narrative quantified with specific numbers.
- Derived-metrics table: FICO bucket | Cumulative Prepay | SMM | CPR.
- Composition-drift table: FICO bucket | Share_t | Share_{t+3} | Share_{t+6} | Share_{t+12} | Δ (bps).

## Example phrasing

- "The 651-700 bucket — already 63% of the portfolio — has the lowest prepayment speed (0.59% monthly SMM, 5.72% cumulative by T10). Every other bucket exits faster, so the 651-700 share mechanically grows by ~99 bps over 12 months."
- "The 801-850 bucket is evaporating: 26.3% cumulative prepayment by T3, 9.67% monthly SMM (70.5% annualized CPR)."

## Labeling

Projections must be labeled as such. Use "projected based on current rates" with explicit assumptions. Never present projections as observed data.

## Default visual

If visuals are enabled (see `../../../abf-gateway/knowledge/reference/visuals-playbook.md`):
- **Grouped bar chart** — FICO bucket × (SMM, CPR) side-by-side.
- **Stacked area chart** — projected composition drift across buckets at t+3 / t+6 / t+9 / t+12 months.
