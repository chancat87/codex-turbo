# codex-turbo

[English](./README.en.md) | 简体中文

本仓库是 Codex CLI 的个人配置模板集，旨在充分利用 CLI 原生能力，实现多智能体自主协调下的并行任务调度。

> 当前项目适配版本：**Codex CLI v0.114.0**

## 核心要点

- 💡 **并行工作流**：`multi_agent = true` 最大并行度与最小阻塞设计
- 🔧 **系统级契约**：在 `config.toml` 中通过 `developer_instructions` 注入 Agent 并行工作规范，优先级高于 `AGENTS.md`
- 🧠 **原生记忆**：`memories = true` 自动提取和归并对话记忆，提升上下文连贯性
- 🔌 **WebSocket 支持**：`responses_websockets_v2 = true` 启用实时流式响应，不支持自动回退
- 🎯 **对话风格**：强视觉边界、emoji 编号、直而短句的终端输出规范
- 📝 **标准契约**：子代理任务下发的清晰指令模板（名称/目标/动作/结果）
- ⚙️ **并发控制**：`max_threads = 10` 自定义单轮最大子任务数
- ⚠️ **风险管控**：危险操作确认机制与不可变原则
- 📋 **可复制模板**：开箱即用的 `AGENTS.template.md` 与 `config.template.toml`

## 为什么做这个仓库

原帖信息`https://linux.do/t/topic/1603762`，但偏“长文流”，此次优化为：

- 按主题查阅（上手 / 配置 / FAQ / 模板）
- 按团队二次定制（模板直接复制改）
- 持续迭代（PR/Issue 留痕）

## 目录结构

```text
.
├── README.md                  # 中文文档（本页）
├── README.en.md               # English Documentation
└── templates/
    ├── cn/                        # 中文模板
    │   ├── AGENTS.template.md         # 开发原则与输出风格
    │   ├── config.template.toml       # 系统配置模板
    │   ├── agents/                    # 子代理配置
    │   │   ├── explorer.toml
    │   │   └── worker.toml
    │   └── skills/                    # 技能模板
    │       └── terminal-dialog-style/
    └── en/                        # English Templates
        ├── AGENTS.template.en.md
        ├── config.toml.en.example
        ├── agents/
        └── skills/
```

## 快速上手（5 分钟）

目标：把你的 Codex CLI 切到”并行 + 模板化”工作模式。

### 1. 克隆仓库

```bash
git clone <your-repo-url>
cd codex-turbo
```

### 2. 复制模板配置

本仓库提供以下模板文件：

| 文件 | 用途 | 目标位置 |
|------|------|----------|
| `templates/cn/config.template.toml` | 核心的系统配置（含 `developer_instructions` 并行工作规范） | `~/.codex/config.toml` |
| `templates/cn/AGENTS.template.md` | 开发原则与输出风格指南 | `~/.codex/AGENTS.md` |
| `templates/cn/agents/` | 子代理配置（explorer、worker） | `~/.codex/agents/` |
| `templates/cn/skills/` | 技能模板（terminal-dialog-style 等） | `~/.codex/skills/` |

> config.toml 请根据服务商的要求自行完善 key 等供应商信息。

**首次使用（直接复制）**：

```bash
# 创建目标目录（如不存在）
mkdir -p ~/.codex

# 复制核心配置文件
cp templates/cn/AGENTS.template.md ~/.codex/AGENTS.md
cp templates/cn/config.template.toml ~/.codex/config.toml

# 复制子代理和技能目录
cp -r templates/cn/agents ~/.codex/
cp -r templates/cn/skills ~/.codex/
```

**已有配置（手动合并）**：查看注释后，对比差异后合并关键配置。

> ⚠️ **重点**：`config.template.toml` 中的 `developer_instructions` 是系统级契约，优先级高于 `AGENTS.md`，务必确保已合并。

> 说明：本文档按 Codex CLI `v0.115.0` 适配；不同版本或供应商字段名可能有差异，请以你本地 CLI 支持为准。

## 文档导航

- `README.md`：快速上手（本页）
- `templates/cn/AGENTS.template.md`：开发原则与输出风格模板
- `templates/cn/config.template.toml`：系统配置模板（含 `developer_instructions`）
- `templates/cn/agents/`：子代理配置模板
- `templates/cn/skills/`：技能模板

## 免责声明

本仓库是方法论与模板参考，当前按 Codex CLI v0.115.0 验证。
请注意，多智能体并发可能导致Token 消耗上升20%~30%，请根据自身情况合理使用。

⚠️ **风险提示**：LLM 可能产生错误判断，导致合理数据被误删或代码被错误修改。请合理分配权限，建议在可控环境中先行测试，使用本模板所产生的任何后果需自行承担。
