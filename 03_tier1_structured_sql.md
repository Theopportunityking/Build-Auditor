# Tier 1 Checklist — Structured SQL / Metadata Filtering

- [ ] No semantic search for exact lookups — queries route to structured DB or deterministic API calls
- [ ] Metadata tags defined — records have explicit IDs, dates, status flags for filtering
- [ ] Text-to-SQL or filter queries validated — if generated dynamically, validation layer prevents malformed queries
- [ ] Null result handling defined — system says "not found" clearly, does not substitute a similar record
- [ ] Real-time vs. cached data decided — if fast-changing data, cache refresh interval is defined and client knows it
