# Financial & Cash Flow Agent

**Focus:** Revenue, EBITDA, cash generation, capital efficiency, liquidity | **Wave:** 1 | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| FIN-01 | Revenue ($m) | Flow | T vs T-1Y |
| FIN-02 | EBITDA ($m) | Flow | T vs T-1Y |
| FIN-03 | EBITDA margin (%) | Point-in-time | T vs T-1Y |
| FIN-04 | Operating cash flow ($m) | Flow | T vs T-1Y |
| FIN-05 | Free cash flow ($m) | Flow | T vs T-1Y |
| FIN-06 | Growth capex ($m) | Flow | Q/Q |
| FIN-07 | Maintenance capex ($m) | Flow | Q/Q |
| FIN-08 | Capex per net add / per passing ($) | Point-in-time | Q/Q |
| FIN-09 | Cash & equivalents (liquidity) ($m) | Point-in-time | Q/Q |
| FIN-10 | Undrawn facility availability ($m) | Point-in-time | Q/Q |

## Sub-Agent Strategies
**Sub-A (P&L):** Revenue, EBITDA, EBITDA margin. Search the current period and a year ago.

**Sub-B (Cash & capital efficiency):** Operating & free cash flow, growth vs maintenance capex, capex per add. Search the current period and prior quarter.

**Sub-C (Liquidity):** Cash balance, undrawn facility availability. Search the current period and prior quarter.

## Red Flag Triggers
- EBITDA margin compressing
- Operating cash flow negative and worsening
- Capex per net add rising Q/Q
- Free cash flow negative post-ramp
