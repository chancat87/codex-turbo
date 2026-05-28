# Specification: Templates and Skills Translation (CN -> EN)

This document specifies the plan to translate and sync templates from `templates/cn/` into `templates/en/` within the `codex-turbo` repository, complying with the user's decision to drop the `.en` suffix from filenames for cleaner structure.

## Goal Description

The goals of this translation are:
1. Translate all Chinese-specific instruction sets, configurations, sub-agent behaviors, and communication style specifications into precise English.
2. Synchronize English sub-agents config options (`name` and `description` sections) which were missing in old EN files.
3. Bring the terminal output layout guidelines in the English version of the `terminal-dialog-style` Skill up to date. The old English version restricted tables to handwritten ASCII formatting; we will synchronize it to the modern Chinese version which permits Markdown tables (native terminal rendering support) and bans manual ASCII borders (`+---+`).
4. Reorganize directory structures: Remove unnecessary `.en` filename suffixes in `templates/en` and keep it identical to `templates/cn/`.

---

## Proposed Changes

We will perform file deletions, creations, and updates in `templates/en/`.

### 1. File Name Cleanups

#### [DELETE] [AGENTS.template.en.md](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/AGENTS.template.en.md)
* Reason: Dropping the `.en` language suffix in favor of path nesting.

#### [DELETE] [config.template.en.toml](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/config.template.en.toml)
* Reason: Dropping the `.en` language suffix.

---

### 2. New Translated Files (No Language Suffix)

#### [NEW] [AGENTS.template.md](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/AGENTS.template.md)
* **Source**: `templates/cn/AGENTS.template.md`
* **Translation Highlights**:
  * Translate all basic principles, quality standards (engineering, code quality, testing requirements), safety checklists, and response rules.
  * Translate all 5 basic principles including sub-agent parallel scheduling and comment instructions (which were missing in the old English version).
  * Translate safety verification rules (e.g. Dangerous Operation Confirmation Mechanism).

#### [NEW] [config.template.toml](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/config.template.toml)
* **Source**: `templates/cn/config.template.toml`
* **Translation Highlights**:
  * Translate primary developer instructions (main agent调度策略, worker constraints, and runtime boundaries).
  * Update model configurations to reflect `gpt-5.4` recommendation.
  * Translate descriptions for `agents.explorer` and `agents.worker` sections.

---

### 3. Sub-agent Configurations Updates

#### [MODIFY] [explorer.toml](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/agents/explorer.toml)
* **Source**: `templates/cn/agents/explorer.toml`
* **Changes**:
  * Add `name = "explorer"` (fixing spelling error `expoloer` in the Chinese version).
  * Add translated `description` field which was completely missing in the old English config.
  * Update `developer_instructions` to reflect the latest rules for exploration.

#### [MODIFY] [worker.toml](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/agents/worker.toml)
* **Source**: `templates/cn/agents/worker.toml`
* **Changes**:
  * Add `name = "worker"`.
  * Add translated `description` field (missing in the old English config).
  * Update and translate the comprehensive `developer_instructions` (including handover protocols for mid-task blocks).

---

### 4. Skill Synchronization

#### [MODIFY] [SKILL.md](file:///Users/alistar/code-all/ai/codex-turbo/templates/en/skills/terminal-dialog-style/SKILL.md)
* **Source**: `templates/cn/skills/terminal-dialog-style/SKILL.md`
* **Key Changes**:
  * **Critical update**: Fully synchronize table design logic. Translate and replace the obsolete "prohibit Markdown table syntax, force ASCII borders" instructions with the new "CLI natively supports Markdown tables, prohibit manually-drawn ASCII tables" rules.
  * Ensure all markdown headers (`#` / `##`) are completely avoided in terminal conversational output samples, replacing them with bolded groups as specified in the Chinese source.
  * Translate all output examples, structural hierarchies, and layout rules precisely.

---

## Verification Plan

### Manual Verification
* Inspect and confirm that all translated files do not contain leftover Chinese characters (except in comments/metadata if necessary, though target is full English translation).
* Verify file name correctness: ensure no `.en` suffix files are left in `templates/en/`.
* Perform git status verification to confirm exact folder mappings.
