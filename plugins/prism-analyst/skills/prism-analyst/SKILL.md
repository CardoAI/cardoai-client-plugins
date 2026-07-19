---
name: prism-analyst
description: Use when the user asks about a Prism deal or transaction, mentions a deal by name (e.g. "NBPE", "westlake", "volkswagen", "ftai"), or asks about portfolio data, sector allocation, top companies, KPIs, NAV, or any financial metric that requires querying the Prism MCP tools.
version: 3.0.0
---

# Prism Analyst - Domain-Orchestrated Multi-Agent Retrieval

This skill uses a hierarchical multi-agent architecture where domain-specialized orchestrator agents (Opus) each spawn and manage their own sub-agents (Haiku), exchange data through a shared Working State file, and produce verified, confidence-scored analysis.

## Architecture

```
                    ┌────────────────────────┐
                    │     WORKING STATE      │
                    │   (shared .md file)     │
                    └──┬───┬───┬───┬───┬────┘
                       │   │   │   │   │
  Wave 1 (parallel):   │   │   │   │   │
    Performance Agent ──┘   │   │   │   │   (each spawns 2-3 Haiku sub-agents)
    Cash Flow Agent ────────┘   │   │   │
    Composition Agent ──────────┘   │   │
                                    │   │
  Wave 2 (reads Wave 1 findings):  │   │
    Risk Agent ─────────────────────┘   │
                                        │
  Wave 3 (reads complete state):        │
    Reporting Agent ────────────────────┘
```

Each domain agent is an Opus orchestrator that:
1. Reads the Working State for cross-domain context
2. Spawns 2-3 Haiku sub-agents in parallel with different search strategies
3. Cross-validates sub-agent results, selects the best value per metric
4. Logs its decision rationale (which sub-agent was chosen and why)
5. Writes verified findings to its section of the Working State
6. Flags gaps and red flags for other domain agents

## Core Protocol

### Step 0 - Clarification Gate

Before any retrieval, evaluate the question for ambiguity:

- **Deal**: Can the deal be resolved to a canonical transaction_id? If not, call `list_deals` and ask.
- **Period**: Is a specific reporting period clear? If ambiguous, ask.
- **Metric**: Is the requested data point specific enough? If vague, ask.
- **Scope**: Single value, trend, or comparison? If unclear, ask.

If ANY dimension is ambiguous, ask a concise clarifying question. Do NOT guess.

### Step 1 - Load Deal Context (MANDATORY)

These are the tools provided by the Prism MCP server. Call them by name:

1. `list_deals()` - resolve deal name to transaction_id. Results are paginated (default `limit=50`); if the deal isn't in the first page, page through with `offset` before asking the user to disambiguate.
2. `get_deal_skill(transaction_id=<id>)` - load operator playbook
3. `list_field_values(field_name="doc_type", within_transaction_id=<id>)` - discover document types. `field_name` only accepts `transaction_id, doc_type, report_period, table_type, element_type, section, filename, entities` - there is no `entity` or `kpi_name` option here. For entity aliases and KPI names, use `get_deal_skill`'s `entity_aliases` / `kpi_names` fields instead.

Extract: periods_available, doc_types, entity aliases, active feedback bundle, enrichment overrides.

### Step 1.5 - Period Resolution

Determine comparison periods from `periods_available`:
- **T** (target): The period the user is asking about
- **T-1** (prior): Immediately preceding period in the list
- **T-1Y** (year-ago): Same calendar position ~12 months earlier
- If user asks about a full year, T = Dec year-end, T-1Y = prior Dec year-end

### Step 2 - Create Working State File

Create the Working State file at:
`~/.claude/Projects/Prism/.prism-workspace/session-{deal}-{period}-{timestamp}.md`

Use the template from `references/working-state-template.md`. Fill in the Deal Context section with data from Steps 1 and 1.5.

### Step 3 - Wave 1: Parallel Domain Agents

Spawn THREE domain agents in parallel using the Agent tool, each with `model: "opus"`:

**Performance Agent** - NAV, returns, value drivers, operating metrics
**Cash Flow Agent** - Realisations, investments, distributions, liquidity
**Composition Agent** - Holdings, sector/geography allocation, portfolio changes

Each domain agent's prompt must include:
- The deal context (transaction_id, periods, doc_types, entity aliases)
- The comparison periods (T, T-1, T-1Y)
- The user's question
- Its domain specification (from `references/domains/<domain>.md`)
- This rule, verbatim: **"The metric table in your domain file is a catalog, not a checklist. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched."**
- This rule, verbatim: **"Require a `chunk_uuid` from every sub-agent for every data point, and pass them through in your findings. Step 5's `score_answer` call needs the `chunk_uuid` of every chunk the answer draws on - a missing one cannot be recovered later."**
- Instructions to spawn 2-3 Haiku sub-agents internally, cross-validate, and return structured findings

Each domain agent must return:
- Verified metrics table (metric, T value, T-1Y value, source, `chunk_uuid`) - Step 5's `score_answer` call needs the `chunk_uuid` of every chunk the answer draws on
- Sub-agent decision log (which sub-agent was selected per metric and why)
- Gaps (metrics it couldn't find)
- Red flags (anomalies detected)
- Narrative fragments (GP quotes for later audit)
- Chart/image data points (tagged for corroboration, with `chunk_uuid` when the source is a figure - needed for `render_figure`)

### Step 3.5 - Merge Wave 1 & Detect Cross-Domain Signals

After all Wave 1 agents return:

1. **Read** all three domain agent outputs
2. **Write** their findings to the Working State file (each to its own section)
3. **Detect cross-domain signals:**
   - If Performance shows NAV declined but EBITDA grew -> flag "multiple contraction" for Risk
   - If Cash Flow shows realisations < distributions -> flag "funding gap" for Risk
   - If Composition shows concentration increased -> flag for Risk
   - If Performance shows large FX impact -> flag for Risk with specific amount
4. **Write** cross-domain signals to the Risk Agent's "Cross-Domain Inputs" section

### Step 4 - Wave 2: Risk Agent

Spawn ONE Risk Agent with `model: "opus"`. Its prompt must include:
- Everything from Wave 1 (via the Working State or direct output)
- The cross-domain signals identified in Step 3.5
- Instructions to investigate these specific signals with targeted sub-agents
- Its domain specification

The Risk Agent:
1. Reads Wave 1 findings and cross-domain signals
2. Spawns 2-3 Haiku sub-agents, including at least one targeted at the flagged signals
3. Cross-validates, writes verified risk metrics to the state
4. Flags any new red flags discovered

### Step 4.5 - Update Working State

Write Risk Agent findings to the Working State. Compile the complete Cross-Domain Red Flags table.

### Step 5 - Wave 3: Reporting Agent

Spawn ONE Reporting Agent with `model: "opus"`. The Reporting Agent ALWAYS runs, on every question, however narrowly scoped - it owns `score_answer`, the Sources table, and the pre-emit check, all of which are mandatory on every answer.

Its prompt must include the complete Working State, all chart/image data points needing corroboration, and all narrative fragments for audit.

The Reporting Agent runs these steps in order. There are no branches:

1. Fill any remaining PENDING metrics (spawn gap-filler Haiku sub-agents)
2. Corroborate every `[CHART/IMAGE]` data point per the Chart/Image Rules below
3. Audit GP narrative against the verified numbers - this produces the `!` flags
4. Compute all period-over-period deltas and flags
5. Draft the answer
6. Collect the ⚠ Flagged Data rows from the three signals listed in Step 6
7. Score the FINAL ANSWER once, never per metric:
   `score_answer(question="<the user's question>", answer="<your drafted answer>", chunk_uuids=[<every chunk_uuid the answer draws on>])`
   Use only the returned `band` and `reason`. Ignore every other field.
8. Write the Methodology block into the Working State's Report Draft section (never into the answer)
9. Self-check before emitting: the Sources table is present and non-empty, and every value stated in the answer has a row in it. Add any missing row; do not emit otherwise
10. Emit the structured response per Step 6

Nothing blocks the report. A `low` band is reported, not adjudicated.

### Step 6 - Structured Response

The Reporting Agent produces, and the parent presents, exactly these sections in this order:

**Period Comparison** table (always included when comparison data exists):

| Metric | Current (T) | Prior (T-1Y) | Delta | % Change | Flag |
|--------|------------|-------------|-------|----------|------|

Flag symbols: `>>>` significant positive (>15%) | `<<<` significant negative (>15%) | `~` stable | `!` directional concern (narrative vs. numbers) | `-` no prior data

**Answer** - clear, direct response with analysis and interpretation. A caveat that is not attached to a specific value belongs here, in the prose, where it is read - not in a footer.

**Sources** - MANDATORY on every answer, never inlined in prose: the provenance of EVERY data point the answer states, one row each - a single-value answer still gets a one-row table, a list gets one row per item. The value itself lives in the Answer; this table cites where each one came from. No per-metric confidence is shown.

| Data Point | Source Type | Document | Page |
|------------|-------------|----------|------|
| NAV ($m) | `TABLE` | 2025 Annual Report | p.62 |
| FX impact | `CHART` | 2025 Annual Report | p.26 |
| Net Cash Flow | `CHART` | Apr 2026 Pres | p.19 |

Column definitions:
- **Source Type**: `TABLE` | `TEXT` | `CHART` | `KPI`
- **Document**: Document name (use short form: "2025 AR", "Apr 2026 Pres", "Dec 2024 FS")
- **Page**: Exact page for traceability

**⚠ Flagged Data** - include ONLY when at least one flagged item exists; omit the section entirely otherwise. Never ask the user to confirm, correct, or adjudicate these values - show them and move on.

```
## ⚠ Flagged Data
These values could not be fully verified. Treat with caution.

| Metric | Value | Source | Issue |
|--------|-------|--------|-------|
| FX impact | +$34m | `CHART` 2025 AR p.26 | uncorroborated; no independent TEXT/TABLE source |
```

Rows come from exactly three signals, and nowhere else:
1. Unresolved sub-agent conflicts (Sub-Agent Decision Protocol, step 6)
2. `UNCORROBORATED` or `PARTIALLY_CORROBORATED` chart values (Chart/Image Rules)
3. `!` directional-concern flags

`score_answer` CANNOT supply these rows - it returns one verdict for the whole answer and identifies no specific value.

**Overall Confidence** - the single `score_answer` band from Step 5, and the only confidence ever surfaced:
- `high` or `medium` -> print no confidence line at all
- `low` -> print exactly one line: **`Overall Confidence: 🔴 low`** - `{reason}`

`{reason}` is `score_answer`'s `reason` field, passed through **verbatim**. Do not paraphrase or invent it. If `reason` is null (which happens when `judge_ran` is false), use exactly: *"the answer is not sufficiently grounded in its cited chunks."*

This supersedes the deal playbook's "end with `score:`" directive - never append a separate `score: high/medium/low` line.

There is no Methodology section and no Caveats section in the answer. Methodology is written to the Working State (Step 5); value-specific caveats live in ⚠ Flagged Data; everything else lives in the Answer prose.

## Scoping Rules

Not every question requires all Wave 1/Wave 2 domain agents. The parent scopes Wave 1 and Wave 2 based on the query. **The Reporting Agent (Wave 3) always runs regardless** - it owns `score_answer`, the Sources table, and the pre-emit check.

| Query Type | Wave 1 / Wave 2 agents to spawn |
|------------|--------------------------------|
| Specific metric (e.g., "what is the NAV?") | Relevant domain agent only (e.g., Performance) |
| Company deep-dive (e.g., "Solenis performance") | Performance + Composition (Wave 1), then Risk (Wave 2) |
| Full review / scan | Performance + Cash Flow + Composition (Wave 1), then Risk (Wave 2) |
| Risk question | Performance (Wave 1 for context) + Risk (Wave 2) |
| Comparison question | Relevant domain(s) with emphasis on T-1Y retrieval |

When scoping down, still create the Working State file - just leave unused domain sections empty.

## Sub-Agent Decision Protocol

Every domain agent follows this when its sub-agents return conflicting data:

1. **Collect** all sub-agent values for the same metric
2. **Compare** - do they agree?
3. **If agree:** Use the value from the most authoritative source (see the hierarchy below)
4. **If disagree:** Apply the Source Reliability Hierarchy, highest tier wins:

   1. **Admin-approved feedback** (enrichment knowledge overrides) - always authoritative, never contradict it
   2. **Annual Financial Reports** - audited, most comprehensive
   3. **Investor Presentations** - detailed but unaudited
   4. **Factsheets** - summary snapshots, may use different classification schemes
   5. **Schedule of Investments** (within any doc) - named holdings with exact values
   6. **Narrative sections** - contextual but may be approximate
   7. **Chart/image extraction** - least reliable, subject to OCR errors

   Within a tier, prefer `TABLE` > `TEXT` > `KPI` > `CHART`. If still tied, use the value confirmed by more sub-agents.
5. **Log** the decision with rationale
6. **Flag** unresolved conflicts in the state - an unresolved value has no cleanly-grounded source, so it will score `low`

## Chart/Image Rules

A `[CHART/IMAGE]` value must be corroborated before the answer uses it. It clears on **at least one** of:

- **(a)** `render_figure(chunk_uuid=<id>)` - a pixel-level check of bar heights, slice sizes, and axis labels against the extracted value, or
- **(b)** an independent `TEXT` or `TABLE` source confirming the same value.

Stop at the first success; you do not need both. Charts frequently publish data that exists nowhere else in the document, so requiring both would permanently flag every waterfall value and the flag would stop carrying information.

Corroboration search order:

1. `render_figure(chunk_uuid)` - check bar heights, slice sizes, axis labels
2. Narrative text on the same or adjacent pages
3. Footnotes and endnotes
4. Tables in the same document
5. The same metric in a different document type
6. Audited financial statements

Record one status per chart value:

- **`CORROBORATED`** - exact value confirmed by `render_figure`, or found in an independent `TEXT` / `TABLE` source (cite it)
- **`PARTIALLY_CORROBORATED`** - a related value was found, but it disagrees (note the discrepancy)
- **`UNCORROBORATED`** - neither check landed

`PARTIALLY_CORROBORATED` and `UNCORROBORATED` values are still used, but they MUST appear in the ⚠ Flagged Data table (Step 6).

Detection markers for chart-sourced text: `picture intentionally omitted`, `Start/End of picture text`.

There is no per-value or per-source confidence - chart values, like all others, feed the single whole-answer `score_answer` band from Step 5.

## General Rules

- NEVER skip the Working State file - it's the backbone of cross-agent communication
- NEVER fabricate data - if not found, mark as PENDING/gap
- NEVER state a data point (number or named item) without citing it - it must have a row in the mandatory Sources table (see Step 6); never inline the source in prose
- NEVER ask the user to confirm, correct, or adjudicate a value. Flagged data is shown, not negotiated (see Step 6's ⚠ Flagged Data)
- NEVER surface a confidence band other than the single whole-answer `score_answer` band, and only when it is `low`. There is no per-metric, per-value, or per-source confidence
- ALWAYS include period comparison when comparison data exists
- When asked to produce an artifact (dashboard, exported document, chart), ALWAYS apply `references/artifact-style.md` - read it first for the palette and layout; never emit an unstyled or off-brand artifact
- Use hyphens with spaces instead of em-dashes (user preference)

## References

- `references/domains/performance.md`, `cash-flow.md`, `composition.md`, `risk.md`, `reporting.md` - per-domain metric catalogs, sub-agent search strategies, cross-validation rules, red flag triggers. Each domain agent reads only its own file.
- `references/working-state-template.md` - Working State file template and lifecycle
- `references/prism-tools-reference.md` - Prism MCP tool signatures, parameters, and common pitfalls
- `references/artifact-style.md` - colors, typography, page layout, and chart-type defaults for rendered artifacts (HTML dashboard, exported document, image).
