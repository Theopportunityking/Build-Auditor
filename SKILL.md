---
name: smb-ai-build-auditor
description: >
  Use this skill when a builder needs to audit an AI system for retrieval
  degradation before client handoff. Triggers include: "run a pre-build audit",
  "QA this build", "is this ready to ship", "audit my retrieval architecture",
  or any request to evaluate an AI system before delivery to a non-technical
  client. Covers five SMB use case types across four retrieval tiers.
  Platform-agnostic — works regardless of what tools were used to build the system.
---

# SMB AI Build Auditor — Skill Instructions

When this skill is invoked, read `00_entry/AGENT_START_HERE.md` and follow
the navigation instructions from there. The directory structure is the workflow.

Do not skip the context phase (`01_context/`). Do not run tests against
inferred build behavior — ask the builder to run queries live and paste
results back for grading.

Save all audit outputs to `07_output_traces/` using the naming format:
`YYYY-MM-DD_[project-name]_[phase].md`

---

# How to Deploy This as a Claude Code Skill

This section is for anyone who cloned this repo and wants to use it as a
live Claude Code skill — invokable with `/smb-ai-build-auditor` or loaded
automatically when Claude Code detects a relevant task.

---

## What a Claude Code Skill Is

A skill is a reusable workflow you install once and invoke any time. Instead
of re-explaining your QA process in every session, you install the skill and
Claude Code loads the full workflow on demand.

This repo is already structured as a skill. The `SKILL.md` you're reading
right now is the entry point. The numbered folders are the phases Claude Code
navigates automatically.

This is ICM (Interpreted Context Methodology) in action: the directory
structure is the agent's instruction set.

---

## Three Ways to Deploy

### Option 1 — Personal skill (available across all your projects)

Install once. Use everywhere. Best for solopreneur builders who want this
in every project they work on.

```bash
# Create your personal skills directory if it doesn't exist
mkdir -p ~/.claude/skills

# Clone this repo into it
git clone https://github.com/yourusername/smb-ai-build-auditor \
  ~/.claude/skills/smb-ai-build-auditor
```

That's it. Open Claude Code in any project and type:

```
/smb-ai-build-auditor
```

Or just describe what you need — Claude Code will load the skill automatically
when it detects you're asking about QA, retrieval architecture, or client handoff.

---

### Option 2 — Project skill (available only in a specific project)

Best when you want the auditor scoped to one client engagement or repo.

```bash
# From inside your project directory
mkdir -p .claude/skills

git clone https://github.com/yourusername/smb-ai-build-auditor \
  .claude/skills/smb-ai-build-auditor
```

Or if you don't want a nested git repo, copy the files directly:

```bash
mkdir -p .claude/skills/smb-ai-build-auditor
cp -r /path/to/smb-ai-build-auditor/* .claude/skills/smb-ai-build-auditor/
```

---

### Option 3 — Symlink (keep one copy, use it everywhere)

Clone the repo once. Symlink it wherever you need it.
Claude Code follows symlinks and reads SKILL.md from the target directory.

```bash
# Clone to a central location
git clone https://github.com/yourusername/smb-ai-build-auditor \
  ~/ai-tools/smb-ai-build-auditor

# Symlink to personal skills
mkdir -p ~/.claude/skills
ln -s ~/ai-tools/smb-ai-build-auditor \
  ~/.claude/skills/smb-ai-build-auditor
```

---

## How to Invoke It

**Slash command (you trigger it):**
```
/smb-ai-build-auditor
```

**Natural language (Claude Code triggers it automatically):**
```
Run a pre-build audit on this project
QA this build before I hand it off
Is my retrieval architecture right for this use case?
```

**With a specific phase:**
```
/smb-ai-build-auditor run pre-build audit
/smb-ai-build-auditor post-build QA
```

---

## How to Use It With Other LLMs (No Claude Code)

**Any LLM with file access** (ChatGPT with file upload, Gemini, etc.):

Upload the contents of `00_entry/AGENT_START_HERE.md` and say:
```
Follow the instructions in this file.
```

**Claude Project (no file access needed):**

Copy the contents of `00_entry/SYSTEM_PROMPT.md` into your Claude Project
system prompt. Upload your build documentation. Type:
```
Run a pre-build audit
```

**Manual (no LLM at all):**

Work through the numbered folders in order. Every file is plain markdown
written for human readers. The framework works without AI.

---

## Keeping It Updated

```bash
# If installed via git clone
cd ~/.claude/skills/smb-ai-build-auditor
git pull

# Claude Code watches skill directories for file changes —
# updates take effect immediately, no restart needed.
```

---

## What Gets Saved

Audit outputs are saved to `07_output_traces/` inside the skill directory.
The `.gitignore` excludes these files from version control by default —
your client audit records stay local.

If you want to track audit history in a separate private repo, point
`07_output_traces/` at a different directory using a symlink.

---

## The Bigger Picture: Workflow Automation

This skill is a starting point, not an endpoint.

The same ICM pattern — numbered directories, phase prompts, agent navigation
without custom orchestration code — can be applied to any repeatable workflow:

- Client onboarding audits
- Content production pipelines
- System architecture reviews
- Proposal generation workflows

Every workflow you build this way becomes: a Claude Code skill, a GitHub
portfolio piece, and a teaching asset for your community. One build, three
assets. That's the ICM advantage.

---

## About This Project

Built by [Rico / WayMaker Services](https://github.com/yourusername) as a
demonstration of ICM (Interpreted Context Methodology) — a framework for
building agentic AI workflows using filesystem structure as the orchestration
layer, with no custom code required.

The methodology: directories are state machines. Files are instructions.
The agent reads and acts. No framework dependency. No lock-in.
