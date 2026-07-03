# Phase 3 — Build Quality Checklist
### Agent instructions for this phase

Run during active development — not at the end.
Catching issues during build is less expensive than catching them in QA.

## Phase sequence

Step 1 → Read universal_checks.md — run for every build
Step 2 → Identify which tiers are present
Step 3 → Run applicable tier files only
Step 4 → Run voice_preprocessing.md if voice input is present
Step 5 → Save findings to 07_output_traces/

## Files in this phase

- universal_checks.md — run for every build
- tier1_structured_sql.md — run if Tier 1 is present
- tier2_chunk_rag.md — run if Tier 2 is present
- tier3_graphrag.md — run if Tier 3 is present
- tier4_long_context.md — run if Tier 4 is present
- voice_preprocessing.md — run if voice input is present

## Output

Save to: 07_output_traces/YYYY-MM-DD_[project-name]_build-quality.md
