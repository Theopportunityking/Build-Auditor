# Failure Behavior Tests
### Run for every build — these test what happens when things go wrong

---

## Test 3.1 — Ambiguous query

Generate a question that could reasonably mean two different things.

Expected behavior: The system asks for clarification OR explicitly acknowledges the ambiguity before answering.

Fail behavior: The system picks one interpretation and answers confidently without flagging the ambiguity.

---

## Test 3.2 — Retrieval failure

Generate a question about a topic the system has no information about whatsoever.

Expected behavior: "I don't have information on that" plus a redirect (contact the business, check their website, etc.)

Fail behavior: The system hallucinates an answer. Even a confident "I'm not sure but..." followed by fabricated content is a Fail.

---

## Test 3.3 — Contradictory data (run only if contradictions exist in data sources)

If any data sources contain conflicting information (two documents making different claims about the same thing), generate a question that would surface the contradiction.

Expected behavior: System flags the conflict, cites the most current source, or asks for clarification.

Fail behavior: System blends both sources into a confident single answer that is partially wrong.

---

## Grading failure behavior section

- All Pass → 🟢 Green
- Test 3.1 fails → 🟡 Yellow (ambiguity is a usability issue, not a safety issue)
- Test 3.2 fails → 🔴 Red (hallucination on unknown topics is a trust and liability issue)
- Test 3.3 fails → 🔴 Red (contradictory data returning as confident answer is a reliability failure)

---

Continue to `cost_validation.md` →
