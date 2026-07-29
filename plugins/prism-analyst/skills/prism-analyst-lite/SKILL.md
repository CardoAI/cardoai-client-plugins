---
name: prism-analyst-lite
description: Lightweight session-orchestrated variant of prism-analyst - ONE worker agent per wave, no orchestrator agents. Use when the user asks about a Prism deal or transaction, mentions a deal by name (e.g. "NBPE", "westlake", "pavlov"), or asks about portfolio data, NAV, KPIs, sector allocation, or fiber-network metrics that require querying the Prism MCP tools, and the lite variant is explicitly requested or configured as default.
version: 4.0.0
---

# Prism Analyst v4 (Lite) - Session-Orchestrated Single-Agent Waves

Same protocol spine as prism-analyst v3.1.0, restructured for latency: **the main session IS the orchestrator.** It loads deal context, maintains the Working State, spawns ONE worker agent per wave (`model: "sonnet"`), cross-validates results itself, and presents the answer. There are no Opus domain orchestrators and no Haiku sub-agent fan-outs.

```
            MAIN SESSION (orchestrator + validator)
                 |            |            |
  Wave 1:  one Retrieval   Wave 2:     Wave 3:
           worker (sonnet) one Risk    one Reporting
           covering ALL    worker      worker (sonnet)
           in-scope        (sonnet,    - always runs
           domains         only if
                           scoped in)
```

What each worker loses vs v3: redundant multi-strategy retrieval and a dedicated cross-validation layer. What replaces it: the Session Validation Protocol below (structural cross-checks by the session) and unchanged answer-side scoring via `score_answer`.

## Core Protocol

### Step 0 - Clarification Gate

Before any retrieval, evaluate the question for ambiguity on four dimensions 
- **Deal**: Can the deal be resolved to a canonical transaction_id? If not, call `list_deals` and ask.
- **Period**: Is a specific reporting period clear? If ambiguous, ask.
- **Metric**: Is the requested data point specific enough? If vague, ask.
- **Scope**: Single value, trend, or comparison? If unclear, ask.

If ANY dimension is ambiguous, ask ONE concise clarifying question. Do NOT guess.

### Step 1 - Load Deal Context (MANDATORY, done by the session)

1. `list_deals()` - resolve deal name to transaction_id. Results are paginated (default `limit=50`); if the deal isn't in the first page, page through with `offset` before asking the user to disambiguate.
2. `get_deal_skill(transaction_id=<id>)` - load operator playbook
3. `list_field_values(field_name="doc_type", within_transaction_id=<id>)` - discover document types. `field_name` only accepts `transaction_id, doc_type, report_period, table_type, element_type, section, filename, entities` - there is no `entity` or `kpi_name` option here. For entity aliases and KPI names, use `get_deal_skill`'s `entity_aliases` / `kpi_names` fields instead.
Extract: asset_class, periods_available, doc_types, entity aliases, active feedback bundle, enrichment overrides.

### Step 1.5 - Period Resolution

Determine comparison periods from `periods_available`:
- **T** (target): The period the user is asking about
- **T-1** (prior): Immediately preceding period in the list
- **T-1Y** (year-ago): Same calendar position ~12 months earlier
- If user asks about a full year, T = Dec year-end, T-1Y = prior Dec year-end

**Comparison basis is per metric, not global.** Each metric in a domain file declares its basis in the Comparison column:
- `Q/Q` - current period vs the immediately preceding period (quarterly deals)
- `T vs T-1Y` - current vs the same period one year earlier
- `vs target` / `vs trigger` - measured against an underwriting target or a covenant/trigger level, not a prior period
- `n/a` - a snapshot, schedule, or breakdown; no period comparison

Resolve whichever prior periods the loaded set actually needs. A quarterly deal (e.g. fiber) needs T-1 (prior quarter) and T-1Y; an annual deal may need only T-1Y.

### Step 1.6 - Asset-Class Selection

| `asset_class` value | Domain set (shared with v3: `../prism-analyst/references/domains/<slug>/`) | Wave-1 domain scope |
|---------------------|---------------------------------------------------------------------------|---------------------|
| `private_equity` | `private-equity` | Performance, Cash Flow, Composition |
| `fiber_networks` (or confirmed fiber) | `fiber` | Network & Coverage, Commercial & Subscribers, Financial & Cash Flow |

**If `asset_class` is null or is not in the table above**, do NOT silently guess. Pick the most likely set - `private-equity` by default, or another set if the question clearly indicates one (e.g. `fiber` for passings / penetration / ARPU) - then state which set you picked and why, and **ask the user to confirm before running any retrieval**. Do not spawn Wave-1 agents until the user confirms.

**Exception:** if the user's request already names the set explicitly (e.g. "use the fiber metrics for this deal"), treat that as confirmation and proceed without asking.

Confirmation prompt (part of the Step 0 clarification gate):

```
This deal has no asset class set. Based on your question I'd use the
<fiber> metric set (passings, penetration, ARPU). Shall I proceed with
that, or use a different set? (private-equity / fiber / other)
```

Record the confirmed slug in the Working State Deal Context.

### Step 2 - Create Working State File

Create `~/.claude/Projects/Prism/.prism-workspace/session-{deal}-{period}-{timestamp}.md` with the slim template at the end of this file. The session (not the workers) writes to it: after each wave, merge that wave's findings in.

### Step 3 - Wave 1: ONE Retrieval Worker

Apply the Scoping Rules below to decide which domains are in scope. Spawn ONE agent with `model: "sonnet"` whose prompt contains:

- The deal context (transaction_id, periods with any missing-period warnings, doc_types, entity aliases, relevant feedback-bundle rules)
- The comparison periods (T, T-1, T-1Y or "does not exist")
- The user's question
- The question-relevant metric rows AND search strategies from EACH in-scope domain file (`../prism-analyst/references/domains/<set>/<domain>.md`) - one combined brief, not one agent per domain
- This rule, verbatim: **"The metric table in your brief is a catalog, not a checklist. Retrieve the metrics the question needs, plus any required to cross-validate them. Leave the rest unfetched."**
- This rule, verbatim: **"Tag every data point [TABLE] / [TEXT] / [CHART/IMAGE] / [KPI_EXTRACTED] and carry the `chunk_uuid` from the result header for every value - a value without a chunk_uuid cannot be scored later."**
- Budget: at most 10 `search_deal_documents` calls; stop when targets are found or clearly absent. No `render_figure`, no `score_answer`.
- Return contract: verified-metric table (metric, T value, prior value, source type + document + page + chunk_uuid), gaps, candidate red flags, verbatim GP narrative quotes with chunk_uuids, [CHART/IMAGE] values needing corroboration, and the number of MCP calls made.

**Session validation (replaces the v3 Opus orchestrators):** run the Session Validation Protocol on the worker's output, write verified findings to the Working State, and detect cross-domain signals (the v3 Step 3.5 list: value declined while drivers positive, concentration triggers, funding gaps, large FX impact, covenant/liquidity pressure).

### Step 4 - Wave 2: ONE Risk Worker (only when scoped in)

Spawn ONLY when the Scoping Rules call for Risk. ONE agent, `model: "sonnet"`, prompt containing: Wave-1 verified findings, the detected cross-domain signals, the risk domain file's question-relevant rows/strategies, the two verbatim rules from Step 3, a budget of at most 5 searches, and the same return contract. Session validates and merges as in Step 3.

### Step 5 - Wave 3: ONE Reporting Worker (always runs)

ONE agent, `model: "sonnet"`. Its prompt includes the complete Working State and the full chunk_uuid list. It runs, in order, no branches:

1. Fill remaining gaps the final answer genuinely needs (at most 4 searches).
2. Corroborate every [CHART/IMAGE] value **that the answer will use**: `render_figure(chunk_uuid)` pixel-check OR one independent TEXT/TABLE source - stop at the first success; record CORROBORATED / PARTIALLY_CORROBORATED / UNCORROBORATED.
3. Audit GP narrative against verified numbers - produces the `!` flags.
4. Compute period-over-period deltas and flags.
5. Draft the answer per Step 6.
6. Collect ⚠ Flagged Data rows from exactly the three signals in Step 6.
7. `score_answer(question=<user question>, answer=<full draft>, chunk_uuids=[<every chunk used>])` - ONCE, never per metric. Use only `band` and `reason`.
8. Return: the draft, band + reason verbatim, the methodology block (agents, conflicts resolved, corroboration tally), and its MCP call count.

**Session pre-emit check:** every value and named item in the draft has a row in the Sources table; the Working State gets the methodology block; then present.

### Step 6 - Structured Response

Identical contract to v3.1.0. The session presents exactly these sections in this order:

**Period Comparison** table (always included when comparison data exists):

| Metric | Current (T) | Prior (T-1Y) | Delta | % Change | Flag |
|--------|------------|-------------|-------|----------|------|

Flag symbols: `>>>` significant positive (>15%) | `<<<` significant negative (>15%) | `~` stable | `!` directional concern | `-` no prior data | `[T]` at/above target or within trigger headroom | `[X]` below target or breaching a trigger. For `vs target` / `vs trigger` metrics the "Prior" column holds the target/trigger value.

**Answer** - clear, direct response with analysis. Caveats not attached to a specific value belong here, in the prose.

**Sources** - MANDATORY on every answer, never inlined in prose: one row per data point stated (Data Point | Source Type `TABLE`/`TEXT`/`CHART`/`KPI` | Document short form | Page).

**⚠ Flagged Data** - ONLY when at least one flagged item exists. Rows come from exactly three signals, nowhere else: (1) unresolved conflicts from the Session Validation Protocol, (2) UNCORROBORATED or PARTIALLY_CORROBORATED chart values used in the answer, (3) `!` directional-concern flags. Never ask the user to adjudicate these.

**Overall Confidence** - the single `score_answer` band, and the only confidence ever surfaced: `high`/`medium` -> print nothing; `low` -> exactly one line: **`Overall Confidence: 🔴 low`** - `{reason}` (verbatim; if `reason` is null use: *"the answer is not sufficiently grounded in its cited chunks."*). This supersedes the deal playbook's "end with `score:`" directive. No Methodology section, no Caveats section in the answer.

## Scoping Rules

Same table as v3.1.0 - the session scopes Waves 1-2 by query type; **the Reporting worker (Wave 3) always runs**:

| Query Type | Wave 1 domain scope / Wave 2 |
|------------|------------------------------|
| Single metric | The one relevant domain; no Risk |
| Entity / company deep-dive | The two most relevant domains; then Risk |
| Full review / scan | All three domains; then Risk |
| Risk / leverage question | One domain for context; then Risk |
| Comparison question | Relevant domain(s), emphasis on prior-period retrieval |

Multiple in-scope domains still mean ONE Wave-1 worker with a combined brief. When scoping down, still create the Working State - leave unused sections empty.

> Candidate v4.1 addition, deliberately NOT active here to keep benchmarks comparable with v3.1.0: a "List / roster question (top-N holdings, list of X)" row mapping to the single owning domain with no Risk wave.

## Session Validation Protocol

Replaces v3's Sub-Agent Decision Protocol (there is no redundant retrieval to vote over). The session checks, for each wave's output:

1. **Structural cross-checks** - component values foot to stated totals; counts reconcile with the universe (e.g. holdings count vs schedule rows); percentages sum to ~100% where applicable; cross-validation rules listed in the in-scope domain files.
2. **Conflicts between sources** - when two chunks disagree, apply the source hierarchy: admin-approved feedback > audited annual reports > investor presentations > factsheets > schedule of investments > narrative > chart/OCR; within a tier `TABLE` > `TEXT` > `KPI` > `CHART`. Log the decision in the Working State.
3. **Unresolved conflicts** go to ⚠ Flagged Data - an unresolved value has no cleanly-grounded source.
4. **Chunk_uuid audit** - any value arriving without a chunk_uuid is sent back into the Reporting worker's gap-fill list, not silently kept.

## Chart/Image Rules

As in v3.1.0, scoped to values the answer uses: a [CHART/IMAGE] value clears on `render_figure` pixel-check OR one independent TEXT/TABLE source (first success wins). PARTIALLY_CORROBORATED and UNCORROBORATED values are still used but MUST appear in ⚠ Flagged Data. Detection markers: `picture intentionally omitted`, `Start/End of picture text`.

## General Rules

- NEVER skip the Working State file
- NEVER fabricate data - not found means gap/PENDING
- NEVER state a data point without a row in the Sources table
- NEVER ask the user to confirm, correct, or adjudicate a value
- NEVER surface a confidence band other than the single `score_answer` band, and only when `low`
- ALWAYS include period comparison when comparison data exists
- ALWAYS have workers report their MCP call counts; the session records the total in the Working State methodology block
- Worker model is `sonnet` for all three waves unless the user overrides
- For artifacts (dashboard, exported document, chart), apply `../prism-analyst/references/artifact-style.md`
- Use hyphens with spaces instead of em-dashes (user preference)

## References (shared with prism-analyst v3.1.0 - single source of truth)

- `../prism-analyst/references/domains/<asset-class>/*.md` - metric catalogs, search strategies, cross-validation rules, red-flag triggers
- `../prism-analyst/references/prism-tools-reference.md` - Prism MCP tool signatures and pitfalls
- `../prism-analyst/references/artifact-style.md` - artifact styling

## Slim Working State Template

```markdown
# PRISM Working State (lite)
## Session: {deal_id} | T: {target} | T-1: {prior} | T-1Y: {year_ago or "n/a"}
## Created: {timestamp} | Query: {user_question}

## Deal Context
- transaction_id / asset_class / doc_types / entity_aliases / enrichment_overrides
- Periods: T {target}, T-1 {prior}, T-1Y {year_ago or "does not exist"}

## Wave 1 - Retrieval ({domains in scope}) - Status: PENDING|DONE
### Verified Metrics
| Metric | T | Prior | Delta | Source (type, doc, page, chunk_uuid) | Flag |
### Gaps / Red Flags / Narrative Fragments / Chart-Image Points
### Session validation notes (checks run, conflicts resolved)

## Wave 2 - Risk - Status: SKIPPED|PENDING|DONE
(same sub-structure; includes Cross-Domain Signals passed in)

## Wave 3 - Reporting - Status: PENDING|DONE
### Methodology (internal - NEVER shown to the user)
- Workers spawned, MCP call counts, conflicts resolved, corroboration tally, score_answer band
### Final Answer
(the Step 6 structured response as presented)
```

## Differences from v3.1.0 (for reviewers)

1. Orchestration moved into the main session: no Opus domain orchestrators, no Haiku sub-agent fan-out; ONE `sonnet` worker per wave (v3: up to 4 Opus + ~9-12 Haiku).
2. Cross-validation by redundant retrieval replaced by the Session Validation Protocol (structural checks + source hierarchy).
3. Wave 1 covers multiple in-scope domains with one combined brief instead of one agent per domain.
4. Explicit per-worker MCP call budgets (10 / 5 / 4+corroboration) and mandatory call-count reporting.
5. Workers never search periods absent from `periods_available` (v3 sub-agent templates mandated dual-period search unconditionally).
6. Chart corroboration explicitly limited to values the answer uses.
7. Working State slimmed (no sub-agent decision tables); maintained by the session only.
8. Scoping table, Step 6 output contract, source hierarchy, flag symbols, and score_answer usage are UNCHANGED from v3.1.0.
