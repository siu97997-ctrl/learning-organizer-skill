# Learning Organizer Skill

[简体中文](README.md) | [English](README_EN.md)

把分散在多个对话中的学习问题与回答，整理成一份结构清晰、方便检索的 Notion 学习手册。

![Learning Organizer 工作流程](docs/workflow.svg)

## 兼容性

本 Skill 遵循通用的 **Agent Skill 规范**：`SKILL.md` 用 `name` / `description` frontmatter 描述触发条件，配套 `references/` 与 `assets/` 目录存放参考与模板。因此**任何兼容该规范的 Agent 都能直接使用**，包括但不限于：

- OpenAI Codex / Codex CLI
- Anthropic Claude（Agent SDK / Claude Code）
- WorkBuddy

目录里的 `agents/openai.yaml` 只是 Codex 的元数据（显示名、默认 prompt、隐式触发开关），其他 Agent 会自动忽略它，**不影响功能**。

## 为什么做这个项目

聊天记录通常按照时间排列，但真正的学习需要按照知识逻辑组织。随着对话越来越多，重要回答会变得难以查找，重复问题会产生大量噪声，零散笔记也很难帮助使用者建立完整的知识体系。

Learning Organizer 会把对话记录转化为可以长期积累的知识结构：

```text
可访问的学习对话
        ↓
提取问题与完整回答
        ↓
语义去重与内容合并
        ↓
按照知识体系分类
        ↓
定向更新 Notion 手册
        ↓
生成每日索引与下一步建议
```

## 主要功能

- 从可访问的学习对话中提取问题和对应回答
- 按照知识概念组织内容，而不是简单堆叠聊天记录
- 保留每日学习索引，同时避免重复复制完整回答
- 自动识别并合并语义相近的问题
- 补充前置知识、相关概念和下一步学习建议
- 标记可能随时间变化、需要重新核实的信息
- 只对指定的 Notion 页面进行定向更新，严格限制写入范围
- 可用于 AI、产品、语言、商业、研究等不同学习领域

## 效果示例

### 原始学习对话

```text
星期一：“API 是什么？”
星期二：“前端和后端是如何通信的？”
星期五：“API 密钥应该存放在哪里？”
```

### 整理后的知识手册

```text
软件开发基础
├── API 是什么？
├── 前端和后端如何通信
└── API 密钥安全

每日学习索引
├── 星期一 — API 基础
├── 星期二 — 请求流程
└── 星期五 — 安全边界
```

每个问题会包含简短结论、完整解释、前置知识、相关概念和最初学习日期。完整效果可以查看[输出示例](examples/sample-output.md)。

## 仓库结构

```text
skill/organize-learning/
├── SKILL.md
├── agents/openai.yaml        # 仅 Codex 使用；其他 Agent 忽略，可删除
├── references/classification-guide.md
└── assets/handbook-template.md
examples/
├── sample-input.md
└── sample-output.md
```

## 安装和使用

### 通用（Claude / WorkBuddy 等）

把 `skill/organize-learning/` 整个目录复制到对应 Agent 的个人或项目 skills 目录即可：

```text
<你的 Agent skills 目录>/
└── organize-learning/
    ├── SKILL.md
    ├── agents/openai.yaml        # 仅 Codex 使用，可忽略
    ├── references/classification-guide.md
    └── assets/handbook-template.md
```

### Codex

使用 Codex 的 Skill Installer 安装本仓库中的 `skill/organize-learning` 目录，或者把这个目录复制到个人 Skill 文件夹。

### 触发方式

不同 Agent 的调用约定略有差异，但都能通过自然语言和 `SKILL.md` 的 `description` 匹配触发：

| Agent | 显式调用 | 自然语言触发 |
|-------|----------|--------------|
| Codex | `$organize-learning` | 支持（依赖 `openai.yaml` 的 `allow_implicit_invocation`） |
| Claude / WorkBuddy | `/organize-learning`（如支持 slash 命令）或直接描述需求 | 支持（匹配 `SKILL.md` 的 `description`） |

安装后可以明确调用：

```text
整理今天的学习内容，并更新到我已有的 Notion 学习手册。
```

如果使用的 Agent 支持自然语言触发，也可以直接说“整理今天的学习内容”。

## 使用条件

- Codex 或其他兼容 Agent Skill 规范的客户端
- 能够访问学习对话，或者已经导出的聊天内容
- 已连接 Notion，并准备好一个用于接收内容的现有页面

当系统无法安全确认目标页面时，这个 Skill 会先询问使用者。未经明确允许，它不会创建额外页面，也不会修改页面的分享权限。

## 核心设计

### 一个问题只保留一份标准答案

完整回答只保存在知识地图中。每日索引负责记录当天学过什么，但不会重复复制整篇回答。

### 稳定的结构，灵活的学习领域

如果手册已经有分类体系，Skill 会优先沿用原结构。如果还没有分类体系，则使用简洁、通用的分类方法，避免创建大量零散栏目。

### 安全的增量更新

Skill 会在编辑前后读取目标页面，优先进行局部更新，并且不会在没有获得允许的情况下扩大写入范围。

## 隐私与限制

- 只能整理当前环境能够访问的对话
- 无法恢复已经删除或没有访问权限的聊天记录
- 外部平台的内容需要连接器、导出文件或手动粘贴
- 不建议把密码、密钥等敏感信息写入学习手册
- 医疗、法律、金融和时效性信息在使用前仍需要人工核实

公开版本不包含个人 Notion 地址、账号信息或固定知识分类，可以根据不同学习领域复用。

## 开源许可

MIT
