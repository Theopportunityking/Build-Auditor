# Tier 3 Checklist — GraphRAG / Knowledge Graph

- [ ] Relational reasoning confirmed as genuinely required — not just "it seemed like a good idea"
- [ ] Entity extraction validated — entities correctly identified and consistently tagged across all documents
- [ ] Graph relationships explicitly defined by builder — not inferred by system
- [ ] Query volume cost confirmed acceptable — (daily queries x cost per query x 30) calculated and acceptable
- [ ] Fallback defined — if multi-hop query fails to resolve, system responds gracefully rather than fabricating
- [ ] Entity naming consistency verified — same entity not named differently across source documents
