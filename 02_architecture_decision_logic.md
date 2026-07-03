# Architecture Decision Logic
### Apply after collecting all five diagnostic answers

---

## Decision tree

Work through this in order. Stop at the first match.

```
STEP 1: Are the majority of user queries exact factual lookups?
(inventory, order status, pricing, specific records)

    YES → Primary: Tier 1 (Structured SQL / Metadata)
          Check: Does the build also need policy/FAQ answers?
              YES → Add Tier 2 + Router
              NO  → Tier 1 only

    NO  → Continue to Step 2


STEP 2: Do queries require connecting information across
        multiple documents or relational reasoning?
(strategic synthesis, cross-referencing, entity relationships)

    YES → Check query volume first:
              Under 50/day  → Tier 3 (GraphRAG) — cost acceptable
              50–500/day    → Flag cost to builder, confirm acceptable
              Over 500/day  → Strongly reconsider — recommend Tier 2
                              with explicit limitation documented

    NO  → Continue to Step 3


STEP 3: Does the full knowledge corpus fit in a context window
        AND is query volume under 50/day?

    YES → Tier 4 (Long-Context with prompt caching)
          Confirm: Is prompt caching available on their platform?
              NO  → Flag cost risk, may still be viable at very low volume

    NO  → Continue to Step 4


STEP 4: Default case — unstructured content, moderate volume

    → Tier 2 (Chunk RAG with memory compression)


STEP 5: Does the build handle MULTIPLE query types from different steps above?

    YES → Implement Intent-Classifier Router
          Apply all relevant tiers
          Document routing logic clearly

    NO  → Single tier is sufficient
```

---

## Volume × damage matrix

Use this to flag risk when the recommended tier conflicts with query volume or damage level:

| Change frequency | Damage if wrong | Recommended approach |
|---|---|---|
| Continuous | High | Tier 1 mandatory — no vector search |
| Continuous | Low | Tier 1 preferred — vector only for non-critical queries |
| Regular | High | Tier 1 or Tier 2 with versioning controls mandatory |
| Regular | Low | Tier 2 with version tagging |
| Rarely | High | Tier 2 with version control + manual update process |
| Rarely | Low | Tier 2 standard |

---

## Platform constraint flag

If the builder's platform does not support the recommended tier natively, document this explicitly in the report:

```
PLATFORM CONSTRAINT IDENTIFIED
Recommended tier: [X]
Platform default: [Y]
Mismatch: [describe]
Compensating control: [what the builder should do instead]
Known limitation: [what this means for the build in production]
```

A platform-constrained build is acceptable if limitations are documented. It is not acceptable if limitations are ignored.

---

## After producing the recommendation

Go to `pre_build_signoff.md` and run the sign-off checklist with the builder.
