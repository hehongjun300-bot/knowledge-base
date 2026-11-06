---
title: "Creative Media Toolchain / 视频与网页动效工具链"
created: 2026-11-06
updated: 2026-11-07
tags: [technology, video, web-animation, 3d, audio, agents]
status: active
lang: both
---

# 视频与网页动效工具链

这份清单记录可供 Agent 在网页、视频、3D、音频和导出任务中选择的工具。开始任务时先检查项目现有技术栈，再按需使用。

## 本机部署状态

设备为 Apple Silicon Mac，8 GB 统一内存。工具和 Skill 已按用户授权安装到用户目录；大型生成模型不在本次安装范围内。

- **Remotion Agent Skills**：13 个官方 Skill 已安装在 Codex，包括 remotion-best-practices、remotion-create、remotion-render、remotion-captions 等。它们是工作指引，不等于软件或模型。
- **OpenMontage / HyperFrames 相关 Skills**：从 [calesthio/OpenMontage](https://github.com/calesthio/OpenMontage) 安装了 `hyperframes-core`、`hyperframes-creative`、`hyperframes-animation`、`hyperframes-media`、`media-use`、`video-edit`、`visual-style`、`create-video`，位于 `~/.codex/skills/`。这些本机 Skill 不会随知识库 GitHub 同步；本页只记录用途和来源。`create-video` 依赖 HeyGen Video Agent/API，使用前需确认 `HEYGEN_API_KEY` 和账号能力。
- **JavaScript 工具链**：共享目录 ~/.codex/creative-media-toolchain 已安装 Remotion 4.0.541、Anime.js 4.5.0、Motion 14.9.1、Lottie Web 5.13.0、Three.js 0.187.0、Three GPU Pathtracer 0.0.28、Jolt Physics JS 1.1.1、postprocessing 6.39.6、Three.quarks 0.17.1、Tweakpane 4.0.5、FFmpeg static 5.3.0 和 Remotion headless Chromium。实际项目仍应把所需库写入自己的依赖清单。
- **Manim / librosa / FFmpeg**：Manim Community 0.22.1、librosa 0.11.0、FFmpeg/ffprobe 已安装在共享 Python 环境，命令可从 ~/.local/bin 调用。
- **WhisperX**：3.8.6 已安装，命令可调用。模型按首次任务需要下载；本机建议 CPU、int8 和较小模型。
- **CosyVoice**：源码及 Python 3.10 推理环境已安装，MPS 可用且核心模块导入成功。语音模型未下载；推荐 0.5B 模型仓库约 9.7 GB，超过本机内存预算。
- **Blender + MCP**：Blender 5.2.3 LTS 已安装；MCP 插件 1.8 已启用，Codex 配置在 ~/.codex/config.toml。本地服务监听 127.0.0.1:9876，工具握手成功。若当前 Codex 会话里尚未出现 Blender 工具，重启 Codex 后加载配置。
- **OBS Studio**：33.0.1 已安装。首次录屏时 macOS 可能要求授予屏幕录制权限。
- **LosslessCut**：3.70.2 已安装。
- **ComfyUI**：Comfy Desktop 1.1.8 已安装；本地 Apple Silicon/MPS ComfyUI 0.44.0 服务运行于 http://127.0.0.1:8188。尚未安装生成模型。视频工作流的入门模型约 41–53 GB，不适合本机空间和内存预算。

本机 Codex Skill creative-media-toolchain 提供按任务选工具的路由说明，版本与路径见 ~/.codex/skills/creative-media-toolchain/references/local-setup.md。

## 开源视频制作路线参考

- **OpenMontage**：开源 Agent 视频制作系统，包含 documentary-montage 流程，可检索开放影像/素材并剪成真实动态镜头时间线，也覆盖旁白、音乐、字幕、合成和成片检查。适合实拍 B-roll、情绪蒙太奇和视频 essay 的工作流参考。仓库采用 AGPL-3.0；本机只安装了上面的 Skills，没有克隆或部署整套应用。使用具体素材时仍应逐条核对素材页许可。[GitHub 仓库](https://github.com/calesthio/OpenMontage)
- **HyperFrames**：独立的 HTML/CSS/GSAP 视频合成项目，适合动态字幕、标题、图文动效和可控转场；它负责合成动效，不会自动提供真实摄影镜头。[官方仓库](https://github.com/heygen-com/hyperframes)，Apache-2.0。
- **本机使用边界**：HyperFrames/OpenMontage Skills 只是工作指导，不会自动安装媒体库、API 凭证、音色或模型。`hyperframes-media`、`media-use` 和 `create-video` 涉及 HeyGen 等外部 provider；没有对应凭证时应选可用的本地/免费路径，并明确 TTS 仍可能是合成音。

## 按任务选择

### 网页、界面动画与 3D

- **Motion**：React 界面动画和布局过渡。
- **Anime.js**：时间线编排和 DOM/SVG 动画。
- **Three.js**：浏览器 3D 场景和镜头运动。
- **postprocessing**：Three.js 后期效果；与 Three.js 项目配套。
- **Three.quarks**：Three.js 粒子系统。
- **Tweakpane**：开发时实时调试场景参数。
- **Three GPU Pathtracer**：高质量路径追踪；先验证设备性能。
- **Lottie**：播放已有矢量动画；创作需配套工具。

### 程序化视频、图解和导出

- **Remotion**：React 编写并渲染数据驱动视频。
- **Manim**：数学、公式和图表讲解动画。
- **FFmpeg**：音视频转码、滤镜、合成与导出。
- **LosslessCut**：快速无损剪切。
- **OBS Studio**：录屏和直播采集。

### 3D、物理与生成素材

- **Blender + MCP for Blender**：Agent 操作 Blender 场景；插件和 MCP 服务端均已安装配置。
- **Jolt Physics**：实时 3D 项目的物理模拟；按项目集成。
- **ComfyUI**：本地节点式生成工作流；应用和服务已安装，模型按任务添加。

### 音频与字幕

- **CosyVoice**：语音生成；运行环境已安装，推理模型未下载。
- **librosa**：音频分析和节拍提取。
- **WhisperX**：语音识别及词级时间对齐；模型按需下载。

## Agent 工作规则

1. 视频或网页任务开始时，查看项目已有框架、依赖和运行脚本。
2. 只选完成需求所需的工具；新增 JavaScript 依赖写入当前项目，避免污染其他项目。
3. 需要模型权重时，先检查机器内存、存储和模型大小；模型不是应用安装的一部分。
4. 导出前检查分辨率、帧率、音频、字幕和目标格式，并交付可复现源文件与命令。
5. 涉及 Remotion 商业用途时，先查当前许可条件。

## 原始项目链接

[Remotion](https://github.com/remotion-dev/remotion) · [Remotion Skills](https://github.com/remotion-dev/skills) · [Anime.js](https://github.com/juliangarnier/anime) · [Motion](https://github.com/motiondivision/motion) · [Manim](https://github.com/ManimCommunity/manim) · [Lottie](https://github.com/airbnb/lottie-web) · [MCP for Blender](https://github.com/ahujasid/mcp-for-blender) · [Three.js](https://github.com/mrdoob/three.js) · [Three GPU Pathtracer](https://github.com/gkjohnson/three-gpu-pathtracer) · [Jolt Physics](https://github.com/jrouwe/JoltPhysics) · [postprocessing](https://github.com/pmndrs/postprocessing) · [Three.quarks](https://github.com/Alchemist0823/three.quarks) · [Tweakpane](https://github.com/cocopon/tweakpane) · [ComfyUI](https://github.com/Comfy-Org/ComfyUI) · [CosyVoice](https://github.com/QwenAudio/CosyVoice) · [librosa](https://github.com/librosa/librosa) · [WhisperX](https://github.com/m-bain/whisperX) · [OBS Studio](https://github.com/obsproject/obs-studio) · [LosslessCut](https://github.com/mifi/lossless-cut) · [FFmpeg](https://github.com/FFmpeg/FFmpeg)
