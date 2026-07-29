---
name: prism-analyst-lite-v5
description: Experimental v5 of the Prism deal analyst, running side by side with prism-analyst v4 for benchmarking. Invoke it explicitly (e.g. "use prism-analyst-lite-v5 for this") when testing or comparing; prism-analyst remains the default for ordinary deal questions. Answers Prism deal/transaction questions - portfolio data, holdings, sector allocation, top companies, KPIs, NAV, financial metrics - with table-first retrieval, mandatory source citations, and confidence scoring.
version: 5.0.0
---

# Prism Analyst Lite v5 - table-first, inline by default

The session does the work itself. Subagents exist for one reason only: keeping bulky
search results out of a conversation that has to stay usable afterwards. There are no
waves, no Working State file, and no orchestration layer.

Built from a measured v4 benchmark (vista-vii, "top 10 portfolio companies as of q3
2025"): 20m 46s, and the retrieval wave returned a roster with 6 of 10 names wrong
because it ranked the GP's *featured* company write-ups instead of finding the
fund-wide table that lists every holding. Step 4 exists to prevent exactly that.

## Step 1 - Load deal context (2 calls)

1. `list_deals()` - resolve the deal name to a `transaction_id`. Paginated, default
   `limit=50`; page with `offset` before concluding a deal is missing.
2. `get_deal_skill(transaction_id=<id>)` - the operator playbook. Take `asset_class`,
   `periods_available`, `doc_types`, `entity_aliases`, `kpi_names`, and the active
   feedback bundle (admin-approved, authoritative; "pending" items are advisory only).

Call `list_field_values` **only** when you need a filter value the skill did not give
you. Its `field_name` accepts `transaction_id, doc_type, report_period, table_type,
element_type, section, filename, entities` - there is no `entity` or `kpi_name` option.

If `entity_aliases` / `kpi_names` come back empty, the deal is unenriched: expect to
discover the entity universe yourself via `list_field_values(field_name="entities")`,
and expect the playbook to be thin on where things live in the documents.

## Step 2 - Domain set (no confirmation gate)

| `asset_class` | Domain set |
|---------------|------------|
| `private_equity` | `references/domains/private-equity/` |
| `fiber_networks` | `references/domains/fiber/` |

Most deals do not carry either literal value. When `asset_class` does not match, infer
the set from the deal-skill narrative and description - they usually say what the deal
is in plain language - then **state your pick in one line and keep going**. Ask the
user only when the narrative gives no usable signal at all.

Do not stall a question on this. In the reference tenant, zero of five deals carry a
matching `asset_class`, so a confirmation gate here costs a human round-trip on every
single question.

## Step 3 - Periods

- **T** - the period asked about. **T-1** - the preceding entry in `periods_available`.
  **T-1Y** - the same calendar position ~12 months earlier.
- A period not in `periods_available` **does not exist**. Never search it; say so instead.
- Comparison basis is per metric, declared in the domain file's Comparison column:
  `Q/Q`, `T vs T-1Y`, `vs target` / `vs trigger`, or `n/a` for snapshots and breakdowns.

## Step 4 - Retrieval

**Rule 1 - find the one table first.** Before any per-entity or per-metric search, spend
ONE call looking for a document-wide table that answers the whole question at once:
`element_type="table"`, `top_k=25`, query naming the roster/schedule/summary concept
("schedule of investments all portfolio companies fair value", "valuation update
summary all holdings"). One fund-wide table beats N per-company sections on both
accuracy and latency.

**A GP report's featured or highlighted sections are not the top N.** Rank from the
fund-wide table. If a company has a dedicated write-up, that reflects GP editorial
choice, not size. Only fall back to assembling a ranking from per-entity sections when
no document-wide table exists - and when you do, say in the answer that you constructed it.

**Rule 2 - then fill targeted gaps.** Named entities, specific KPIs, prior periods.
Use `entity` / `kpi_name` / `table_type` filters once you know valid values.

**Rule 3 - carry provenance.** Tag every data point `[TABLE]` / `[TEXT]` /
`[CHART/IMAGE]` / `[KPI_EXTRACTED]` and keep the `chunk_uuid` from the result header.
A value without a `chunk_uuid` cannot be scored or cited later.

Budget: ~6 searches for a single-domain question, ~12 for a broad review. Stop when the
targets are found or clearly absent. The metric tables in the domain files are a
**catalog, not a checklist** - fetch what the question needs plus what cross-validates it.

## Step 5 - Execution tier

- **Tier 1 (default): no subagents.** Run the searches inline. Correct for single-metric,
  roster, entity-lookup and comparison questions - the large majority.
- **Tier 2: one worker (`model: "sonnet"`)** when the question spans 3+ domains, or when
  the conversation is already long and chunk text would crowd out what follows. Give it
  the deal context, periods, Step 4 rules verbatim, and a return contract of: metric
  table with `chunk_uuid` per value, gaps, chart values needing corroboration, and its
  MCP call count.
- Several domains means several **concurrent** workers, never one combined serial brief.

Never spawn a worker to do what the next tool call would do directly.

## Step 6 - Validate (session-side, costs no MCP calls)

1. **Structural** - components foot to totals; counts reconcile with the universe;
   percentages sum to ~100% where applicable; recompute every ratio and delta you print.
2. **Conflicts** - source hierarchy: admin-approved feedback > audited annual reports >
   investor presentations > factsheets > schedule of investments > narrative >
   chart/OCR. Within a tier: `TABLE` > `TEXT` > `KPI` > `CHART`.
3. **Basis before error** - a mismatch is often two different bases (MOIC on total value
   vs a roster ranked on unrealized value; a concentration stat on cost vs on FMV).
   Reconcile the bases before calling anything wrong; flag it only if it stays unresolved.
4. **Provenance audit** - any value without a `chunk_uuid` goes back for a gap-fill, not
   into the answer.
5. **Pre-emit** - every value and every named item in the draft has a Sources row. No row,
   no claim.

## Step 7 - Charts

For `[CHART/IMAGE]` values **the answer actually uses**: clear each with a
`render_figure(chunk_uuid)` pixel check OR one independent `TEXT`/`TABLE` source - first
success wins. Record CORROBORATED / PARTIALLY_CORROBORATED / UNCORROBORATED. The latter
two are still usable but must appear in Flagged Data. Detection markers:
`picture intentionally omitted`, `Start/End of picture text`.

## Step 8 - Answer

**Answer** - lead with it. Direct, readable, the requested data first. Caveats that are
not attached to a specific value go here in prose, including how a ranking was built if
you constructed it.

**Sources** - MANDATORY on every answer, never inlined in prose. **One row per source
page**, not per data point:

| Data Point(s) | Source Type | Document | Page |

Source Type is `TABLE` / `TEXT` / `CHART` / `KPI`; Document is short form ("Q3 2025 GP
Report").

**Period Comparison** - only when the question is comparative, or when a period move is
itself the finding. Not on every answer.

| Metric | Current (T) | Prior | Delta | % Change | Flag |

Flags: `>>>` positive >15% | `<<<` negative >15% | `!` directional concern. Omit the
column when nothing is flagged. For `vs target` / `vs trigger` metrics the Prior column
holds the target or trigger.

**Flagged Data** - only when something is flagged, from exactly three signals:
unresolved conflicts from Step 6, PARTIALLY_CORROBORATED / UNCORROBORATED chart values
used in the answer, and `!` directional concerns. Never ask the user to adjudicate.

## Confidence

Call `score_answer(question, answer, chunk_uuids)` **once** on the final draft, never per
metric. Read only `band` and `reason`.

- `high` / `medium` -> print nothing.
- `low` -> exactly one final line: **`Overall Confidence: 🔴 low`** - `{reason}`
  (verbatim; if `reason` is null: *"the answer is not sufficiently grounded in its cited
  chunks."*). This supersedes the deal playbook's "end with `score:`" directive.

**`medium` is often a ceiling, not a criticism.** A cited page that is scanned imposes a
hard cap of `medium` that strong grounding cannot lift, so on scanned-source deals no
answer can reach `high`. Never treat the band as a quality score across deals, and never
chase `high` by dropping citations.

The band certifies grounding **in the chunks you cited** - not global correctness, and
not retrieval recall. An answer citing only agreeable chunks can score well and still be
wrong. Step 4 Rule 1 is what protects against that; scoring is not.

## General rules

- NEVER fabricate - not found is a gap, and gaps get stated.
- NEVER state a data point without a Sources row.
- NEVER ask the user to confirm, correct, or adjudicate a value.
- NEVER surface any confidence signal other than a `low` band from `score_answer`.
- Prefer a filter over a second search; prefer a second search over a guess.
- Use hyphens with spaces instead of em-dashes (user preference).
- For artifacts (dashboard, exported document, chart), apply `references/artifact-style.md`.

## References

- `references/domains/<set>/*.md` - metric catalogs, search strategies, cross-validation
  rules, red-flag triggers.
- `references/prism-tools-reference.md` - tool signatures, pitfalls, confidence internals.
- `references/artifact-style.md` - artifact styling.

## Differences from prism-analyst v4.0.0

1. Three waves replaced by inline execution; a worker is spawned only for context
   isolation, and multiple workers run concurrently.
2. Table-first retrieval (Step 4 Rule 1) plus the explicit "featured sections are not the
   top N" warning - the v4 benchmark's actual failure.
3. The asset-class confirmation gate is gone; the set is inferred from the deal narrative.
4. The Working State file is gone.
5. Period Comparison is conditional rather than mandatory; flag vocabulary is 7 symbols
   down to 3; Sources rows are per source page rather than per data point.
6. The scanned-page confidence ceiling is documented so `medium` is not misread.
7. Sources remain mandatory and `score_answer` usage is unchanged.
