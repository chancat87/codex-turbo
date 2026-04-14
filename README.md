# codex-turbo

[English](./README.en.md) | 简体中文

本仓库是 Codex CLI 的个人配置模板集。秉承 **“轻量高效”** 的原则，在不引入复杂依赖的前提下，深度挖掘 CLI **原生能力**，通过多智能体协作实现高效的任务调度。这套配置仅作为个人实践分享，希望能**抛砖引玉**，助你构建出最适合自己的 AI 工作流。

> 💡 **不知道如何操作？** 可以将以项目地址发送给 AI 助手（如 Claude Code CLI、Codex CLI 等），让其根据你的实际情况协助合并或新建。

> 当前项目适配版本：**Codex CLI v0.120.0**


## 核心要点

- 💡 **并行工作流**：`multi_agent = true` 最大并行度与最小阻塞设计
- 🔧 **系统级契约**：在 `config.toml` 中通过 `developer_instructions` 注入 Agent 并行工作规范，优先级高于 `AGENTS.md`
- 🧠 **原生记忆**：`memories = true` 自动提取和归并对话记忆，提升上下文连贯性
- 🎯 **交互风格**：针对 Codex 原生输出“长句堆砌、路径泛滥、视觉挤压”的终端阅读灾难，深度对齐 `Claude Code` 风格。通过**强制断行、视觉锚点与极简短句**，将混乱的控制台信息转化为层次分明、生动直观的对话体验。

## 核心文件与目录

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

**相关文档**

- [CHANGELOG](./CHANGELOG.md)

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

**已有配置（手动合并）**：→ 详见 [配置迁移指南](./docs/manual-merge.md)

> 说明：本文档按 Codex CLI `v0.116.0` 适配；不同版本或供应商字段名可能有差异，请以你本地 CLI 支持为准。


## 常见问题

**Q1：开了 `multi_agent` 一定更快吗？**

不一定。只有任务可拆、且无写冲突时才明显提速。

**Q2：开了子代理带来什么好处？**

- **上下文隔离** — 子代理独立上下文，避免主代理上下文爆炸
- **职责聚焦** — 每个子代理只处理单一任务，输出更精准
- **并行提效** — 独立任务可并行执行，缩短整体耗时

**Q3：子代理会增加费用吗？**

会。启用子代理后，费用可能上浮 **20%~30%**，具体涨幅取决于项目规模和任务复杂度。

**Q4：子代理开几个合适？**

建议默认即可，观察质量和成本，再逐步调整。

**Q5：子代理模型和主代理模型不一致怎么办？**

通过 `worker.toml` 或 `explorer.toml` 的 `model` 字段单独指定。

**Q6：这套模板适合所有人吗？**

不是。它是起点模板，最好按你的团队习惯逐步裁剪。


## 免责声明

本仓库提供的是配置方法论与模板参考，基于 Codex CLI `v0.116.0` 验证。

**成本提示**：多智能体并发模式下，Token 消耗可能上升 20%~30%，请根据实际情况合理评估使用。

**风险提示**：LLM 可能产生错误判断，导致数据误删或代码被错误修改。建议：
- 合理配置沙箱权限与操作确认机制
- 在可控环境中先行测试
- 对重要数据做好备份

使用本模板所产生的一切后果由使用者自行承担。
