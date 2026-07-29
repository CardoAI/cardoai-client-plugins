# Network & Coverage Agent

**Focus:** Passings, network density, build-cost efficiency | **Wave:** 1 | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| NET-01 | Total premises passed (passings) | Point-in-time | Q/Q |
| NET-02 | Passings added in period | Flow | Q/Q |
| NET-03 | Passings growth rate (%) | Flow | T vs T-1Y |
| NET-04 | Cumulative passings vs prior year | Point-in-time | T vs T-1Y |
| NET-05 | Serviceable passings (ready-for-service) | Point-in-time | Q/Q |
| NET-06 | Passings by market / region | Point-in-time | n/a |
| NET-07 | Network route / fiber miles | Point-in-time | Q/Q |
| NET-08 | Construction cost per foot ($) | Point-in-time | Q/Q |
| NET-09 | MDU units / beds under contract | Point-in-time | Q/Q |

## Sub-Agent Strategies
**Sub-A (Passings):** Total & added passings, growth rate, cumulative vs prior year, serviceable count. Search the current period and the prior quarter / prior year.

**Sub-B (Reach & cost):** Passings by market, route / fiber miles, cost per foot. Search the current period and prior quarter.

**Sub-C (Under-contract base):** MDU units & beds under contract, properties & sites served. Search the current period and prior quarter.

## Red Flag Triggers
- Passings added below prior-quarter run-rate
- Passings growth rate decelerating YoY
- Serviceable passings lagging total passings (activation gap)
- Cost per foot rising Q/Q
