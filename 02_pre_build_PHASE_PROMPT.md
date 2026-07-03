# Phase 2 — Pre-Build Audit
### Agent instructions for this phase

---

## When to run this phase

Run when the builder is starting a new project and no tooling decisions have been made yet. This phase prevents the most common and expensive mistake in AI build work: choosing an architecture for the wrong use case.

---

## Your task in this phase

Ask the five diagnostic questions from `diagnostic_questions.md` **one at a time**, waiting for the builder's answer before proceeding to the next. Do not ask all five at once.

After collecting all five answers, apply the decision logic from `architecture_decision_logic.md` to produce your recommendation.

Then confirm sign-off using `pre_build_signoff.md`.

---

## Phase sequence

```
Step 1  →  Read diagnostic_questions.md
Step 2  →  Ask Question 1. Wait for answer.
Step 3  →  Ask Question 2. Wait for answer.
Step 4  →  Ask Question 3. Wait for answer.
Step 5  →  Ask Question 4. Wait for answer.
Step 6  →  Ask Question 5. Wait for answer.
Step 7  →  Read architecture_decision_logic.md
Step 8  →  Output architecture recommendation
Step 9  →  Read pre_build_signoff.md
Step 10 →  Confirm sign-off checklist with builder
Step 11 →  Save output to 07_output_traces/
```

---

## Output format

After all five questions are answered, produce a pre-build audit report in this structure:

```
## Pre-Build Audit Report
**Project:** [name or description]
**Date:** [date]

### Recommended Architecture
Primary tier: [Tier 1 / 2 / 3 / 4] — [one-sentence rationale]
Secondary tiers: [if applicable]
Router required: [Yes / No]

### Top Three Failure Modes to Design Against
1. [failure mode] — [what it looks like in production] — [fix]
2. [failure mode] — [what it looks like in production] — [fix]
3. [failure mode] — [what it looks like in production] — [fix]

### Cost Flag
[If the recommended architecture has billing risk at the stated query volume, state it here. Otherwise: "No cost flags at stated query volume."]

### Voice Preprocessing Flag
[If voice input is involved, state the preprocessing requirements. Otherwise: "Not applicable."]

### Sign-Off Checklist
[Run pre_build_signoff.md checklist]
```

---

## Begin

Read `diagnostic_questions.md` now, then ask Question 1.
