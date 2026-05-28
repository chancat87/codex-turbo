# 已有配置：手动合并指南

English version → [manual-merge.en.md](./manual-merge.en.md)

不要直接覆盖现有的 `~/.codex`，建议按下面的步骤合并。

> - 你的现有配置：`~/.codex/config.toml`、`~/.codex/AGENTS.md`
> - 本仓库模板：`templates/cn/config.template.toml`、`templates/cn/AGENTS.template.md`

## 1. 先备份现有配置

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.bak
cp ~/.codex/AGENTS.md ~/.codex/AGENTS.md.bak
[ -d ~/.codex/agents ] && cp -R ~/.codex/agents ~/.codex/agents.bak
[ -d ~/.codex/skills ] && cp -R ~/.codex/skills ~/.codex/skills.bak
```

> 如果你本地已经存在 `~/.codex/agents.bak` 或 `~/.codex/skills.bak`，请先手动处理旧备份，避免再次执行 `cp -R` 时把目录复制成嵌套结构。

## 2. 先看差异，再决定怎么合

```bash
diff -u ~/.codex/config.toml templates/cn/config.template.toml
diff -u ~/.codex/AGENTS.md templates/cn/AGENTS.template.md
```

## 3. `config.toml` 至少合并这些关键块

- `developer_instructions`
- `[features]`
- `[agents]`（注意：自 `v1.7.0` 起，主配置中冗余的子代理 `[agents.explorer]` 与 `[agents.worker]` 区块已废弃并删除，合并时无需保留）
- `[memories]`

## 4. 同步子代理与技能文件，不要遗漏

自 `v1.7.0` 起，虽然在主 `config.toml` 中已彻底废弃了子代理显式区块（改为由程序在 `agents/` 目录下自动扫描加载），但这些子代理的真实 TOML 配置文件及终端对话 Skill 文件仍必须同步存在：

```bash
mkdir -p ~/.codex/agents ~/.codex/skills/terminal-dialog-style
cp templates/cn/agents/explorer.toml ~/.codex/agents/explorer.toml
cp templates/cn/agents/worker.toml ~/.codex/agents/worker.toml
cp templates/cn/skills/terminal-dialog-style/SKILL.md ~/.codex/skills/terminal-dialog-style/SKILL.md
```

## 5. 合并完成后，做一次快速自检

```bash
# 检查 config.toml 关键配置块
rg -n "developer_instructions|\[features\]|\[agents\]|\[memories\]" ~/.codex/config.toml

# 检查关联文件是否存在
test -f ~/.codex/agents/explorer.toml && echo "OK: agents/explorer.toml"
test -f ~/.codex/agents/worker.toml && echo "OK: agents/worker.toml"
test -f ~/.codex/skills/terminal-dialog-style/SKILL.md && echo "OK: skills/terminal-dialog-style/SKILL.md"

# 可选：查看目录结构
ls -R ~/.codex/agents ~/.codex/skills
```

预期结果：

- 第一个命令应至少匹配出这些关键配置块：`developer_instructions`、`[features]`、`[agents]`、`[memories]`
- 后三个 `test -f` 命令都应输出对应的 `OK: ...`
- 如果 `ls -R` 报 `No such file or directory`，说明关联目录没有准备完整，需要回到上一步补齐

## 6. 如果需要回滚，按下面恢复

先确认这些备份文件或目录存在：

- `~/.codex/config.toml.bak`
- `~/.codex/AGENTS.md.bak`
- `~/.codex/agents.bak`
- `~/.codex/skills.bak`

然后执行：

```bash
cp ~/.codex/config.toml.bak ~/.codex/config.toml
cp ~/.codex/AGENTS.md.bak ~/.codex/AGENTS.md

rm -rf ~/.codex/agents
rm -rf ~/.codex/skills

cp -R ~/.codex/agents.bak ~/.codex/agents
cp -R ~/.codex/skills.bak ~/.codex/skills
```

> ⚠️ `rm -rf ~/.codex/agents` 和 `rm -rf ~/.codex/skills` 会直接删除当前目录内容。执行前请先确认 `~/.codex/agents.bak` 与 `~/.codex/skills.bak` 确实存在，且里面是你要恢复的旧配置。

> 不建议直接覆盖你本地已有的供应商配置、API key、MCP 服务配置或其他带环境依赖的字段；模板负责"工作方式"，你本地配置负责"运行环境"。

> ⚠️ **重点**：`config.template.toml` 中的 `developer_instructions` 是系统级契约，优先级高于 `AGENTS.md`，务必确保已合并。
