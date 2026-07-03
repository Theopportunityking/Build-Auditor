# Handoff Documentation Check
### The last gate before delivery

---

## Check 5.1 — Client knows what it does AND doesn't do

The client has been told:
- [ ] What questions the system is designed to answer
- [ ] What questions it will decline or redirect
- [ ] What a wrong answer looks like and that they should report it

---

## Check 5.2 — Wrong answer process is defined

The client knows:
- [ ] Who to contact when something seems wrong
- [ ] How to report an issue (not just "tell the builder")
- [ ] What happens next when they report one

---

## Check 5.3 — Known limitations are in writing

Any limitations identified in QA are:
- [ ] Documented in writing — not just mentioned verbally
- [ ] Acknowledged by the client before go-live
- [ ] Scheduled for resolution if they are Yellow-level flags

---

## Check 5.4 — Maintenance is defined

If builder maintains the system:
- [ ] Schedule and scope of maintenance is in writing
- [ ] How data updates are handled is documented
- [ ] Client knows what triggers a maintenance request

If client self-maintains:
- [ ] Client has been trained on the update process
- [ ] Documentation exists for them to reference
- [ ] Client has demonstrated understanding (not just acknowledged)

---

## Grading

- All checked → 🟢 Green
- 1–2 unchecked, non-critical → 🟡 Yellow (resolve within first week post-launch)
- Client doesn't know what to do when it breaks → 🔴 Red
- Known limitations not documented → 🔴 Red

---

## After completing all sections

Produce the overall QA report using the format in PHASE_PROMPT.md and save to:
`07_output_traces/YYYY-MM-DD_[project-name]_post-build-qa.md`
