# codex-turbo

[English](./README.en.md) | 简体中文

分享基于 Codex 原生功能的配置模板，克制功能扩展，追求更快、更稳、更可复用。

> 当前项目适配版本：**Codex CLI v0.114.0**

## 核心要点

- 💡 **并行工作流**：`multi_agent = true` 最大并行度与最小阻塞设计
- 🔧 **系统级契约**：在 `config.toml` 中通过 `developer_instructions` 注入 Agent 并行工作规范，优先级高于 `AGENTS.md`
- 🧠 **原生记忆**：`memories = true` 自动提取和归并对话记忆，提升上下文连贯性
- 🔌 **WebSocket 支持**：`responses_websockets_v2 = true` 启用实时流式响应，不支持自动回退
- 🎯 **对话风格**：强视觉边界、emoji 编号、直而短句的终端输出规范
- 📝 **标准契约**：子代理任务下发的清晰指令模板（名称/目标/动作/结果）
- ⚙️ **并发控制**：`max_threads = 5` 保守限制单轮最大子任务数
- ⚠️ **风险管控**：危险操作确认机制与不可变原则
- 📋 **可复制模板**：开箱即用的 `AGENTS.template.md` 与 `config.toml.example`

## 为什么做这个仓库

原帖信息`https://linux.do/t/topic/1603762`，但偏“长文流”，此次优化为：

- 按主题查阅（上手 / 配置 / FAQ / 模板）
- 按团队二次定制（模板直接复制改）
- 持续迭代（PR/Issue 留痕）

## 目录结构

```text
.
├── README.md              # 中文文档（本页）
├── README.en.md           # English Documentation
├── docs/
│   ├── faq.md             # 中文 FAQ
│   └── faq.en.md          # English FAQ
└── templates/
    ├── AGENTS.template.md     # 中文开发原则模板
    ├── AGENTS.template.en.md  # English Development Guidelines
    ├── config.toml.example    # 中文配置模板
    └── config.toml.en.example # English Config Template
```

## 快速上手（5 分钟）

目标：把你的 Codex CLI 切到”并行 + 模板化”工作模式。

### 1. 克隆仓库

```bash
git clone <your-repo-url>
cd codex-turbo
```

### 2. 复制模板配置

本仓库提供两个核心模板文件：

| 文件 | 用途 | 目标位置 |
|------|------|----------|
| `templates/config.toml.example` | 系统配置（含 `developer_instructions` 并行工作规范） | `~/.codex/config.toml` |
| `templates/AGENTS.template.md` | 开发原则与输出风格指南 | `~/.codex/AGENTS.md` |

**首次使用（直接复制）**：

```bash
cp templates/AGENTS.template.md ~/.codex/AGENTS.md
cp templates/config.toml.example ~/.codex/config.toml
```

**已有配置（手动合并）**：查看注释后，对比差异后合并关键配置。

> ⚠️ **重点**：`config.toml.example` 中的 `developer_instructions` 是系统级契约，优先级高于 `AGENTS.md`，务必确保已合并。

> 说明：本文档按 Codex CLI `v0.114.0` 适配；不同版本或供应商字段名可能有差异，请以你本地 CLI 支持为准。

## 文档导航

- `README.md`：快速上手（本页）
- `docs/faq.md`：常见坑与排查
- `templates/AGENTS.template.md`：开发原则与输出风格模板
- `templates/config.toml.example`：系统配置模板（含 `developer_instructions`）

## 适用范围提醒

- 个人项目：可激进，迭代快
- 团队/公司项目：以团队规范、发布流程、兼容策略为准

特别是“修改功能不保留旧兼容代码”这条：

- 对可控项目是提效利器
- 对企业项目必须评估影响并走评审流程

## 免责声明

本仓库是方法论与模板参考，当前按 Codex CLI v0.114.0 验证。

⚠️ **风险提示**：LLM 可能产生错误判断，导致合理数据被误删或代码被错误修改。请合理分配权限，建议在可控环境中先行测试，使用本模板所产生的任何后果需自行承担。
