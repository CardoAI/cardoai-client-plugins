# prism-analyst - Version History

Not needed at runtime. Reviewer/maintainer reference only.

## 4.1.0 (2026-07-29) - Tiered trim

Motivation: v4.0.0 measured 7m05s on the canonical single-table question (raw no-skill baseline 1m34s); users reported Opus 5 main sessions much slower than Sonnet 5. 82% of wall was worker spawn/token generation + MCP floors; the session-side remainder was output-generation heavy, which scales worst on Opus. Design doc: vault `Projects/CardoAI Skills/Design - prism-analyst v4.1 Trim.md` (audit: 4 lenses + 10 adversarial verifiers).

1. **Fast path** (new Step 3): simple questions answered by the session directly - no workers. Guardrails: <=4 searches, top_k<=5, >=1 unfiltered search, roster-footing eligibility rule, fail-closed checklist, provenance rule, pre-emit chunk_uuid set equality, mechanical escalation to the worker path.
2. **Wave-3 Reporting conditional**: spawns only when the post-validation union (gaps, uuid-less values, chart values used, unresolved conflicts, sub-TABLE answer-critical values) is non-empty; otherwise the session ABSORBS its duties, with a post-draft re-check. Previously mandatory on every question (measured 1m57s + ~50K tokens to make one score_answer call).
3. **Asset-class gate**: infer-and-state replaces block-on-user. Inference is evidence-gated on get_deal_skill kpi_names/entity_aliases matching exactly one domain set; inferred sets are disclosed on every answer; ask only on zero or 2+ matches. Previously the gate fired every session for any deal whose asset_class was not private_equity/fiber_networks.
4. **list_field_values demoted**: no longer mandatory in Step 1; required before filtered searches and negative existence claims. Never populate doc_types from list_deals (returns [] live).
5. **Validation bounded**: 6-check list, one line each with compared quantities, FAIL-MISSING semantics, session computes from returned rows (worker self-reported pass/fail never accepted - adversarial audit rated worker self-verification UNSAFE).
6. **Opus generation fixes**: domain files pasted verbatim into briefs (no row selection); workers return pre-formatted Working-State sections (merge = append); Wave-3 worker receives the state file PATH, not inlined contents; final draft presented verbatim, never regenerated; deal context cached per session; Step 0 reduced to binary tests; Step 1.5 mechanical.
7. **Contract fix**: Period Comparison "Prior" column now states its basis per row (T-1 / T-1Y / target) instead of a hard-coded T-1Y header.
8. **Working State**: mandatory but write-behind on the fast path (pre-write when band=low, hierarchy-resolved conflicts, or Flagged Data exist); Wave-3 status gains ABSORBED.
9. Removed from SKILL.md: v3 comparison prose, this changelog's previous inline location, the inactive v4.1-candidate scoping note (now active as the fast path), MCP call-count telemetry threading (counts live in the methodology block only). Stripped the v3 agent-prompt templates from prism-tools-reference.md (they contradicted v4: unconditional dual-period search, own output format).

Unchanged (protected): Step 6 section order and flag legend, Sources-table mandate, 3-signal Flagged Data rule, single score_answer band with low-only surfacing, source hierarchy, chart corroborate-or-flag obligation, the two verbatim worker rules, no-fabrication rules.

## 4.0.0 (2026-07-28) - Session-orchestrated lite (differences from v3.1.0)

1. Orchestration moved into the main session: no Opus domain orchestrators, no Haiku sub-agent fan-out; ONE `sonnet` worker per wave (v3: up to 4 Opus + ~9-12 Haiku).
2. Cross-validation by redundant retrieval replaced by the Session Validation Protocol (structural checks + source hierarchy).
3. Wave 1 covers multiple in-scope domains with one combined brief instead of one agent per domain.
4. Explicit per-worker MCP call budgets (10 / 5 / 4+corroboration) and mandatory call-count reporting.
5. Workers never search periods absent from `periods_available` (v3 sub-agent templates mandated dual-period search unconditionally).
6. Chart corroboration explicitly limited to values the answer uses.
7. Working State slimmed (no sub-agent decision tables); maintained by the session only.
8. Scoping table, Step 6 output contract, source hierarchy, flag symbols, and score_answer usage unchanged from v3.1.0.

## 3.1.0 (2026-07-21)

Confidence overhaul (band only, shown only when `low`), per-domain file split (progressive disclosure), asset-class hierarchy (private-equity + fiber sets), asset-class confirmation gate.
