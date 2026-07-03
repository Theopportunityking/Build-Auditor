# The Four Retrieval Architecture Tiers
### Context file 2 of 3 — read before any audit

---

## The routing architecture

When a build handles more than one query type, the **first thing to build is the router** — not the retrieval layer. The router classifies incoming queries and directs each one to the appropriate tier. Without a router, every query goes through the same retrieval method, which means some query types are systematically underserved.

```
                    [ USER / AGENT QUERY ]
                              │
                              ▼
                 [ Intent-Classifier Router ]
                              │
      ┌─────────────┬─────────┴──────────┬──────────────┐
      ▼             ▼                    ▼              ▼
[ Tier 1       [ Tier 2            [ Tier 3        [ Tier 4
  Structured     Chunk RAG +         GraphRAG ]      Long-Context
  SQL/Meta ]     Compression ]                        Caching ]
  Exact facts    Scraped data /      Cross-doc         Training /
  Inventory      SOPs / FAQs         reasoning         deep analysis
  Order status   Surface answers     Strategy          Onboarding
```

The router can be:
- A prompt-based LLM classification step (most common for SMB builds)
- A lightweight rules-based keyword filter (for simpler builds)
- A trained classifier model (for high-volume, high-variability query sets)

---

## Tier 1 — Structured SQL / Metadata Filtering

**Use when:** the query needs an exact factual answer from a database.

**Best for:** inventory checks, order status, pricing lookups, customer records, appointment availability, any query where "similar" is not acceptable and only "exact" is correct.

**Do not use:** vector/semantic search for these queries. Vector finds documents that sound like the query. Exact lookups need deterministic retrieval.

**Key failure modes:**
- Semantic search returns a similar-but-wrong record
- Null results handled with a hallucinated answer instead of "not found"
- Stale cached data returned for fast-changing information (inventory, pricing)

**Cost profile:** Very low per query. Sustainable at any SMB volume.

---

## Tier 2 — Chunk RAG with Memory Compression

**Use when:** the query needs a surface-level answer from unstructured content.

**Best for:** FAQs, SOPs, policy documents, product descriptions, scraped web content, any question answerable from a single passage of documentation.

**Preprocessing is mandatory:** Scraped and unstructured content must be cleaned before ingestion. HTML noise, navigation elements, repeated headers, and boilerplate text pollute vector scores and cause retrieval to return page chrome instead of content.

**Key failure modes:**
- Chunk size too small: precise retrieval but no context for the answer
- Chunk size too large: context preserved but too much noise in the retrieved passage
- Version contamination: old and new document versions coexist, blended into wrong answers
- Dirty input: navigation menus, cookie banners, and footers retrieved as content

**Configuration notes:**
- Store a compressed summary alongside chunk vectors for documents longer than 500 words
- Set a minimum relevance threshold — results below it should not be returned
- Consider a reranking step for builds where precision matters more than recall

**Cost profile:** Low per query. Sustainable at high SMB volume.

---

## Tier 3 — GraphRAG (Knowledge Graph)

**Use when:** the query requires connecting information across multiple documents.

**Best for:** strategic synthesis, cross-referencing historical records, entity relationship mapping, multi-hop reasoning ("what did we promise client A in Q1, and does the current project scope deliver on that?").

**Do not use:** where Tier 2 would suffice. GraphRAG is 3–5× more expensive than standard RAG. Confirm that relational reasoning is genuinely required before deploying this tier.

**Key failure modes:**
- Used for single-document queries, tripling cost with no accuracy benefit
- Same entity named differently across documents (Client Alpha / Alpha Inc / AP2026) breaks graph relationships
- Stale graph from outdated document sync
- Fabricated relationships when graph doesn't contain the connection being queried

**Cost profile:** High. Calculate: (expected daily queries × cost per query × 30) before recommending for SMB clients.

---

## Tier 4 — Long-Context Prompt Caching

**Use when:** the full knowledge corpus fits in a context window AND query volume is low.

**Best for:** training materials, onboarding guides, deep analytical reasoning over a stable document set.

**Why it works for training:** Training materials benefit from the model having full context of the entire guide, not just the most semantically similar chunk. A user asking "what comes after the prep step?" needs the model to understand the full procedure sequence — something chunk retrieval frequently loses.

**Key failure modes:**
- Deployed at high volume without prompt caching (cost spikes unsustainably)
- Corpus exceeds context window (silent truncation — model answers from partial information)
- Document updated but long-context corpus not refreshed (stale answers)

**When to switch to Tier 2 instead:**
- Corpus is too large for context window
- Materials update frequently
- Query volume is growing beyond low-volume threshold

**Cost profile:** Low at low volume with prompt caching enabled. Unsustainable at high volume without caching.

---

## Quick reference

| Query type | Tier | Never use |
|---|---|---|
| Exact record lookup (inventory, status, pricing) | 1 | Vector search |
| Policy or procedure question | 2 | — |
| FAQ or product description | 2 | — |
| Scraped web content | 2 | — |
| Cross-document synthesis | 3 | — |
| Strategic analysis across files | 3 | — |
| Full training guide | 4 | — |
| Onboarding deep-dive | 4 | — |
| Multiple query types | Router + all applicable tiers | Single-tier for everything |

---

Continue to `five_smb_use_cases.md` →
