# Pre-Build Sign-Off
### Confirm before moving to build

Every box must be checked before architecture decisions are finalized.
Any unchecked box is a production failure waiting to happen.

---

## Sign-off checklist

- [ ] Three real user queries are documented (not demo queries — real ones)
- [ ] All data sources are identified and confirmed accessible
- [ ] Any "answers in someone's head" are flagged and extraction plan exists
- [ ] Version change frequency is documented
- [ ] Damage level of wrong answers is assessed and documented
- [ ] Query volume estimate is recorded
- [ ] Cost implications at stated query volume are confirmed acceptable
- [ ] Primary retrieval tier is selected with rationale written down
- [ ] Router is planned if multiple query types exist
- [ ] Voice preprocessing plan exists if voice input is part of the build
- [ ] Platform constraints (if any) are documented with compensating controls

---

## Gate decision

**All boxes checked →** Proceed to build. Architecture decisions are documented.

**Any box unchecked →** Resolve before building. Document what is unresolved and why.

**"Answers in someone's head" unchecked →** Do not proceed to build. Data extraction is Phase 1. Architecture is Phase 2.

---

## Output instruction

Save the completed pre-build audit report to:
`07_output_traces/YYYY-MM-DD_[project-name]_pre-build.md`

Then begin build with architecture decisions documented.
