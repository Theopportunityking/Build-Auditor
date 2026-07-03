# The Five Use Cases
### Context file 3 of 3 — read before any audit

These are the five most common AI system types built for SMB clients. Each maps to a primary architecture tier and carries specific failure patterns the auditor must check for.

---

## Use Case 1 — Customer Q&A Agent

**What it does:** Answers customer questions based on the business's internal data — inventory, pricing, services, availability, order status, policies.

**Primary tier:** Tier 1 (Structured SQL / Metadata) for exact factual lookups + Tier 2 (Chunk RAG) for policy and service description questions.

**Routing split:**
- Exact lookups (availability, pricing, order status) → Tier 1
- General questions (turnaround time, what's included, warranty) → Tier 2

**Critical failure modes:**
- Inventory answers based on stale cache (cache refresh interval must be defined)
- Policy answers from outdated documents (version control on SOPs required)
- No graceful failure — system hallucinates when it has no answer

**Who feels it first:** The client's customer. Usually in the form of a wrong price quoted, a product ordered that turns out to be unavailable, or a policy explained incorrectly.

---

## Use Case 2 — Productivity Assistant (Internal)

**What it does:** Helps internal team members complete tasks, find information, draft communications, and reason through decisions.

**Primary tier:** Tier 2 (Chunk RAG) for knowledge retrieval + Tier 4 (Long-Context) for deep reasoning tasks + Tier 1 for structured internal data lookups.

**Routing split:**
- "Find the record for client X" → Tier 1
- "What's our policy on X?" → Tier 2
- "Help me think through this proposal given these documents" → Tier 4

**Critical failure modes:**
- All queries routed through single vector store regardless of type
- Long-context invoked for high-frequency queries without prompt caching
- Internal data accessible beyond appropriate scope (access control)

**Who feels it first:** The internal team member who acts on a wrong answer. May not surface until a client is affected downstream.

---

## Use Case 3 — Internal Training System

**What it does:** Surfaces training materials, answers questions during onboarding, guides users through procedures.

**Primary tier:** Tier 4 (Long-Context with prompt caching) for stable corpora that fit in context window. Tier 2 (Chunk RAG) for large or frequently updated training sets.

**Choose Tier 4 when:** Training materials are stable, the full corpus fits in context window, and query volume is low. Full-context reasoning preserves procedure sequence in a way chunked retrieval does not.

**Choose Tier 2 when:** Corpus is too large, materials update frequently, or query volume may grow.

**Critical failure modes:**
- Procedure steps retrieved out of sequence (especially dangerous in technical or safety contexts)
- Outdated training materials coexisting with current ones
- Long-context at moderate query volume without caching

**Who feels it first:** The trainee or new hire who follows an outdated or incomplete procedure. May not surface until a mistake is made.

---

## Use Case 4 — Scraped Data Retrieval

**What it does:** Answers questions based on information scraped from websites, aggregated feeds, or external content sources.

**Primary tier:** Tier 2 (Chunk RAG) with aggressive preprocessing.

**Preprocessing is non-negotiable:** Scraped content is the noisiest input type in SMB builds. Without preprocessing, navigation menus, cookie banners, repeated headers, and boilerplate legal text pollute the vector store and cause retrieval to return page chrome instead of content.

**Preprocessing checklist before ingestion:**
- Strip all HTML tags and formatting artifacts
- Remove navigation elements, headers, footers, repeated site-wide boilerplate
- Deduplicate content that appears across multiple scraped pages
- Tag content sections by type (product vs. review vs. FAQ vs. legal)
- Chunk by content section, not by character count

**Critical failure modes:**
- Navigation text returned as an answer
- Multiple scraped versions of the same page contaminating results
- Broken pagination causing partial content ingestion

**Who feels it first:** The user who receives a garbled answer that includes menu text, footer links, or legal disclaimers as if they were content.

---

## Use Case 5 — Google Drive / Document Strategic Answers

**What it does:** Synthesizes across file repositories to answer strategic questions — connecting proposals, meeting notes, client history, project plans, and financial documents.

**Primary tier:** Tier 3 (GraphRAG) for genuine relational queries + Tier 2 (Chunk RAG) for single-document lookups.

**Routing split:**
- "Find the proposal for client X" → Tier 2
- "What did we commit to in the proposal vs. what's in the current scope?" → Tier 3

**Confirm relational reasoning is genuinely required before deploying Tier 3.** Many "strategic" queries are actually single-document lookups that Tier 2 handles at a fraction of the cost.

**Critical failure modes:**
- Same entity named differently across documents breaks graph relationships
- Graph built on a stale Drive snapshot (sync schedule must be defined)
- GraphRAG invoked for simple single-document queries (unnecessary cost)
- Drive permissions not reflected in retrieval scope (user sees documents they shouldn't)

**Who feels it first:** The business owner or executive who relies on a strategic answer that stitched together wrong or outdated information across documents.

---

## Use case to tier quick map

| Use case | Primary tier | Secondary tier | Watch for |
|---|---|---|---|
| Customer Q&A | Tier 1 | Tier 2 | Stale inventory, version contamination |
| Productivity assistant | Tier 2 | Tier 1, Tier 4 | Cost at high volume, access control |
| Training system | Tier 4 | Tier 2 | Sequence loss, outdated materials |
| Scraped data | Tier 2 | — | Dirty input, version contamination |
| Google Drive strategy | Tier 3 | Tier 2 | Cost, entity naming, stale sync |

---

## Context phase complete

You now have the background knowledge needed to conduct audits.

**If running a pre-build audit:** Go to `02_pre_build_audit/PHASE_PROMPT.md`
**If running a post-build QA:** Go to `04_post_build_qa/PHASE_PROMPT.md`
**If reviewing architecture:** Go to `05_architecture_guide/routing_architecture.md`
