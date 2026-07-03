# What Is Retrieval Degradation?
### Context file 1 of 3 — read before any audit

---

## The plain-language definition

When you build an AI system that answers questions, the system has to **find** the right information before it can **answer**; this finding process is called retrieval.

**Retrieval degradation** is when the system finds the wrong information, outdated information, or finds information that's close but not quite right — and then answers confidently based on it. The answer sounds correct but it isn't.

---

## Why this matters for SMB AI system builders specifically

Enterprise builders have QA teams, staging environments, and users who can usually identify when something looks wrong. SMB AI system builders and their clients typically have none of these.

When retrieval degrades in a deployment:
- The client's customer gets a wrong answer and loses trust in the business
- The client often doesn't know the answer was wrong — they assume the AI is correct
- The builder often finds out weeks later, usually from a frustrated client

**The builder is responsible for catching this before handoff, but the client cannot.**

---

## When degradation happens

Retrieval degradation almost never surfaces in demos. It surfaces in production because:

- **Demo queries** are written by the builder who knows what's in the system
- **Production queries** come from real users who don't know what the system knows
- The gap between those two query types is where degradation hides

A system can pass every demo test and fail on the first real customer query; this framework closes that gap.

---

## The four structural causes

### 1. Architecture mismatch
The wrong retrieval method is used for the query type.

A vector database is good at finding documents that *sound similar* to a question. It is bad at finding the exact record that answers a specific factual question.

**Example:** A client who manages inventory asks "Is the matte black 3M wrap in stock?" A vector search returns a product description for a similar matte wrap that is in stock — even though the specific product asked about is not. The system answers "yes." The order gets placed. The product doesn't exist in inventory.

### 2. Version contamination
Multiple versions of the same document coexist in the database with no way for the system to know which is current.

**Example:** A 2025 pricing sheet and a 2026 pricing sheet are both in the vector store. A customer asks about pricing. The system blends both into a confident answer. The quoted price is from the old sheet. The client has an uncomfortable conversation.

### 3. Chunk size conflict
Standard retrieval systems break documents into pieces (chunks) before storing them. Small chunks are precise but lose context. Large chunks have context but return too much noise. One chunk size applied everywhere fails some query types systematically.

**Example:** A procedure document is chunked into 100-token pieces for precision. A user asks about step 3 of a 10-step process. The chunk retrieved is accurate but lacks the context of steps 1-2, so the answer is technically correct but practically useless.

### 4. Cost architecture mismatch
The retrieval method chosen is too expensive for the query volume, or the volume grows past what the architecture can sustain.

**Example:** A relational knowledge graph (GraphRAG) is used for a customer-facing chatbot. It works in testing at 5 queries/day. The client launches and handles 300 queries/day. The monthly LLM bill becomes unjustifiable.

---

## What this auditor checks for

Every phase of this framework is designed to catch one or more of these four failure modes before they reach production.

Continue to `four_retrieval_tiers.md` →
