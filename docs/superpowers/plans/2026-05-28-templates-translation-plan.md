# Templates and Skills Translation (CN -> EN) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Translate all configurations, sub-agent behaviors, and communication style instructions from `templates/cn/` to `templates/en/` and remove obsolete `.en` suffix from filenames for nesting consistency.

**Architecture:** A file-by-file translation and directory restructure approach: clean up `.en` suffixes, translation of markdown and TOML formats, rewrite table layout specifications, and verify consistency.

**Tech Stack:** TOML config format, Markdown.

---

### Task 1: Cleanup Obsolete Suffix Files

**Files:**
- Delete: `templates/en/AGENTS.template.en.md`
- Delete: `templates/en/config.template.en.toml`

- [ ] **Step 1: Verify file existence and delete them**

Run commands to remove the deprecated files:
```bash
rm templates/en/AGENTS.template.en.md
rm templates/en/config.template.en.toml
```

- [ ] **Step 2: Verify deletion**

Run `git status` to ensure they are listed as deleted.

---

### Task 2: Translate and Sync AGENTS.template.md

**Files:**
- Create: `templates/en/AGENTS.template.md`
- Source: `templates/cn/AGENTS.template.md`

- [ ] **Step 1: Translate the Chinese content into English**
Translate all 5 basic principles, quality standards, dangerous operations confirmation template, and response guidelines. Ensure formatting and markdown blocks are preserved.

- [ ] **Step 2: Write implementation**
Create and write the translated content into `templates/en/AGENTS.template.md`.

- [ ] **Step 3: Verify no untranslated Chinese characters left**
Inspect the written file.

---

### Task 3: Translate and Sync config.template.toml

**Files:**
- Create: `templates/en/config.template.toml`
- Source: `templates/cn/config.template.toml`

- [ ] **Step 1: Translate all descriptions and instruction strings**
Translate `developer_instructions`, descriptions for explorer and worker sub-agents, and model reasoning effort explanations. Keep TOML syntax intact.

- [ ] **Step 2: Write implementation**
Create and write the translated content into `templates/en/config.template.toml`.

- [ ] **Step 3: Verify syntax**
Verify that the TOML syntax is completely valid.

---

### Task 4: Sync and Translate Sub-agent Configs (explorer & worker)

**Files:**
- Modify: `templates/en/agents/explorer.toml`
- Modify: `templates/en/agents/worker.toml`
- Source: `templates/cn/agents/explorer.toml` & `templates/cn/agents/worker.toml`

- [ ] **Step 1: Translate and modify explorer.toml**
Ensure `name = "explorer"`, translate and insert the `description` field, and sync the `developer_instructions`.

- [ ] **Step 2: Translate and modify worker.toml**
Ensure `name = "worker"`, translate and insert the `description` field, sync the `developer_instructions`, and preserve the handover protocol templates.

- [ ] **Step 3: Verify syntax**
Ensure both explorer.toml and worker.toml are valid TOML configurations.

---

### Task 5: Translate and Align terminal-dialog-style SKILL.md

**Files:**
- Modify: `templates/en/skills/terminal-dialog-style/SKILL.md`
- Source: `templates/cn/skills/terminal-dialog-style/SKILL.md`

- [ ] **Step 1: Completely rewrite Table Design specification in English**
Align with the latest Chinese version: CLI natively supports Markdown tables, prohibit handwritten ASCII borders (`+---+`). Change all "Prohibit Markdown Table Syntax" into "Prohibit ASCII Table borders, embrace native Markdown tables".

- [ ] **Step 2: Translate all instructions and output examples**
Translate the three output examples precisely into English. Replace `#` and `##` with bolded groupings in conversational samples.

- [ ] **Step 3: Write implementation**
Write the newly aligned translation into `templates/en/skills/terminal-dialog-style/SKILL.md`.

---

### Task 6: Final Verification

- [ ] **Step 1: Git status and diff check**
Run `git status` to verify files are in correct places and names.

- [ ] **Step 2: Final sanity check on Chinese presence**
Verify that there are no leftover Chinese descriptions inside the English template files.
