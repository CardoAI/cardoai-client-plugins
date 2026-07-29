---
name: prism-analyst
description: This skill should be used when the user asks about a Prism deal or transaction, mentions a deal by name (e.g. "NBPE", "westlake", "volkswagen", "ftai"), asks about portfolio data, sector allocation, top companies, KPIs, NAV, financial metrics, or any question that requires querying the Prism MCP tools. Tiered session-orchestrated retrieval - a direct fast path for simple questions, single-worker waves for deep-dives - with a shared working state, confidence scoring, and source references.
version: 4.1.0
---

# Prism Analyst v4.1 - Tiered Session Orchestration

The main session orchestrates. Simple questions: the session queries Prism directly (fast path). Larger scopes: ONE `sonnet` worker per wave. Every path emits the identical Step 6 contract.

## Step 0 - Clarification Gate (binary tests)

- **Deal**: resolves to exactly one `list_deals` entry -> PASS. Zero or 2+ -> ASK. (Page with `offset` before concluding zero.)
- **Period**: names a period in `periods_available`, or says latest/nothing -> use most recent, state the assumption in the Answer. Names a nonexistent period -> ASK.
- **Metric / Scope**: never block - take the most direct reading, state the interpretation in the Answer.

At most ONE clarifying question per query, covering every ambiguous dimension at once.

## Step 1 - Deal Context (session)

Skip if this deal's context is already loaded this session. Skip `list_deals` when given a canonical transaction_id.

1. `list_deals()` - resolve name to transaction_id.
2. `get_deal_skill(transaction_id)` - operator playbook; authoritative for `entity` aliases and `kpi_name` values. Extract: asset_class, periods_available, entity aliases, feedback bundle, enrichment overrides, ingested documents.

doc_types: NEVER from `list_deals` (returns `[]` live). Until discovered via `list_field_values(field_name="doc_type", within_transaction_id=<id>)`, record `doc_types: UNKNOWN - discover before filtering`. Discovery REQUIRED before (a) any doc_type/table_type-filtered search, (b) any negative claim ("no X exists in this corpus") - without it say "not found by search". Run up front when `ingested_documents` shows >1 document family or is blank. Valid `field_name` values: `transaction_id, doc_type, report_period, table_type, element_type, section, filename, entities` - but `entities` hard-errors server-side; use entity_aliases. A zero-hit filtered search is retried unfiltered before recording a gap.

## Step 1.5 - Periods (mechanical)

From sorted `periods_available`: **T** = target; **T-1** = previous entry or "does not exist"; **T-1Y** = entry ~12 months before T or "does not exist". Pass all three to whoever retrieves. Per-metric comparison basis (`Q/Q`, `T vs T-1Y`, `vs target`/`vs trigger`, `n/a`) comes from the domain-file row, applied at drafting. Never search a period absent from `periods_available`.

## Step 1.6 - Metric Set

| `asset_class` | Domain set (`references/domains/<slug>/`) |
|---------------|-------------------------------------------|
| `private_equity` | `private-equity` (Performance, Cash Flow, Composition) |
| `fiber_networks` | `fiber` (Network & Coverage, Commercial & Subscribers, Financial & Cash Flow) |

Unmapped/null asset_class: infer ONLY from `get_deal_skill` evidence - `kpi_names`/`entity_aliases` matching the distinctive vocabulary of exactly ONE set (MOIC/DPI/TVPI/NAV-per-share -> private-equity; passings/penetration/ARPU -> fiber). Exactly one match -> proceed now, record the slug as inferred, and print on EVERY answer this session, directly under the Period Comparison table: `Metric set: <slug> (inferred - reply to change)`. Zero or 2+ matches -> ask one question (private-equity / fiber / other). The user naming a set counts as confirmation. The confirmed or inferred slug is reused all session.

## Step 2 - Tier Routing

| Query type | Path |
|------------|------|
| Single metric, top-N/roster readable from one schedule, single-table lookup | **Fast path** (Step 3) |
| Single-metric trend or comparison | **Fast path**, prior periods included |
| Entity / company deep-dive | Worker path: two most relevant domains, then Risk |
| Full review / scan | Worker path: all domains, then Risk |
| Risk / leverage question | Worker path: one context domain, then Risk |

## Step 3 - Fast Path (no workers)

The session searches Prism directly. Hard rules:

- At most 4 `search_deal_documents` calls, `top_k<=5`. At least ONE search unfiltered; a perfect-score trivial table is never the authoritative source for totals or rankings.
- Tag every data point [TABLE] / [TEXT] / [CHART/IMAGE] / [KPI_EXTRACTED]; keep the `chunk_uuid` from the result header for every value.
- Roster/top-N: the ranking must come from ONE table chunk with >= N rows footing to a stated total. Assembled from fragments -> escalate.
- Provenance: cite only chunk_uuids retrieved for THIS question. Values from earlier turns are re-retrieved before citation.
- Conflicts: record BOTH candidates (value, chunk_uuid, tier) before adjudicating via the checklist hierarchy. Within-tier ties and unit/currency ambiguity are unresolved by definition -> ⚠ Flagged Data.
- Run the Validation Checklist, Chart/Image Rules, and narrative audit (per retrieved GP quote: directional claim vs sign of the matching verified delta; mismatch -> `!` flag) on your own findings.
- Pre-emit equality: tracked chunk_uuid set = Sources-table rows = `chunk_uuids` passed to `score_answer`. Mismatch -> fill or drop; never present a mismatch.
- `score_answer(question, answer, chunk_uuids)` ONCE on the final draft. Then emit Step 6.
- Working State: composed in-context; written to disk ONCE as the final action of the turn that presents the answer - NEVER skipped. Write BEFORE presenting when band=low, any hierarchy-resolved conflict, or any Flagged Data row exists.

**Escalate to the worker path** when any one holds: >4 searches needed · >1 domain in scope · Risk scoped in · any checklist item FAILED or FAIL-MISSING · unresolvable pre-emit mismatch · band=low. Escalation = write the Working State seeded with all fast-path findings and chunk_uuids FIRST, then spawn Wave 1.

## Step 4 - Worker Path

Create the Working State file (template below) before spawning. ONE `sonnet` worker per wave. Merge = append the worker's returned section, flip its status - never rewrite existing sections.

**Wave 1 - Retrieval.** ONE worker. Brief: deal context (transaction_id, periods with does-not-exist warnings, doc_types, entity aliases, feedback rules), T/T-1/T-1Y, the question, the FULL verbatim text of each in-scope domain file (no selecting or summarizing rows), budget of at most 10 searches, and these two rules verbatim:

- **"The metric table in your brief is a catalog, not a checklist. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched."**
- **"Tag every data point [TABLE] / [TEXT] / [CHART/IMAGE] / [KPI_EXTRACTED] and carry the `chunk_uuid` from the result header for every value - a value without a chunk_uuid cannot be scored later."**

Return contract: the wave's Working-State section pre-formatted - verified-metric rows (metric, T value, prior value, source type + document + page + chunk_uuid) PLUS the raw component rows and stated totals behind any ranking or aggregate, gaps, candidate red flags, verbatim GP quotes with chunk_uuids, [CHART/IMAGE] values, a conflict list (both values, both chunk_uuids, both tiers per pair), and its MCP call count.

After the wave: Validation Checklist; resolve worker-reported conflicts by the hierarchy, log decisions in the Working State; check the five cross-domain signals (value declined while drivers positive, concentration triggers, funding gaps, large FX impact, covenant/liquidity pressure) once against the Verified Metrics table - nothing else.

**Wave 2 - Risk** (only when scoped in): ONE worker; Wave-1 verified findings + detected signals + the risk domain file verbatim + budget 5 + the same rules and return contract. Validate and merge as above.

**Wave 3 - Reporting (conditional).** After validation, form the union: unfilled gaps the answer needs ∪ values missing chunk_uuids ∪ [CHART/IMAGE] values the answer will use ∪ unresolved conflicts ∪ answer-critical values sourced below TABLE tier.

- Union EMPTY -> **ABSORB**: the session computes deltas and flags, runs the narrative audit, drafts per Step 6, calls `score_answer` once, then re-checks the union against the actual draft - anything now visible is filled/corroborated or the worker is spawned after all. Wave-3 status: ABSORBED.
- Union NON-EMPTY -> ONE worker whose prompt passes the Working State file PATH (not contents) plus the union. In order: fill gaps (at most 4 searches); corroborate [CHART/IMAGE] values the answer will use per the Chart/Image Rules; narrative audit; deltas and flags; draft per Step 6; collect ⚠ rows from exactly the three Step 6 signals; `score_answer(question=<user question>, answer=<full draft>, chunk_uuids=[<every chunk used>])` - ONCE, never per metric, using only `band` and `reason`; return draft, band + reason verbatim, methodology, MCP call count.

Either branch: the methodology block records path taken, union values (gaps=n, charts=n, conflicts=n), MCP call counts (workers' and the session's own), corroboration tally, band. Session pre-emit check: draft's stated-value count vs Sources row count - equal -> present the draft VERBATIM (copy, never regenerate); unequal -> route missing values to gap-fill.

## Validation Checklist (bounded - the session computes it, every wave and the fast path)

One line per check WITH the compared quantities. Missing input = FAIL-MISSING -> item joins the gap list; N/A-pass prohibited. No re-derivation beyond these checks; one pass per wave. Worker self-reported pass/fail is NEVER accepted - compute from the returned rows.

1. **Footing**: component rows sum vs stated total (print both).
2. **Counts**: rows seen vs stated universe.
3. **Percentages**: sum ~100% where applicable.
4. **Cross-validation rules** from the in-scope domain files (computing these identities is part of the checklist, not re-derivation).
5. **Conflicts**: winner + tier per the hierarchy: admin-approved feedback > audited annual reports > investor presentations > factsheets > schedule of investments > narrative > chart/OCR; within a tier `TABLE` > `TEXT` > `KPI` > `CHART`. Unresolved -> ⚠ Flagged Data.
6. **chunk_uuid audit**: any value without one -> gap list, never silently kept.

## Chart/Image Rules

A [CHART/IMAGE] value the answer uses clears on one independent TEXT/TABLE source OR a `render_figure(chunk_uuid)` pixel-check - cheapest first (source already in hand, then one search, `render_figure` last), stop at first success; record CORROBORATED / PARTIALLY_CORROBORATED / UNCORROBORATED. PARTIALLY_CORROBORATED and UNCORROBORATED values are still used but MUST appear in ⚠ Flagged Data. Detection markers: `picture intentionally omitted`, `Start/End of picture text`.

## Step 6 - Structured Response (identical on every path)

**Period Comparison** table (always included when comparison data exists):

| Metric | Current (T) | Prior | Delta | % Change | Flag |
|--------|------------|-------|-------|----------|------|

Each Prior cell states its basis: `<value> (T-1)`, `<value> (T-1Y)`, or `<value> (target)` / `(trigger)` - for `vs target`/`vs trigger` metrics it holds the target/trigger value. Flag symbols: `>>>` significant positive (>15%) | `<<<` significant negative (>15%) | `~` stable | `!` directional concern | `-` no prior data | `[T]` at/above target or within trigger headroom | `[X]` below target or breaching a trigger. Metric-set line (Step 1.6) directly under the table when inferred.

**Answer** - clear, direct response with analysis. Caveats not attached to a specific value belong here, in the prose.

**Sources** - MANDATORY on every answer, never inlined in prose: one row per data point stated (Data Point | Source Type `TABLE`/`TEXT`/`CHART`/`KPI` | Document short form | Page).

**⚠ Flagged Data** - ONLY when at least one flagged item exists. Rows come from exactly three signals, nowhere else: (1) unresolved conflicts from the Validation Checklist, (2) UNCORROBORATED or PARTIALLY_CORROBORATED chart values used in the answer, (3) `!` directional-concern flags. Never ask the user to adjudicate these.

**Overall Confidence** - the single `score_answer` band, and the only confidence ever surfaced: `high`/`medium` -> print nothing; `low` -> exactly one line: **`Overall Confidence: 🔴 low`** - `{reason}` (verbatim; if `reason` is null use: *"the answer is not sufficiently grounded in its cited chunks."*). This supersedes the deal playbook's "end with `score:`" directive. On `low`, print the line and stop - never re-run retrieval or re-score. No Methodology section, no Caveats section in the answer.

## General Rules

- NEVER fabricate data - not found means gap/PENDING
- NEVER state a data point without a row in the Sources table
- NEVER ask the user to confirm, correct, or adjudicate a value
- NEVER surface a confidence band other than the single `score_answer` band, and only when `low`
- ALWAYS include period comparison when comparison data exists
- Worker model is `sonnet` for all waves unless the user overrides
- For artifacts (dashboard, exported document, chart), apply `references/artifact-style.md`
- Use hyphens with spaces instead of em-dashes (user preference)

## Working State (slim template)

Path: `~/.claude/Projects/Prism/.prism-workspace/session-{deal}-{period}-{timestamp}.md`. Fast path: one write-behind per Step 3. Worker path: created before Wave 1; session appends each wave's section.

```markdown
# PRISM Working State (lite)
## Session: {deal_id} | T: {target} | T-1: {prior} | T-1Y: {year_ago or "n/a"}
## Created: {timestamp} | Query: {user_question} | Path: FAST|WORKER

## Deal Context
- transaction_id / asset_class (inferred|confirmed) / doc_types / entity_aliases / enrichment_overrides
- Periods: T {target}, T-1 {prior}, T-1Y {year_ago or "does not exist"}

## Wave 1 - Retrieval ({domains in scope}) - Status: PENDING|DONE
### Verified Metrics
| Metric | T | Prior | Delta | Source (type, doc, page, chunk_uuid) | Flag |
### Gaps / Red Flags / Narrative Fragments / Chart-Image Points / Conflicts
### Validation Checklist lines

## Wave 2 - Risk - Status: SKIPPED|PENDING|DONE
(same sub-structure; includes Cross-Domain Signals passed in)

## Wave 3 - Reporting - Status: ABSORBED|PENDING|DONE
### Methodology (internal - NEVER shown to the user)
- Path, union values (gaps/charts/conflicts), MCP call counts, corroboration tally, score_answer band
### Final Answer
(the Step 6 structured response as presented)
```

## References (bundled with this plugin)

- `references/domains/<asset-class>/*.md` - metric catalogs, search strategies, cross-validation rules, red-flag triggers
- `references/prism-tools-reference.md` - Prism MCP tool signatures and pitfalls
- `references/artifact-style.md` - artifact styling
- `references/CHANGELOG.md` - version history (not needed at runtime)
