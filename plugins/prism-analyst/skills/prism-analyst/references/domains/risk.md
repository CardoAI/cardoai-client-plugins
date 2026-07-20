# Risk Agent

**Focus:** Leverage, FX, debt, covenants, stress factors | **Wave:** 2 - runs AFTER Wave 1 and reads their findings | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| RISK-01 | Net Debt/EBITDA (x) | Point-in-time | T vs T-1Y |
| RISK-02 | Interest coverage ratio (x) | Point-in-time | T vs T-1Y |
| RISK-03 | % cov-lite debt | Point-in-time | T vs T-1Y |
| RISK-04 | FX impact ($m) | Flow | T vs T-1Y |
| RISK-05 | Debt maturity profile | Point-in-time | n/a |
| RISK-06 | Near-term maturities ($m or %) | Point-in-time | T vs T-1Y |
| RISK-07 | Share price discount to NAV (%) | Point-in-time | T vs T-1Y |
| RISK-08 | Unrealised losses ($m) | Flow | T vs T-1Y |
| RISK-09 | Credit facility utilisation | Point-in-time | T vs T-1Y |
| RISK-10 | LTV ratio | Point-in-time | T vs T-1Y |

## Cross-Domain Inputs (from Working State)
- From Performance: If NAV declined, investigate leverage and FX as causes
- From Performance: If EBITDA grew but NAV flat, investigate multiple contraction
- From Cash Flow: If realisations < distributions, check credit facility draw
- From Composition: If concentration increased, flag single-name risk

## Sub-Agent Strategies
**Sub-A (Leverage & Debt):** Search for leverage, debt, covenants, maturity. Query: "net debt EBITDA leverage covenant debt maturity interest coverage". Search T and T-1Y.

**Sub-B (FX & Market):** Search for FX impact, currency exposure, public holdings. Query: "foreign exchange FX impact currency USD EUR GBP quoted public holdings discount NAV". Search T and T-1Y.

**Sub-C (Stress & Targeted):** Based on Wave 1 findings - search for specific risks flagged by other agents. Dynamically constructed query.

## Red Flag Triggers
- Leverage > 6.0x
- Interest coverage < 2.0x
- Near-term maturities > 20% of total debt
- FX impact > 5% of NAV
- Discount to NAV > 30%
- Unrealised losses > unrealised gains
