# Tier 4 Checklist — Long-Context Prompt Caching

- [ ] Corpus fits in context window — total document set confirmed within LLM provider limit with margin
- [ ] Prompt caching enabled — configured with LLM provider if same corpus used across multiple queries
- [ ] Query volume is low — if volume may grow, migration plan to Tier 2 is defined
- [ ] Document update process defined — when source documents change, process for updating context is documented
- [ ] Reasoning depth validated — tested with questions requiring full-document synthesis, not just passage retrieval
