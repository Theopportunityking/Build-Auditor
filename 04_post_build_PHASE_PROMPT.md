# Phase 4 — Post-Build QA
### Agent instructions for this phase

---

## When to run this phase

Run before every client handoff. No exceptions.

This is the last gate between the build and the client. It is designed to surface failure modes that testing never catches — the queries real users ask that demo queries don't cover.

---

## What you need from the builder before starting

Ask the builder to provide:
1. A description of the completed build (what it does, what data sources it uses)
2. The primary retrieval tier(s) used
3. Any sample queries they tested during development
4. Any known edge cases or limitations they've already identified

If the builder does not know the retrieval tier used, help them identify it from the build description before proceeding.

---

## Phase sequence

```
Step 1  →  Collect build description from builder
Step 2  →  Identify which tiers are present in the build
Step 3  →  Run accuracy_baseline_tests.md (all builds)
Step 4  →  Run tier_specific_tests.md (applicable tiers only)
Step 5  →  Run failure_behavior_tests.md (all builds)
Step 6  →  Run cost_validation.md (all builds)
Step 7  →  Run handoff_documentation.md (all builds)
Step 8  →  Produce overall health grade
Step 9  →  Save output to 07_output_traces/
```

---

## How to run tests

For each test, generate the test query and ask the builder to:
1. Run it against their live deployed build
2. Paste the exact response back to you
3. You grade the response using the criteria in each test file

**You grade from the actual response the builder pastes. Not from your inference about what the build might return.**

---

## Overall health grading rules

🟢 **Green — Production ready**
All tier checks pass. Test queries return accurate, appropriately scoped answers. Failure scenarios handled gracefully. Cost validated.

🟡 **Yellow — Conditional**
No critical failures, but at least one Flag-level item. Document the flag, communicate it to client as known limitation, establish monitoring schedule.

🔴 **Red — Do not hand off**
At least one Fail-level item. Resolve before delivery.

**Never grade Green without a documented test suite. A build with no tests is always 🟡 minimum.**

---

## Output format

```
## Post-Build QA Report
**Project:** [name or description]
**Date:** [date]
**Build description:** [one paragraph summary]
**Tiers present:** [list]

### Section Results
| Section | Grade |
|---|---|
| Accuracy baseline | 🟢 / 🟡 / 🔴 |
| Tier-specific tests | 🟢 / 🟡 / 🔴 |
| Failure behavior | 🟢 / 🟡 / 🔴 |
| Cost validation | 🟢 / 🟡 / 🔴 |
| Handoff documentation | 🟢 / 🟡 / 🔴 |
| **Overall** | 🟢 / 🟡 / 🔴 |

### Findings
[For each Flag or Fail item:]
**[Finding name]**
- What it looks like in production: [description]
- Who notices it first: [client / client's customer / builder]
- Fix: [specific remediation step]

### Test Queries for Builder to Run Before Handoff
1. [query tailored to this specific build]
2. [query tailored to this specific build]
3. [query tailored to this specific build]

### Handoff Recommendation
[Proceed / Proceed with documented limitations / Do not proceed]
```

---

## Begin

Ask the builder to describe the completed build, then read `accuracy_baseline_tests.md`.
