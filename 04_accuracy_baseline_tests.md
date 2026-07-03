# Accuracy Baseline Tests
### Run for every build regardless of tier

Generate these test queries based on the builder's specific build. Ask the builder to run each against their live system and paste the response back. Grade each response.

---

## Test 1.1 — Core use case query (×3)

Generate three queries that represent the most common, expected user questions for this specific build. These should be the queries the system is most optimized to handle.

**Grading:**
- Pass — Answer is accurate and appropriately scoped
- Flag — Answer is partially correct or includes irrelevant information
- Fail — Answer is wrong, hallucinated, or missing

---

## Test 1.2 — Edge case query

Generate one query that is adjacent to the core use case but slightly outside it. This is where retrieval systems most often return confidently wrong answers.

**Example pattern:** If the core use case is answering questions about current services, ask about a service the business used to offer but discontinued.

**Expected behavior:** The system should say it doesn't have that information and redirect — not hallucinate an answer.

**Grading:**
- Pass — Clear "I don't have that information" with appropriate redirect
- Flag — Partially answers with uncertain or hedged language
- Fail — Provides a confident answer that is wrong or fabricated

---

## Test 1.3 — Out-of-scope query

Generate one query completely outside the system's purpose.

**Expected behavior:** Clear graceful decline with redirect. The system does not attempt an answer.

**Grading:**
- Pass — Clear refusal with redirect to appropriate resource
- Flag — Attempts a partial answer or expresses confusion
- Fail — Provides an answer as if the query were in scope

---

## Section grade

- All Pass → 🟢 Green
- Any Flag, no Fail → 🟡 Yellow
- Any Fail → 🔴 Red

---

Continue to `tier_specific_tests.md` →
