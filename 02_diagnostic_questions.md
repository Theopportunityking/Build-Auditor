# Diagnostic Questions
### Five questions that determine the correct architecture tier

Ask these ONE AT A TIME. Wait for the builder's answer before proceeding.

---

## Question 1 — What will users actually ask?

**Ask the builder:**
"What specific questions will end users ask this system most often? Give me three real examples — not what the AI will 'do,' but what a real user will actually type or say."

**Why this matters:**
The query type determines the architecture. You cannot make the right architecture decision without knowing the real queries.

**Red flag:** If the builder cannot produce three concrete user questions, the use case is not defined enough to build. Stop here and help them clarify scope before proceeding.

**What different answers signal:**

| If users ask things like... | Points toward |
|---|---|
| "Is the blue F-250 wrap available?" / "What's the price for X?" | Tier 1 — Structured SQL |
| "What's your turnaround time?" / "What does the warranty cover?" | Tier 2 — Chunk RAG |
| "What did we decide in last quarter's review?" / "How does project A relate to client B?" | Tier 3 — GraphRAG |
| "Walk me through the full onboarding checklist" / "Explain the entire prep procedure" | Tier 4 — Long-Context |
| Mix of the above | Router + multiple tiers |

---

## Question 2 — Where does the information live?

**Ask the builder:**
"Where does the information that answers those questions currently live? Be specific — a database, documents, a website, someone's head, or some combination?"

**Options to listen for:**
- Structured database (CRM, inventory system, spreadsheet with defined columns)
- Documents (PDFs, Word docs, Google Docs, SOPs)
- Website or scraped content
- File repository (Google Drive, Dropbox, SharePoint)
- Tacit knowledge (in someone's head, undocumented)
- Combination

**Why this matters:**
If the answer lives in a structured database, semantic vector search is the wrong retrieval method regardless of platform defaults. If the answer lives in someone's head, no retrieval system works until that knowledge is captured first — this is a data problem, not an architecture problem.

**Red flag:** More than 20% of the use case answers live in someone's head. Document extraction (including voice-centered extraction for non-technical operators) must happen before architecture is designed. Flag this explicitly.

---

## Question 3 — How often does the information change?

**Ask the builder:**
"How often does that information change? And: does outdated information create a compliance, liability, or serious trust problem for this client?"

**Change frequency options:**
- Rarely (annual policy updates, stable SOPs)
- Regularly (monthly pricing, weekly inventory)
- Continuously (real-time stock, live order status)
- Unpredictably (changes with business events)

**Damage level options:**
- High — wrong answer damages client relationship or creates liability
- Low — wrong answer is inconvenient but recoverable

**Why this matters:**
High-change data in a flat vector database creates version contamination. The higher the change frequency AND the higher the damage of a wrong answer, the more important structured retrieval with versioning controls becomes over semantic search.

**Red flag:** Continuously-changing data + high damage + flat vector database = guaranteed production failure. Do not proceed without a version control solution named.

---

## Question 4 — What is the query volume?

**Ask the builder:**
"Roughly how many queries will this system handle per day? Give me your best estimate: under 50, 50 to 500, or over 500."

**Why this matters:**
Cost architecture must match query volume. Long-context processing at high volume becomes unsustainable. GraphRAG at high SMB volume is typically financially unjustifiable.

**Volume × cost reference:**

| Tier | Approximate cost per query | Sustainable at 500+/day? |
|---|---|---|
| Tier 1 — Structured SQL | Very low | Yes |
| Tier 2 — Chunk RAG | Low | Yes |
| Tier 3 — GraphRAG | High (3–5× RAG) | Rarely for SMB |
| Tier 4 — Long-context, no caching | Medium-High | No |
| Tier 4 — Long-context, with caching | Low-Medium | Often yes |

**Red flag:** GraphRAG or uncached long-context recommended for a system expecting 500+ daily queries. Flag before proceeding.

---

## Question 5 — Text, voice, or both?

**Ask the builder:**
"Will users interact with this system via text, voice, or both?"

**If voice is involved, follow up with:**
- "Will transcription happen in real time or from recorded audio?"
- "Does speaker identity matter — who said something, not just what was said?"
- "Does sequence or timing matter — step 3 of a process, not just the fact?"

**Why this matters:**
Voice input adds a preprocessing layer before retrieval begins. Poor transcription quality degrades retrieval precision downstream. Temporal and speaker context, if relevant, requires chunking strategies that flat vector stores do not support by default.

**Red flag:** Voice input feeding directly into a standard RAG pipeline without a transcription quality check or context-preservation step.

---

## After all five answers are collected

Go to `architecture_decision_logic.md` and apply the decision framework to produce your recommendation.
