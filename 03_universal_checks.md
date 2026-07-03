# Universal Checks
### Run for every build regardless of tier

- [ ] Intent is routed correctly — if build handles more than one query type, an explicit routing layer exists
- [ ] All data sources are documented — who owns them, how often they change
- [ ] Version control is addressed — no old and new document versions coexisting without resolution
- [ ] Failure behavior is defined — system says "I don't know" instead of hallucinating when retrieval fails
- [ ] A test query set exists — minimum 10 queries covering real use case, not just demo scenario
- [ ] Client handoff is not the first real test — builder has run realistic queries before client sees it

Any unchecked item = open issue to resolve before post-build QA.
