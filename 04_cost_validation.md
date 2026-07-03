# Cost Validation
### Run for every build — this does not require running test queries

---

## Step 4.1 — Calculate monthly cost estimate

Ask the builder to provide or estimate:
- Which architecture tiers are active in the build
- Approximate cost per query for each tier
- Expected daily query volume

Calculate: (cost per query) × (daily queries) × 30 = monthly estimate

Document the result:

| Tier used | Cost per query (approx) | Daily queries | Monthly estimate |
|---|---|---|---|
| | | | |
| | | | |
| **Total** | | | **$XX/month** |

---

## Step 4.2 — Validate against client budget

Is the monthly cost estimate:
- Within the client's operational budget? 
- Additive to any platform fees they're already paying?
- Disclosed to the client in writing?

---

## Step 4.3 — Volume growth flag

If the build is customer-facing, query volume may grow after launch. Ask:
"If this build handles 3× the expected daily queries six months after launch, is the cost architecture still sustainable?"

If the answer is No, flag the architecture for a scaling review and document the threshold at which cost becomes problematic.

---

## Grading

- Cost acceptable, disclosed, growth-validated → 🟢 Green
- Cost acceptable but not yet disclosed to client → 🟡 Yellow
- Cost problematic at expected or growth volume → 🔴 Red
- Cost not calculated at all → 🟡 Yellow minimum

---

Continue to `handoff_documentation.md` →
