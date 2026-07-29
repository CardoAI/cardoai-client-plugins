# Prism MCP Tools - Reference

## Tool Chain

```
list_deals() --> get_deal_skill(transaction_id)
                    |
                    v
            list_field_values(field_name, within_transaction_id)   [only when needed]
                    |
                    v
            search_deal_documents(query, transaction_id, report_period, ...filters)
                    |
                    +--> render_figure(chunk_uuid)   [figure chunks only]
                    |
                    v
            score_answer(question, answer, chunk_uuids)   [once, on the final answer]
```

## list_deals

- **Parameters**: `limit` (default 50, max 200), `offset` (default 0)
- **Returns**: `{id, asset_class, description, doc_types, skill_enrichment_enabled, last_enriched_at}` per deal, plus `total` and `has_more`
- Paginated - page with `offset` before concluding a deal does not exist.
- `skill_enrichment_enabled: false` or a stale `last_enriched_at` predicts a thin playbook. Expect empty `entity_aliases` / `kpi_names` and plan to discover entities yourself.

## get_deal_skill

- **Parameters**: `transaction_id` (required)
- **Returns**: snapshot (asset_class, periods_available, ingested_documents), auto-enriched narrative, entity aliases, KPI scope, retrieval tips, the active feedback bundle (admin-approved, authoritative) and pending suggestions (advisory only)
- Must be called before answering any deal question.
- Authoritative source for a deal's valid `entity` and `kpi_name` values - `list_field_values` does **not** enumerate those two fields.
- The narrative and description are also how you infer the domain set when `asset_class` is not a recognised literal.

## list_field_values

- **Parameters**: `field_name` (required) - one of `transaction_id`, `doc_type`, `report_period`, `table_type`, `element_type`, `section`, `filename`, `entities`; `within_transaction_id` (optional); `limit` (default 100, max 1000)
- **Returns**: distinct values with counts, descending
- Cheap. Use it to learn the entity universe on an unenriched deal, or to confirm a filter value exists before spending a search on it.

## search_deal_documents

- **Required**: `query`, `transaction_id`, `report_period` (`YYYY-MM-DD`, or `"all"` only for genuinely cross-period questions)
- **Optional filters**: `doc_type`, `table_type`, `element_type` (`narrative`, `table`, `figure`, `list`, `loan_tape_summary`), `entity`, `kpi_name`, `kpi_value_gte`, `kpi_value_lte`, `top_k` (default 10, max 50)
- **Returns**: ranked chunks with filename, page/sheet, section, tags (`tx`, `period`, `doc_type`, `element`, plus `table_type` and `chunk_uuid` when present), score, entities, KPIs, chunk text
- No pagination - if `top_k` is hit, narrow with a filter.
- `retrieval_confidence` (strong / moderate / weak) rates how the **search** looked. It says nothing about whether an answer built from the results is correct.

**The highest-value call is usually the first one**: `element_type="table"`, `top_k=25`, querying the document-wide roster or schedule concept. A single fund-wide table answers a whole roster question at once and is more reliable than assembling the same ranking from per-entity sections.

## render_figure

- **Parameters**: `chunk_uuid` (required), from a result header where `element_type="figure"`
- **Returns**: cropped PNG of the figure plus filename/page/section metadata
- For pixel-level checks (bar heights, slice sizes, axis labels) that a text transcription can approximate but not guarantee. On a chart page the `[FIGURE]` chunk carries the actual values; a narrative chunk's KPIs for the same chart can be approximate.

## score_answer

**Live signature** (`gp_mcp/mcp_tools/retrieval.py`):

- `question` (str, required), `answer` (str, required), `chunk_uuids` (list[str], required), `stop_reason` (str | None, optional - usually omit)
- **There is no `citations` parameter on the MCP surface.** Verbatim-citation support exists in the backend's structured-extraction path, not in this tool. Do not build toward passing citations here.

**Returns** `AnswerConfidence`: `band` (`high` / `medium` / `low`), `reason`, plus sub-judgments `answer_type`, `evidence_sufficiency`, `contradicts_evidence`, `answer_overreaches`, `answer_addresses_question`, `refusal_justified`, `judge_ran`, and `rubric_json`. This skill reads only `band` and `reason`. When `judge_ran` is `false` the deterministic gate was terminal and every sub-judgment is null; `reason` is nullable regardless, so any use needs a fallback.

**Scope**: certifies grounding in the **supplied** chunks. Not global correctness, not retrieval recall. An answer that cites only agreeable chunks can score well while being wrong - retrieval strategy is what guards against that, not scoring. It identifies no specific value, so the Flagged Data table is never built from it.

**Confidence ceilings - why `medium` is often the maximum.** The backend applies page-level caps before the judge runs:

- A cited page that is **scanned** sets a **hard** ceiling of `medium` (`extraction/confidence/signals.py`, `apply_page_ceilings`).
- Page **complexity** >= 2 sets a **soft** ceiling of `medium` (`_COMPLEXITY_TO_CEILING`).
- The soft ceiling lifts on strong grounding - for chat-kind scoring that condition is satisfied automatically (`extraction/confidence/gates.py`).
- The hard ceiling does **not** lift. Strong grounding against a scanned page returns `medium` with reason `grounding_strong_capped_by_scanned_page`.

So on a deal whose documents are scanned PDFs, no answer can score `high` however well grounded it is. Treat `medium` there as a pass. Never compare bands across deals as a quality metric, and never drop citations chasing a higher band.

## Common Pitfalls

- **Featured is not largest.** A GP report's dedicated company write-ups reflect editorial choice, not size. Rank from a fund-wide table.
- **Check the basis before declaring a conflict.** Gross MOIC is commonly struck on total value (realized + unrealized) while a holdings roster ranks on unrealized value alone; a "largest position" stat may be on invested capital rather than fair value. Both look like errors and are not.
- Factsheets and annual reports may use different sector classification schemes.
- OCR from pie charts can misattribute percentages to adjacent labels.
- Sub-sector percentages ("Software 49% of TMT") are not portfolio-level allocations.
- "As of" dates in presentations often differ from the reporting period.
- Enrichment KPIs extracted automatically can misparse complex table layouts.
- Entity aliases matter - check `get_deal_skill` for canonical names.
- There is no tool to persist data back to Prism; values are read-only within a session.
- Deals can live on different Prism MCP servers within a tenant. If one server errors, check whether the deal is on another before concluding it is missing.
