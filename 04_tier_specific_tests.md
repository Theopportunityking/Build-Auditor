# Tier-Specific Tests
### Run only the sections that apply to this build

---

## Tier 1 — Structured / Exact Lookup Tests

**Test 2.1 — Exact record retrieval**
Generate a query asking for a specific record by ID, name, or identifier.
Expected: exact match returned.

**Test 2.2 — Near-miss query**
Generate a query using a description that sounds like, but is not, a correct record.
Expected: system does NOT return a similar record as if it were the right one.

**Test 2.3 — Null result**
Generate a query for something that does not exist in the database.
Expected: clear "not found" — no substitution, no hallucination.

**Section grade:** All Pass → 🟢 | Any Flag → 🟡 | Any Fail → 🔴

---

## Tier 2 — Chunk RAG Tests

**Test 2.4 — Factual surface query**
Generate a direct question answerable by a single passage in the knowledge base.
Expected: specific accurate answer, appropriately scoped.

**Test 2.5 — Version contamination test** (only if multiple doc versions exist)
Generate a question whose answer changed between document versions.
Expected: current version answer returned.

**Test 2.6 — Noise resistance test**
Generate a question where the answer is in a document with heavy surrounding noise (headers, navigation, boilerplate).
Expected: content-based answer — no chrome or boilerplate in response.

**Section grade:** All Pass → 🟢 | Any Flag → 🟡 | Any Fail → 🔴

---

## Tier 3 — GraphRAG Tests

**Test 2.7 — Multi-document synthesis**
Generate a question requiring information from at least two separate documents.
Expected: synthesized answer that draws from multiple sources.

**Test 2.8 — Entity relationship query**
Generate a question about the relationship between two named entities in the knowledge graph.
Expected: relationship correctly identified.

**Test 2.9 — Non-existent relationship**
Generate a question about a relationship between two entities that does NOT exist in the graph.
Expected: system does not fabricate a connection.

**Section grade:** All Pass → 🟢 | Any Flag → 🟡 | Any Fail → 🔴

---

## Tier 4 — Long-Context Tests

**Test 2.10 — Deep synthesis query**
Generate a question requiring synthesis across the full document — not just retrieval of a single passage.
Expected: answer that demonstrates full-document comprehension.

**Test 2.11 — Late-document query**
Generate a question whose answer appears near the end of the document corpus.
Expected: system retrieves from end of document, not just beginning (confirms full context window coverage).

**Section grade:** All Pass → 🟢 | Any Flag → 🟡 | Any Fail → 🔴

---

## Voice Preprocessing Tests (if applicable)

**Test 2.12 — Transcription quality**
Ask the builder to submit a voice query using real user speech patterns and vocabulary. Review the transcription for errors.
Expected: transcription accurate enough to form a valid retrieval query.

**Test 2.13 — End-to-end pipeline**
Ask the builder to test the full chain: voice → transcription → query → retrieval → answer.
Expected: correct answer returned from a voice-initiated query.

**Section grade:** All Pass → 🟢 | Any Flag → 🟡 | Any Fail → 🔴

---

Continue to `failure_behavior_tests.md` →
