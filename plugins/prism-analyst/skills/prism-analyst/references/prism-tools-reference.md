# Prism MCP Tools - Complete Reference

## Tool Chain Overview

```
list_deals() --> get_deal_skill(transaction_id)
                    |
                    v
            list_field_values(field_name, within_transaction_id)
                    |
                    v
            search_deal_documents(query, transaction_id, report_period, ...filters)
                    |
                    +--> render_figure(chunk_uuid)   [only for figure/chart chunks]
                    |
                    v
            score_answer(question, answer, chunk_uuids)   [once, on the final answer]
```

## Tool Signatures

### list_deals
- **Parameters**: `limit` (integer, default 50, max 200), `offset` (integer, default 0)
- **Returns**: one page of `{id, asset_class, description, doc_types, skill_enrichment_enabled, last_enriched_at}` plus `total` and `has_more`
- **Purpose**: Discover available deals and resolve free-text deal names to canonical transaction_id. Paginated - if the deal isn't on the first page, page with `offset` before concluding it doesn't exist.

### get_deal_skill
- **Parameters**: `transaction_id` (string, required)
- **Returns**: Operator playbook with:
  - Snapshot (asset_class, periods_available, ingested_documents)
  - Auto-enriched narrative, entity aliases, KPI scope, retrieval tips
  - Active feedback bundle (admin-approved, authoritative)
  - Pending suggested feedback (advisory only)
- **CRITICAL**: Must be called BEFORE answering any deal question
- This is also the authoritative source for a deal's valid `entity` and `kpi_name` values (via `entity_aliases` / `kpi_names`) - `list_field_values` does NOT enumerate those two fields.

### list_field_values
- **Parameters**:
  - `field_name` (string, required) - one of: `transaction_id`, `doc_type`, `report_period`, `table_type`, `element_type`, `section`, `filename`, `entities`
  - `within_transaction_id` (string, optional) - scope to specific deal
  - `limit` (integer, default 100, max 1000)
- **Returns**: Distinct values with counts, ordered by count descending
- **Purpose**: Discover valid filter values before calling `search_deal_documents`. Does NOT cover `entity` (singular, the search filter) or `kpi_name` - get those from `get_deal_skill`.
- **Known defect**: `field_name="entities"` currently hard-errors server-side ("the system rejected the request") despite being listed as valid - use `get_deal_skill` entity_aliases instead. Note also that `list_deals` returns `doc_types: []` for all deals; this tool is the only reliable doc_type inventory.

### search_deal_documents
- **Parameters (required)**:
  - `query` (string) - search question or terms
  - `transaction_id` (string) - canonical deal id (no "all")
  - `report_period` (string) - YYYY-MM-DD or literal "all" (only for genuinely cross-period questions)
- **Parameters (optional filters)**:
  - `doc_type` (string)
  - `table_type` (string)
  - `element_type` (string) - `narrative`, `table`, `figure`, `list`, `loan_tape_summary`
  - `entity` (string)
  - `kpi_name` (string)
  - `kpi_value_gte` (number)
  - `kpi_value_lte` (number)
  - `top_k` (integer, default 10, max 50)
- **Returns**: Ranked chunks (narrative, tables, figures) with filename, page/sheet, section, tags (`tx`, `period`, `doc_type`, `element`, plus `table_type` and `chunk_uuid` when present), score, entities, KPIs, and chunk text. No pagination - narrow with filters if `top_k` is hit.

### render_figure
- **Parameters**: `chunk_uuid` (string, required) - from a `search_deal_documents` result header where `element_type="figure"`
- **Returns**: An MCP image content block (cropped PNG of the figure) followed by filename/page/section metadata
- **Purpose**: Pixel-level verification of chart data (bar heights, slice sizes, axis labels) that a figure's text transcription can approximate but not guarantee. Use this to corroborate `[CHART/IMAGE]` data points instead of relying on text alone - only `element_type="figure"` chunks render.

### score_answer

- **Parameters** (verified against the live server, Oxygen Prism v3.2.4):
  - `question` (string, **required**) - the user's original question
  - `answer` (string, **required**) - the whole drafted answer
  - `chunk_uuids` (list of string, **required**) - every chunk the answer draws on
  - `citations` (list of `{chunk_uuid, cited_text}`, optional, default `null`) - verbatim receipts. `cited_text` must be ONE contiguous, character-exact span copied from that chunk - no paraphrasing, no reformatted numbers, no stitched-together fragments.
  - `stop_reason` (string, optional, default `null`) - answer-generation stop reason, e.g. `end_turn`. Usually omit.
- **Returns**: an `AnswerConfidence` object:

```python
class AnswerConfidence(BaseModel):
    band: ConfidenceBand          # 'high' | 'medium' | 'low'
    reason: str | None            # one-line explanation of the verdict
    answer_type: str | None       # 'substantive' | 'refusal'
    evidence_sufficiency: str | None      # 'yes' / 'partial' / 'no'
    contradicts_evidence: str | None      # 'yes' / 'no'
    answer_overreaches: str | None        # 'yes' / 'no'
    answer_addresses_question: str | None # 'yes' / 'partial' / 'no'
    refusal_justified: str | None         # 'yes' / 'partial' / 'no' / 'n/a'
    judge_ran: bool               # False if the deterministic gate was terminal
    rubric_json: dict             # raw signals, telemetry only
```

- **Purpose**: Certify that a drafted answer is grounded in the chunks it cites. Called ONCE on the final answer, never per metric.
- **CRITICAL - what it does NOT do:**
  - It **certifies grounding in the SUPPLIED chunks, not global correctness.** A `high` band means "faithful to the chunks you chose to cite". An answer that cites only agreeable chunks can earn `high` while being wrong. Never present the band as a correctness guarantee.
  - It **identifies no specific value.** There is no per-claim or per-chunk breakdown in the response. Do not attempt to source a "which value is ungrounded" list from it - the ⚠ Flagged Data table is built from the skill's own signals (see `SKILL.md` Step 6).
  - When `judge_ran` is `False` the deterministic gate was terminal and **every sub-judgment field is null**. `reason` is `str | None` regardless, so any use of it needs a fallback.
- **Usage in this skill**: only `band` and `reason` are read. All other fields are ignored by design - see `SKILL.md` Step 3 (fast path), Step 4 Wave 3, and Step 6.
- **`citations` is not currently sent.** The skill passes only the three required parameters. The tool calls `citations` "strongly recommended": *"With verbatim `citations` the engine verifies each quote against its chunk (extraction-style receipts); without them it falls back to matching the whole answer."* Verified quotes let it *"certify grounding deterministically (and lift the page-complexity cap) instead of judging a prose answer."* This is also why `judge_ran` is effectively always true - omitting `citations` guarantees the LLM-judge fallback. Adopting `citations` would change the sub-agent contract (every sub-agent returning character-exact spans) and is deliberately deferred.

## Source Reliability Hierarchy

Owned by `SKILL.md`'s Validation Checklist (the 7-tier hierarchy). Not restated here.

## Common Pitfalls

- Factsheets and Annual Reports may use different sector classification schemes
- OCR from pie charts can misattribute percentages to adjacent labels
- Sub-sector percentages (e.g., "Software 49% of TMT") are NOT portfolio-level allocations
- "As of" dates in presentations often differ from the reporting period (e.g., April 2024 presentation shows March 31, 2024 data)
- Enrichment KPIs extracted by Haiku may occasionally misparse complex table layouts
- Entity aliases are important - always check `get_deal_skill` for canonical names
- There is no tool to persist data back to Prism - values are read-only within a session
