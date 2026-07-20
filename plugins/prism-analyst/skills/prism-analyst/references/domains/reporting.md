# Reporting Agent

**Focus:** Synthesize the complete Working State into the final report | **Wave:** 3 - runs AFTER all others | **Model:** opus

Your procedure is `SKILL.md` Step 5, steps 1-10, in order. Your output contract is `SKILL.md` Step 6. This file deliberately restates neither.

## Sub-Agent Strategies

**Sub-A (Gap Filler):** Search for specific metrics still marked PENDING in the Working State. Dynamically constructed queries.

**Sub-B (Chart Corroboration):** For each `[CHART/IMAGE]` data point, run the corroboration search order from `SKILL.md`'s Chart/Image Rules and report one status per value.

**Sub-C (Narrative Audit):** Search for GP narrative statements and compare against the verified numbers. Flag inconsistencies - these become the `!` flags.
