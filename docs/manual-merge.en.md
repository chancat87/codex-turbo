# Existing Configuration: Manual Merge Guide

中文版本 → [manual-merge.md](./manual-merge.md)

Do not overwrite your existing `~/.codex` directly. Merge it step by step.

> - Your current files: `~/.codex/config.toml`, `~/.codex/AGENTS.md`
> - Repository templates: `templates/en/config.template.toml`,
>   `templates/en/AGENTS.template.md`

## 1. Back up your current configuration first

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.bak
cp ~/.codex/AGENTS.md ~/.codex/AGENTS.md.bak
[ -d ~/.codex/agents ] && cp -R ~/.codex/agents ~/.codex/agents.bak
[ -d ~/.codex/skills ] && cp -R ~/.codex/skills ~/.codex/skills.bak
```

> If `~/.codex/agents.bak` or `~/.codex/skills.bak` already exists, clean up
> the old backup first. Otherwise `cp -R` may create nested backup directories.

## 2. Review the diff before deciding how to merge

```bash
diff -u ~/.codex/config.toml templates/en/config.template.toml
diff -u ~/.codex/AGENTS.md templates/en/AGENTS.template.md
```

## 3. At minimum, merge these key blocks in `config.toml`

- `developer_instructions`
- `[features]`
- `[agents]` (Note: Starting from `v1.7.0`, explicit sub-agent declaration blocks `[agents.explorer]` and `[agents.worker]` are deprecated; you don't need to merge them anymore)
- `[memories]`

## 4. Sync the sub-agents and skills files, do not omit them

Starting from `v1.7.0`, although the explicit sub-agent blocks in `config.toml` are deprecated (resolved by automatic folder scanning), you must still synchronize the actual agent TOML files and skill files:

```bash
mkdir -p ~/.codex/agents ~/.codex/skills/terminal-dialog-style
cp templates/en/agents/explorer.toml ~/.codex/agents/explorer.toml
cp templates/en/agents/worker.toml ~/.codex/agents/worker.toml
cp templates/en/skills/terminal-dialog-style/SKILL.md ~/.codex/skills/terminal-dialog-style/SKILL.md
```

## 5. Run a quick self-check after the merge

```bash
# Check key blocks in config.toml
rg -n "developer_instructions|\[features\]|\[agents\]|\[memories\]" ~/.codex/config.toml

# Check whether the related files exist
test -f ~/.codex/agents/explorer.toml && echo "OK: agents/explorer.toml"
test -f ~/.codex/agents/worker.toml && echo "OK: agents/worker.toml"
test -f ~/.codex/skills/terminal-dialog-style/SKILL.md && echo "OK: skills/terminal-dialog-style/SKILL.md"

# Optional: inspect the directory tree
ls -R ~/.codex/agents ~/.codex/skills
```

- The first command should match at least these blocks or fields:
  `developer_instructions`, `[features]`, `[agents]`, `[memories]`
- Each `test -f` command should print its corresponding `OK: ...` line
- If `ls -R` reports `No such file or directory`, the related directories were
  not prepared correctly and you should go back to the previous step

## 6. If you need to roll back, restore it like this

First confirm that these backup files or directories exist:

- `~/.codex/config.toml.bak`
- `~/.codex/AGENTS.md.bak`
- `~/.codex/agents.bak`
- `~/.codex/skills.bak`

Then run:

```bash
cp ~/.codex/config.toml.bak ~/.codex/config.toml
cp ~/.codex/AGENTS.md.bak ~/.codex/AGENTS.md

rm -rf ~/.codex/agents
rm -rf ~/.codex/skills

cp -R ~/.codex/agents.bak ~/.codex/agents
cp -R ~/.codex/skills.bak ~/.codex/skills
```

> ⚠️ `rm -rf ~/.codex/agents` and `rm -rf ~/.codex/skills` will delete the
> current directories immediately. Before running them, make sure
> `~/.codex/agents.bak` and `~/.codex/skills.bak` both exist and really contain
> the old configuration you want to restore.

> Do not blindly overwrite your existing provider configuration, API keys, MCP
> server configuration, or any other environment-dependent fields. The
> templates define the workflow; your local configuration defines the runtime.

> ⚠️ **Important**: `developer_instructions` in `config.template.toml` is a
> system-level contract with higher priority than `AGENTS.md`. Make sure it is
> merged.
