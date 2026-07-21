# Performance Agent

**Focus:** Returns, value drivers, operating metrics | **Wave:** 1 | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| PERF-01 | NAV ($m) | Point-in-time | T vs T-1Y |
| PERF-02 | NAV per share ($) | Point-in-time | T vs T-1Y |
| PERF-03 | NAV Total Return (%) | Flow | T vs T-1Y |
| PERF-04 | Private company appreciation (% ex-FX) | Flow | T vs T-1Y |
| PERF-05 | Quoted holdings change (% ex-FX) | Flow | T vs T-1Y |
| PERF-06 | LTM Revenue Growth (%) | Point-in-time | T vs T-1Y |
| PERF-07 | LTM EBITDA Growth (%) | Point-in-time | T vs T-1Y |
| PERF-08 | Top 5 positive contributors ($m) | Flow | T vs T-1Y |
| PERF-09 | Top 5 negative contributors ($m) | Flow | T vs T-1Y |
| PERF-10 | EV/EBITDA multiple (x) | Point-in-time | T vs T-1Y |
| PERF-11 | Top 10 companies % of portfolio | Point-in-time | T vs T-1Y |

## Sub-Agent Strategies
**Sub-A (Targeted):** Search for NAV, total return, per-share metrics. Query: "NAV total return per share net asset value". Use KPI filters where possible. Search both T and T-1Y.

**Sub-B (Value Drivers):** Search for top/bottom contributors, value change waterfall, performance drivers. Query: "key performance drivers value change positive negative contributors top 5 top 10". Search T period.

**Sub-C (Operating Metrics):** Search for revenue growth, EBITDA growth, valuation multiples. Query: "LTM revenue EBITDA growth weighted average EV/EBITDA multiple". Search both T and T-1Y.

## Cross-Validation Rules
- NAV must reconcile: NAV per share x shares outstanding ~ NAV total
- NAV TR should be consistent with (ending NAV + dividends) / beginning NAV - 1
- Top positive + top negative + other = total value change (approximately)
- If operating growth is positive but NAV declined, flag for Risk agent (likely multiple contraction or FX)

## Red Flag Triggers
- NAV TR < 0%
- EBITDA growth < revenue growth (margin compression)
- EV/EBITDA multiple changed > 1.0x
- Top 5 negative > 50% of top 5 positive
