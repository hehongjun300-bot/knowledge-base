---
title: "Creative Media Toolchain / 视频与网页动效工具链"
created: 2026-11-06
updated: 2026-11-06
tags: [technology, video, web-animation, 3d, audio, agents]
status: active
lang: both
---

# 视频与网页动效工具链

这份清单记录可供 Agent 在网页、视频、3D、音频和导出任务中选择的工具。先检查项目现有技术栈和本机依赖，再按任务需要使用；不要把所有库塞进每个项目。

## Agent Skills 已安装

本机 Codex 已安装 Remotion 官方 Skills（来源：[remotion-dev/skills](https://github.com/remotion-dev/skills)），下一轮 Codex 对话中可用：

- remotion-best-practices
- remotion-captions
- remotion-create
- remotion-docs
- remotion-interactivity
- remotion-license
- remotion-maps
- remotion-markup
- remotion-multimedia
- remotion-render
- remotion-saas
- remotion-studio
- remotion-upgrade

Skill 是 Agent 的工作指引，不等于软件或运行时已安装。Remotion 渲染仍需要具体项目的依赖和浏览器环境；商用场景需先核对 Remotion 许可。

## 按任务选择

### 网页、界面动画与 3D

- **Motion**：React 界面动画和布局过渡。按项目添加依赖。
- **Anime.js**：时间线编排和 DOM/SVG 动画。按项目添加依赖。
- **Three.js**：浏览器 3D 场景和镜头运动。按项目添加依赖。
- **postprocessing**：Three.js 后期效果；与 Three.js 项目配套。
- **Three.quarks**：Three.js 粒子系统；按需加入。
- **Tweakpane**：开发时实时调试场景参数。
- **Three GPU Pathtracer**：需要高质量离线式渲染时评估，先验证浏览器与设备性能。
- **Lottie**：播放已有矢量动画；若要制作动画，需另选创作工具。

### 程序化视频、图解和导出

- **Remotion**：React 编写并渲染视频；优先用于可复用、数据驱动或可编程的视频。
- **Manim**：数学、公式和图表讲解动画。
- **FFmpeg**：音视频转码、滤镜、合成与导出；作为命令行工具使用。
- **LosslessCut**：快速无损剪切；桌面应用。
- **OBS Studio**：录屏和直播采集；桌面应用。

### 3D、物理与生成素材

- **Blender + MCP for Blender**：Agent 操作 Blender 场景。需分别安装 Blender 插件和 MCP 服务端，并在 Codex 中配置连接。
- **Jolt Physics**：游戏或实时 3D 项目中的物理模拟；按项目集成。
- **ComfyUI**：本地节点式生成工作流；需单独部署服务与模型，评估磁盘、内存和 GPU 后再安装。

### 音频与字幕

- **CosyVoice**：语音生成；模型和推理环境单独部署。
- **librosa**：音频分析和节拍提取；Python 项目依赖。
- **WhisperX**：语音识别及词级时间对齐；Python/模型依赖，按需部署。

## 当前安装边界

已确认本机有 Node.js/npm；本机 Codex 的 Remotion Skills 已安装。Remotion、Motion、Anime.js、Three.js、Lottie、Jolt、postprocessing、Three.quarks、Tweakpane 等是项目级依赖，应在具体项目中安装，避免全局安装或污染其他项目。FFmpeg、Blender、OBS、LosslessCut、ComfyUI、CosyVoice、WhisperX、Manim 等需要单独安装或配置；安装前应检查当前机器、包管理器、磁盘和模型/GPU需求。当前未确认这些软件/模型可运行。

## Agent 工作规则

1. 视频或网页任务开始时，查看项目已有框架、依赖和可运行脚本。
2. 选最少的一组工具解决需求；新增依赖写入当前项目清单，避免全局安装 JavaScript 库。
3. 系统工具缺失时，说明具体缺项并优先给可复现的安装方式；高体积模型或会下载大量资产的工具，先确认资源需求。
4. 导出前检查分辨率、帧率、音频、字幕和目标格式；尽可能交付可复现的源文件与导出命令。
5. 涉及 Remotion 商业用途时，先查当前许可条件。

## 原始项目链接

[Remotion](https://github.com/remotion-dev/remotion) · [Remotion Skills](https://github.com/remotion-dev/skills) · [Anime.js](https://github.com/juliangarnier/anime) · [Motion](https://github.com/motiondivision/motion) · [Manim](https://github.com/ManimCommunity/manim) · [Lottie](https://github.com/airbnb/lottie-web) · [MCP for Blender](https://github.com/ahujasid/mcp-for-blender) · [Three.js](https://github.com/mrdoob/three.js) · [Three GPU Pathtracer](https://github.com/gkjohnson/three-gpu-pathtracer) · [Jolt Physics](https://github.com/jrouwe/JoltPhysics) · [postprocessing](https://github.com/pmndrs/postprocessing) · [Three.quarks](https://github.com/Alchemist0823/three.quarks) · [Tweakpane](https://github.com/cocopon/tweakpane) · [ComfyUI](https://github.com/Comfy-Org/ComfyUI) · [CosyVoice](https://github.com/FunAudioLLM/CosyVoice) · [librosa](https://github.com/librosa/librosa) · [WhisperX](https://github.com/m-bain/whisperX) · [OBS Studio](https://github.com/obsproject/obs-studio) · [LosslessCut](https://github.com/mifi/lossless-cut) · [FFmpeg](https://github.com/FFmpeg/FFmpeg)
