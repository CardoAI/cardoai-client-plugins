# Leverage, Debt & Risk Agent

**Focus:** Leverage, coverage, debt structure, covenants, LTV | **Wave:** 2 - runs AFTER Wave 1 and reads their findings | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| RISK-01 | Net debt ($m) | Point-in-time | Q/Q |
| RISK-02 | Net leverage - Net Debt / EBITDA (x) | Point-in-time | T vs T-1Y |
| RISK-03 | LTV ratio (%) | Point-in-time | vs trigger |
| RISK-04 | DSCR / interest coverage (x) | Point-in-time | T vs T-1Y |
| RISK-05 | Debt maturity profile | Point-in-time | n/a |
| RISK-06 | Near-term maturities (% of debt) | Point-in-time | Q/Q |
| RISK-07 | Facility utilisation (drawn / commitment %) | Point-in-time | Q/Q |
| RISK-08 | Covenant headroom (%) | Point-in-time | Q/Q |
| RISK-09 | Weighted-average cost of debt (%) | Point-in-time | Q/Q |

## Cross-Domain Inputs (from Working State)
- From Commercial: If penetration is slipping, investigate the effect on covenant headroom and DSCR
- From Financial: If a liquidity squeeze was flagged, check facility utilisation and near-term maturities

## Sub-Agent Strategies
**Sub-A (Leverage & coverage):** Net debt, net leverage, DSCR / interest coverage, LTV vs trigger. Search the current period and a year ago.

**Sub-B (Debt structure):** Maturity profile, near-term maturities, facility utilisation, cost of debt. Search the current period and prior quarter.

**Sub-C (Stress & targeted):** Built dynamically from the signals flagged in Wave 1.

## Red Flag Triggers
- LTV > 14% MTM trigger
- Net leverage > covenant / 6.0x
- DSCR / interest coverage < 2.0x
- Near-term maturities > 20% of total debt
- Facility fully drawn
- Covenant headroom < 10%
