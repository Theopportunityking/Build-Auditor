# Routing Architecture
### Reference — consult when making tier recommendations

The routing architecture is always the starting point when a build handles more than one query type.

```
                    [ USER / AGENT QUERY ]
                              |
                              v
                 [ Intent-Classifier Router ]
                              |
      +-----------+-----------+-----------+-----------+
      v           v           v           v
[ Tier 1     [ Tier 2     [ Tier 3     [ Tier 4
  Structured   Chunk RAG    GraphRAG ]   Long-Context
  SQL/Meta ]   + Compress]              Caching ]
  Exact facts  Scraped /    Cross-doc   Training /
  Inventory    SOPs/FAQs    reasoning   deep analysis
  Order status Surface ans  Strategy    Onboarding
```

The router can be:
- A prompt-based LLM classification step (most common for SMB builds)
- A rules-based keyword filter (for simpler builds with clear query type separation)
- A trained classifier model (for high-volume, high-variability query sets)

For most SMB builds, a prompt-based LLM classifier is sufficient and easier to maintain.

See individual use case files for tier-to-use-case mapping.
