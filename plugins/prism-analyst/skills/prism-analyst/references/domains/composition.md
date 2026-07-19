# Composition Agent

**Focus:** Portfolio construction, holdings, sector/geography/vintage allocation | **Wave:** 1 | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| COMP-01 | Total portfolio value ($m) | Point-in-time | T vs T-1Y |
| COMP-02 | Number of holdings | Point-in-time | T vs T-1Y |
| COMP-03 | Top 10 holdings (names + values) | Point-in-time | T vs T-1Y |
| COMP-04 | Sector allocation (%) | Point-in-time | T vs T-1Y |
| COMP-05 | Geography allocation (%) | Point-in-time | T vs T-1Y |
| COMP-06 | Vintage year distribution (%) | Point-in-time | T vs T-1Y |
| COMP-07 | % in private vs public | Point-in-time | T vs T-1Y |
| COMP-08 | Average holding period (years) | Point-in-time | T vs T-1Y |
| COMP-09 | Top 30 concentration (% of FV) | Point-in-time | T vs T-1Y |
| COMP-10 | New entries since T-1Y | n/a | Diff |
| COMP-11 | Exits since T-1Y | n/a | Diff |

## Sub-Agent Strategies
**Sub-A (Top Holdings):** Search for Schedule of Investments, top 10/20/30 tables. Query: "schedule investments top companies holdings fair value". Search T and T-1Y.

**Sub-B (Allocation):** Search for sector, geography, vintage breakdowns. Query: "sector allocation geography vintage distribution portfolio diversification". Search T and T-1Y.

**Sub-C (Changes):** Search for new investments, exits, portfolio changes. Query: "new investments exits realisations portfolio changes during year". Search T.

## Cross-Validation Rules
- Sum of sector allocations should = ~100%
- Top holdings values should sum to < total portfolio value
- Holdings count should reconcile with exits/entries

## Red Flag Triggers
- Single holding > 10% of NAV (concentration)
- Top 5 holdings > 30% of NAV
- Any sector > 25% (concentration)
- Average holding period > 6 years
