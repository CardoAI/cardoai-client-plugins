# Cash Flow Agent

**Focus:** Realisations, investments, distributions, liquidity | **Wave:** 1 | **Model:** opus

Protocol, decision rules, source hierarchy, and output format: see `SKILL.md`. This file is your metric catalog and search strategies only - it deliberately restates none of them.

The metric table below is a **catalog, not a checklist**. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched.

## Metrics
| Metric ID | Metric | Type | Comparison |
|-----------|--------|------|------------|
| CF-01 | Total realisations ($m) | Flow | T vs T-1Y |
| CF-02 | Realisations as % of opening portfolio | Flow | T vs T-1Y |
| CF-03 | New investments deployed ($m) | Flow | T vs T-1Y |
| CF-04 | Follow-on investments ($m) | Flow | T vs T-1Y |
| CF-05 | Dividends paid ($m) | Flow | T vs T-1Y |
| CF-06 | Dividends per share ($) | Flow | T vs T-1Y |
| CF-07 | Share buybacks ($m) | Flow | T vs T-1Y |
| CF-08 | Total capital returned ($m) | Flow | T vs T-1Y |
| CF-09 | Full exits (names + proceeds) | Flow | n/a |
| CF-10 | Partial exits (names) | Flow | n/a |
| CF-11 | Realisation MOIC (x) | Flow | T vs T-1Y |

## Sub-Agent Strategies
**Sub-A (Realisations):** Search for exits, realisations, proceeds, liquidity events. Query: "realisations exits proceeds cash received full partial sale". Search T and T-1Y.

**Sub-B (Deployments):** Search for new investments, follow-ons, commitments. Query: "new investments deployed follow-on commitments capital calls". Search T and T-1Y.

**Sub-C (Returns to Shareholders):** Search for dividends, buybacks, capital return. Query: "dividends share buyback capital returned shareholders repurchase". Search T and T-1Y.

## Cross-Validation Rules
- Total capital returned ~ dividends + buybacks
- Realisations should be >= capital returned (funding source)
- Named exits should reconcile with Schedule of Investments changes

## Red Flag Triggers
- Realisations < dividends + buybacks (funding gap)
- New investments > realisations (net cash drain)
- Realisation MOIC < 1.0x (exits below cost)
