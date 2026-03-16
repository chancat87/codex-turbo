# codex-turbo

English | [简体中文](./README.md)

Curated configuration templates based on Codex native features, with restrained extensions, pursuing faster, more stable, and more reusable workflows.

> Current compatible version: **Codex CLI v0.114.0**

## Key Features

- 💡 **Parallel Workflow**: `multi_agent = true` for maximum parallelism with minimal blocking
- 🔧 **System-level Contract**: Inject Agent parallel workflow rules via `developer_instructions` in `config.toml`, higher priority than `AGENTS.md`
- 🧠 **Native Memory**: `memories = true` for automatic extraction and consolidation of conversation memory, improving context continuity
- 🔌 **WebSocket Support**: `responses_websockets_v2 = true` for real-time streaming responses, no automatic fallback
- 🎯 **Conversation Style**: Strong visual boundaries, emoji numbering, short and direct terminal output
- 📝 **Standard Contract**: Clear instruction templates for sub-agent tasks (name/goal/action/result)
- ⚙️ **Concurrency Control**: `max_threads = 5` conservative limit for maximum concurrent sub-tasks
- ⚠️ **Risk Management**: Dangerous operation confirmation mechanism and immutable principles
- 📋 **Copy-paste Templates**: Ready-to-use `AGENTS.template.en.md` and `config.toml.en.example`

## Directory Structure

```text
.
├── README.md              # 中文文档
├── README.en.md           # English Documentation (this page)
├── docs/
│   ├── faq.md             # 中文 FAQ
│   └── faq.en.md          # English FAQ
└── templates/
    ├── AGENTS.template.md     # 中文开发原则模板
    ├── AGENTS.template.en.md  # English Development Guidelines
    ├── config.toml.example    # 中文配置模板
    └── config.toml.en.example # English Config Template
```

## Quick Start (5 minutes)

Goal: Switch your Codex CLI to "parallel + template-based" workflow mode.

### 1. Clone Repository

```bash
git clone <your-repo-url>
cd codex-turbo
```

### 2. Copy Template Configuration

This repository provides two core template files:

| File | Purpose | Target Location |
|------|---------|-----------------|
| `templates/config.toml.en.example` | System config (includes `developer_instructions` parallel workflow rules) | `~/.codex/config.toml` |
| `templates/AGENTS.template.en.md` | Development principles and output style guide | `~/.codex/AGENTS.md` |

**First time (direct copy)**:

```bash
cp templates/AGENTS.template.en.md ~/.codex/AGENTS.md
cp templates/config.toml.en.example ~/.codex/config.toml
```

**Existing config (manual merge)**: Review comments and compare differences, then merge key configurations.

> ⚠️ **Important**: The `developer_instructions` in `config.toml.en.example` is a system-level contract with higher priority than `AGENTS.md`. Make sure it's merged.

> Note: This document is adapted for Codex CLI `v0.114.0`; different versions or providers may have different field names, please refer to your local CLI support.

## Documentation Navigation

- `README.en.md`: Quick Start (this page)
- `docs/faq.en.md`: Common pitfalls and troubleshooting
- `templates/AGENTS.template.en.md`: Development principles template
- `templates/config.toml.en.example`: System configuration template (includes `developer_instructions`)

## Scope Notice

- Personal projects: Can be aggressive, iterate fast
- Team/Company projects: Follow team standards, release processes, and compatibility policies

Especially for "not preserving old compatibility code when modifying features":

- For controllable projects: Efficiency booster
- For enterprise projects: Must assess impact and go through review process

## Disclaimer

This repository provides methodology and template references, currently verified with Codex CLI v0.114.0.

⚠️ **Risk Warning**: LLM may produce incorrect judgments, leading to reasonable data being mistakenly deleted or code being incorrectly modified. Please assign permissions reasonably, test in controllable environments first. You are responsible for any consequences of using these templates.
