# Commercial & Subscribers Agent

**Focus:** How passings convert to paying customers - penetration, ARPU, churn | **Wave:** 1 | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| OPS-01 | End-of-period subscribers | Point-in-time | Q/Q |
| OPS-02 | Net new subscribers | Flow | Q/Q |
| OPS-03 | Gross adds / installs | Flow | Q/Q |
| OPS-04 | Subscriber growth rate (%) | Flow | T vs T-1Y |
| OPS-05 | Penetration (subscribers / passings %) | Point-in-time | Q/Q |
| OPS-06 | Penetration by cohort / vintage (%) | Point-in-time | vs target |
| OPS-07 | Take-up vs mature-penetration target (%) | Point-in-time | vs target |
| OPS-08 | Churn rate (%) | Flow | Q/Q |
| OPS-09 | ARPU ($ / month) | Point-in-time | T vs T-1Y |
| OPS-10 | Recurring / contracted revenue ($m) | Flow | T vs T-1Y |
| OPS-11 | MDU premises under service | Point-in-time | Q/Q |

## Sub-Agent Strategies
**Sub-A (Subscriber base):** EoP subscribers, net adds, gross installs, subscriber growth rate, FTTP / MDU splits. Search the current period and its target / prior-year basis.

**Sub-B (Penetration):** Penetration overall & by cohort, take-up vs target, churn. Search the current period and target basis.

**Sub-C (Revenue quality):** ARPU, recurring / contracted revenue, premises under service. Search the current period and prior year.

## Red Flag Triggers
- Net subscriber adds negative in a quarter
- Subscriber growth lagging passings growth (penetration slipping)
- Penetration below target curve
- Penetration flat or declining Q/Q
- Churn rising Q/Q
- ARPU declining Q/Q
