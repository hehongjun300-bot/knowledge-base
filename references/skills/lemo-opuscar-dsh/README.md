---
title: "lemo-opuscar 技能 —— DeepSeek Harness（DSH）适配版"
created: 2026-11-10
updated: 2026-11-10
tags: [references, skills, dsh, video, animation]
status: active
lang: both
---

# lemo-opuscar · DSH 适配版

> ⚠️ **这是 DeepSeek Harness（DSH）的适配版本，不是 Codex 的技能插件，也不是 Claude Code 的 plugin。**
>
> 三者同名同源、互不通用。Codex 的私有技能目录（`~/.codex/skills`）不在本仓库；Claude Code 的插件目录（`~/.claude/`）也不在。本目录只保存 **DSH 版**，文件名和安装路径都带 `dsh` 标识，避免混装。

| | 本项目（本目录） | Codex 技能 | Claude Code 插件 |
|---|---|---|---|
| 平台 | DeepSeek Harness | Codex | Claude Code |
| 安装位置 | `~/.dsh/skills/lemo-opuscar/` | `~/.codex/skills/` | 插件市场 / `~/.claude/` |
| 调用方式 | `/lemo-opuscar`，或直接说"做一支…的视频" | Codex 的 skill 机制 | `/lemo-opuscar:lemo-opuscar` |
| 提问工具 | `ask_user_question` | `AskUserQuestion` | `AskUserQuestion` |
| 上游 | [github.com/lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar) | 同 | 同 |

## 这是什么

Lemo-Opuscar 是一个**用代码直接拍短片**的风格库：66 种风格（油画厚涂、水彩、浮世绘、纸片立体书、卫星简报、产品拆解…），每种风格带一份 `STYLE.md`（不变量）和一支完全由代码生成的样片。技能本身只是一份"转接说明"——它把你交给那个库，由库里的 `AGENTS.md` / `DIRECTOR.md` / `TECHNIQUE.md` 指导选风格、写 treatment、分镜、配音、配乐、渲染和交付。

**技能不含库，也不含素材。** 库要单独克隆到 `~/lemo-opuscar`（见下）。

## 目录内容

```
references/skills/lemo-opuscar-dsh/
├── README.md          ← 本文件（DSH 适配说明）
├── SKILL.md           ← 与安装文件逐字一致，可直接拷回 ~/.dsh/skills/
├── PRODUCTION-NOTES.md← 实战踩坑记录（渲染速度、显存、机位、字幕坐标）
└── scripts/setup.sh   ← 上游脚本，逐字一致
```

`SKILL.md` 和 `scripts/setup.sh` 与 `~/.dsh/skills/lemo-opuscar/` 下的安装文件 **diff 为空**，所以可以直接反向恢复：

```bash
mkdir -p ~/.dsh/skills/lemo-opuscar
cp -R references/skills/lemo-opuscar-dsh/SKILL.md \
      references/skills/lemo-opuscar-dsh/scripts \
      ~/.dsh/skills/lemo-opuscar/
```

## DSH 版改了什么（相对上游原版）

1. **库位置固定，不联网更新。** `~/lemo-opuscar` 指向本机克隆，`setup.sh` 只做定位与依赖检查，不做 `git fetch`／重新克隆。
2. **提问工具换名。** 上游写的 `AskUserQuestion` → DSH 的 `ask_user_question`。
3. **没有 Task / 子代理的硬性要求。** 上游某些段落假设有子代理，DSH 版改为"可选"。
4. **调用形式。** 上游 Claude Code 的 `/lemo-opuscar:lemo-opuscar` 不存在，改 `/lemo-opuscar` 或自然语言触发。
5. **质量提示。** 上游为上代模型调校，DSH 版明确要求：以 `STYLE.md` 的不变量和样片定帧为准则，交付前自检。

## 本机依赖（已就绪）

| 组件 | 状态 |
|---|---|
| Node | 26.x |
| ffmpeg | 9.x |
| Python | `~/lemo-opuscar/.venv`（numpy / scipy / soundfile / fonttools） |
| 浏览器 | Playwright Chromium |
| 库 | `~/lemo-opuscar`（含 `core/`、`styles/`、已装依赖） |

首次补齐（一般无需重跑）：

```bash
sh ~/.dsh/skills/lemo-opuscar/scripts/setup.sh          # 定位库
sh ~/.dsh/skills/lemo-opuscar/scripts/setup.sh deps     # 核心依赖
```

## 怎么用

- 想选风格：让它打开风格画廊（66 个风格各有样片），挑一个再开工。
- 有明确主题：直接说"用纸片立体书做一支《X》的视频"。
- 自己的素材（音频/照片/数据）：放进项目文件夹，告诉它路径。

产出物落在一个项目文件夹里：成片 mp4、封面、srt、`TREATMENT.md`、`CREDITS`、可一键重建的 `build.sh`。

## 边界

- 只存技能文本与脚本；**不含**上游库源码、演示片、素材包。上游许可见其仓库。
- 不代替用户判断素材版权：影片里出现的音乐、词、照片由使用者负责。
- 实战注意事项（尤其**渲染速度**与**字幕定位**）见 [PRODUCTION-NOTES.md](./PRODUCTION-NOTES.md)。

## 相关

- [创意媒体 Agent 能力索引](../../../domains/tech/creative-media-agent-capabilities.md)
- 上游库：<https://github.com/lemomo-ai/lemo-opuscar>
