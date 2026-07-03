# AI Build Auditor
### A platform-agnostic QA framework built on ICM (Interpreted Context Methodology)

---

## How to use this repo with any LLM

This repository is structured using **ICM — Interpreted Context Methodology**.

That means the **directory structure is the agent's instruction set**. Each folder is a phase. Each file inside it is a step. The LLM reads the folders in sequence and knows exactly what to do next — no custom code required.

### To start an audit session in Claude Code (or any LLM with file access):

```
Read the file at 00_entry/AGENT_START_HERE.md and follow the instructions.
```

That single prompt is enough. The agent will navigate the rest.

### To use as a Claude Project (no file access needed):

1. Copy the contents of `00_entry/SYSTEM_PROMPT.md` into your Claude Project system prompt
2. Upload the documents you want audited
3. Type: `Run a pre-build audit` or `Run a post-build QA`

### To use manually (human-run checklist):

Work through the numbered folders in sequence. Each folder contains plain-language protocols any builder can follow without an LLM.

---

## What this framework does

Most AI builds don't break during the demo. They break two weeks after delivery, when a real user asks a question the demo never covered.

This framework is a QA layer that lives **between the builder and the client** — catching retrieval architecture problems before they become production 
failures.

It is designed for builders who:
- Ship across multiple platforms (n8n, Make, Airtable, MCP, direct API — whatever the use case demands)
- Work with non-technical clients who cannot identify a hallucination on their own
- Need a repeatable process that travels with them regardless of tooling

---

## Directory map

```
smb-ai-qa-icm/
│
├── 00_entry/                    ← Start here (agent reads this first)
│   ├── AGENT_START_HERE.md      ← Primary navigation file for LLM agents
│   └── SYSTEM_PROMPT.md         ← For Claude Project / chat-based use
│
├── 01_context/                  ← Background the agent needs before auditing
│   ├── what_is_retrieval_degradation.md
│   ├── four_retrieval_tiers.md
│   └── five_smb_use_cases.md
│
├── 02_pre_build_audit/          ← Run before any tooling decisions
│   ├── PHASE_PROMPT.md          ← Agent instructions for this phase
│   ├── diagnostic_questions.md
│   ├── architecture_decision_logic.md
│   └── pre_build_signoff.md
│
├── 03_build_quality/            ← Run during active development
│   ├── PHASE_PROMPT.md
│   ├── universal_checks.md
│   ├── tier1_structured_sql.md
│   ├── tier2_chunk_rag.md
│   ├── tier3_graphrag.md
│   ├── tier4_long_context.md
│   └── voice_preprocessing.md
│
├── 04_post_build_qa/            ← Run before every client handoff
│   ├── PHASE_PROMPT.md
│   ├── accuracy_baseline_tests.md
│   ├── tier_specific_tests.md
│   ├── failure_behavior_tests.md
│   ├── cost_validation.md
│   └── handoff_documentation.md
│
├── 05_architecture_guide/       ← Reference — use case to tier mapping
│   ├── routing_architecture.md
│   ├── use_case_1_customer_qa.md
│   ├── use_case_2_productivity_assistant.md
│   ├── use_case_3_training_system.md
│   ├── use_case_4_scraped_data.md
│   └── use_case_5_google_drive.md
│
├── 06_example_audits/           ← Real-world audit walkthroughs
│   └── automotive_specialty_services.md
│
└── 07_output_traces/            ← Audit results get saved here
    └── .gitkeep
```

---

## Why ICM structure

In a standard repository, an LLM agent has to infer what to do from scattered documentation. In an ICM-structured repository, the **file tree is the workflow**. The agent reads the entry point, follows numbered phases, and produces outputs — without needing a custom orchestration layer.

This repo is itself a demonstration of ICM in practice.


---

## Origin

Built from a real engagement audit — an automotive specialty services business where the AI integration plan looked clean on paper but the underlying data flows were too fragmented to support reliable retrieval. The audit caught it before deployment. That experience made the need for this framework clear.

See `06_example_audits/automotive_specialty_services.md` for the full walkthrough.

---

## License

MIT — use it, fork it, improve it.
