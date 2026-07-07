# Loss Vintage Analysis

Methodology for cumulative-default-by-cohort, defaults-by-segment, seasoning curves, and elbow detection.

## Applicability

Requires `catalog.profile.cf_determinism: YES`. The report-runner's Discover-phase profile-flag suppression should have already gated this; if the analysis fires anyway with `cf_determinism: NO`, surface to the analyst and stop:

> "Loss vintage curve analysis requires per-asset amortisation schedules (`cf_determinism: YES`). This asset class (`{asset_class}`) uses pool-level dynamics — cohort default curves don't apply. Consider delinquency flow or balance-at-risk analysis instead."

## Retrieve

- Cumulative defaults by cohort (cohort × term-on-book matrix).
- Defaults by segment (FICO, state, product).

## Analyze

1. **Elbow detection** — in the cumulative default curve per cohort, identify the term where the rate jumps materially (e.g., 0.58% → 2.87% at term 8). This is the seasoning elbow.
2. **Cohort comparison** — compare recent cohorts against older ones. Sharper or earlier elbows in recent vintages signal underwriting drift.
3. **Default concentration** — in the defaults-by-segment data, compute each segment's default share vs its portfolio share:
   `Default Share vs Portfolio Share = Segment Default % / Segment Portfolio %`
   - >1.0 → over-representation (segment is contributing more defaults than its size).
   - <1.0 → under-representation.
   Flag segments with ratio >1.0.

## Format

- Seasoning elbow narrative with 2-3 cohort × term data points.
- Default concentration narrative (top 2-3 segments, compact table acceptable if ≤5×5).

## Derived metrics reference

For precise formulas see `../../../abf-gateway/knowledge/reference/derived-metrics.md`.

## Example phrasing

- "The 2023-05 cohort shows a sharp elbow at term 8, jumping from 0.58% to 2.87%."
- "97.8% of defaults sit in sub-750 FICO, against a 63% portfolio share — a default-share ratio of 1.55."

## Default visual

If visuals are enabled (see `../../../abf-gateway/knowledge/reference/visuals-playbook.md`): **heatmap** — cohort (row) × term-on-book (column), values = cumulative default rate. Annotate the elbow cell explicitly.
