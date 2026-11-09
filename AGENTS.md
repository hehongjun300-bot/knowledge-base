# 🤖 AGENTS.md — Agent Entry Point / Agent 入口文件

> **For AI Agents**: Read this file first. It tells you who I am, how this repo is organized, and how to work with me.
>
> **给 AI Agent**：请先阅读此文件。它会告诉你我是谁、这个仓库如何组织、以及如何与我协作。

---

## 👤 Identity / 身份

- **Name / 姓名**: Hugo
- **GitHub**: [@hugo](https://github.com/hugo)
- **Role / 角色**: Builder & Lifelong Learner / 构建者 & 终身学习者
- **Languages / 语言**: 中文 (native), English

> [!NOTE]
> This section will be enriched over time with more details about professional background, skills, and expertise areas.
> 此部分将随时间丰富，加入更多职业背景、技能和专业领域信息。

---

## 🗺️ Repository Map / 仓库地图

```
knowledge-base/
├── AGENTS.md              ← 📍 You are here / 你在这里
├── README.md              ← Human-readable intro / 人类可读介绍
├── CHANGELOG.md           ← Repo changelog / 变更日志
│
├── profile/               ← Who I am / 个人画像
│   ├── about-me.md        ← Background & skills / 背景与技能
│   ├── values.md          ← Core values & principles / 价值观与原则
│   └── goals.md           ← Short & long-term goals / 目标
│
├── domains/               ← Knowledge by topic / 按主题分类的知识
│   ├── tech/              ← Technology / 技术
│   │   └── creative-media-agent-capabilities.md ← Agent 创意媒体能力索引
│   ├── business/          ← Business & startups / 商业
│   ├── reading/           ← Book notes / 阅读笔记
│   └── life/              ← Life philosophy / 生活哲学
│
├── projects/              ← Project records / 项目记录
│   └── (each with overview, decisions, learnings)
│
├── journal/               ← Thinking logs / 思考日志
│   └── YYYY/MM/DD.md
│
├── references/            ← Bookmarks, quotes, tools / 参考资料
│   └── skills/            ← Installed agent skills (DSH-adapted) / 已装技能（DSH 适配）
│       └── lemo-opuscar-dsh/  ← ⚠️ DSH 版，非 Codex 技能、非 Claude Code 插件
│
└── templates/             ← File templates / 文件模板
```

### Priority Reading Order / 优先阅读顺序
1. This file (`AGENTS.md`)
2. `profile/goals.md` — to understand current direction / 了解当前方向
3. `journal/` — latest entries for recent thinking / 最新日志了解近期思考
4. Relevant `domains/` folder based on the task / 根据任务查看相关领域
5. For video, animation, 3D, audio, subtitles, or export tasks, read `domains/tech/creative-media-agent-capabilities.md` / 视频、动效、3D、音频、字幕或导出任务先读该能力索引
6. Before using a saved skill, read its note under `references/skills/` — platform matters: the **DSH** builds are not interchangeable with Codex skills or Claude Code plugins / 用已存技能前先看 `references/skills/` 下的说明——平台不同，**DSH 版与 Codex 技能、Claude Code 插件不可互换**

---

## 🧠 Thinking Framework / 思维框架

### Decision Principles / 决策原则
- **First Principles Thinking** / 第一性原理：回到本质思考问题
- **Simplicity First** / 简洁优先：能简单解决的不要复杂化
- **Learn by Building** / 以建代学：通过实践来学习
- **Write to Think** / 以写促思：通过写作整理思路

### Preferences / 偏好
- Prefer practical solutions over theoretical perfection / 偏好实用方案而非理论完美
- Value clear documentation / 重视清晰的文档
- Like structured thinking but flexible execution / 喜欢结构化思考但灵活执行

---

## 🎯 Current Focus / 当前焦点

> **Last updated / 最后更新**: 2026-11-05

### Active Priorities / 活跃优先事项
1. 🧠 **Building this knowledge base** / 搭建个人知识仓库
   - Establishing structure and habits / 建立结构与习惯
   - Making it AI-agent friendly / 让它对 AI Agent 友好

> [!TIP]
> Update this section regularly to keep agents informed of your latest priorities.
> 请定期更新此部分，让 Agent 了解你的最新优先事项。

---

## 🤝 Collaboration Guide / 协作指南

### Communication Preferences / 沟通偏好
- **Language / 语言**: 中文为主，技术术语可用英文 / Chinese primary, English for technical terms
- **Style / 风格**: 简洁直接，避免废话 / Concise and direct, avoid fluff
- **Detail level / 详细程度**: 给出关键信息和理由，不需要过度解释 / Key info and reasoning, no over-explaining

### When Helping Me / 帮助我时
- ✅ Propose actionable steps / 提出可执行的步骤
- ✅ Challenge my assumptions when needed / 必要时挑战我的假设
- ✅ Suggest connections between topics / 建议主题间的关联
- ✅ Reference existing notes in this repo when relevant / 相关时引用本仓库已有笔记
- ❌ Don't over-explain basic concepts / 不要过度解释基础概念
- ❌ Don't be overly cautious or hedging / 不要过于谨慎或模棱两可

### File Conventions / 文件约定
- All markdown files use **YAML frontmatter** for metadata / 所有 md 文件使用 YAML frontmatter
- Tags follow the format: `tags: [topic, subtopic]`
- Dates use ISO 8601: `YYYY-MM-DD`
- Internal links use relative paths: `[link](../path/to/file.md)`

---

## 📋 Frontmatter Schema / 元数据格式

Every content file should include:

```yaml
---
title: "Document Title"
created: 2026-11-05
updated: 2026-11-05
tags: [topic, subtopic]
status: draft | active | archived
lang: zh | en | both
---
```

---

> **This file is the single source of truth for any Agent interacting with this repository.**
>
> **此文件是任何 Agent 与本仓库交互时的唯一真相来源。**
