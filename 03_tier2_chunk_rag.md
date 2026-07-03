# Tier 2 Checklist — Chunk RAG with Memory Compression

- [ ] Input preprocessed before ingestion — HTML, navigation, footers, boilerplate stripped
- [ ] Chunk size is intentional — specific size chosen for specific reason, not platform default, documented
- [ ] Summaries stored alongside chunks — for documents over 500 words, compressed summary attached to chunk vectors
- [ ] Version contamination addressed — old and new document versions cannot coexist without version tagging
- [ ] Relevance threshold set — results below minimum similarity score are not returned
- [ ] Reranking considered — if precision matters more than recall, reranking step evaluated
