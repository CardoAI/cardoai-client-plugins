# prism-analyst

Ask questions about your Prism deals in plain language — NAV, cash flows, portfolio composition, risk metrics — and get answers with source citations down to the document and page.

**Installation** (Claude Code or the Claude app): see the [main README](../../README.md).

## What you can ask

- *What's the NAV for `<deal name>` this period, compared to a year ago?*
- *How did realisations and distributions evolve for `<deal name>`?*
- *What's the sector and geography allocation? Any concentration risk?*
- *What are the top 10 holdings, and what changed since last year?*
- *What's the leverage and FX exposure for `<deal name>`?*

The metrics adapt to the deal's asset class - private-equity funds are reviewed on NAV, holdings, and sector allocation; fiber networks on passings, penetration, ARPU, and covenant headroom. If a deal's asset class isn't set, the assistant proposes the most likely set (private equity by default, or fiber if your question is clearly about it) and asks you to confirm before retrieving - unless you already named the set in your request.

The skill activates automatically when you mention a deal name, NAV, KPIs, portfolio data, or similar - no special syntax needed. If it doesn't kick in, ask explicitly: "Use prism-analyst to look up...".

## How it works

Behind each answer, several specialized agents retrieve and cross-check data independently (performance, cash flow, portfolio composition, risk), then a final agent reconciles their findings, cites the source document and page for every data point, and scores the finished answer against the sources it cites.

Every answer lists its sources, so you can trace any number back to a document and page. Chart and image data is treated with extra caution, since it comes from automated extraction rather than structured tables — the chart itself is re-rendered and checked against the surrounding text before the value is used.

Confidence is reported by exception: when the finished answer isn't well grounded in its sources, it's marked **🔴 low** with a one-line reason. No news is good news. Separately, any value the skill couldn't fully verify - a chart reading with no independent confirmation, or a figure two retrieval passes disagreed on - is listed in a **⚠ Flagged Data** table with its source and the specific issue, so you can judge it yourself. The report is never held up waiting for input.

## Support

Questions or issues — contact your CardoAI representative, or dev@cardoai.com.
