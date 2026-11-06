---
title: "Creative Media Agent Capabilities / 创意媒体 Agent 能力索引"
created: 2026-11-06
updated: 2026-11-07
tags: [technology, agents, video, animation, 3d, audio]
status: active
lang: both
---

# 创意媒体 Agent 能力索引

本页说明不同 Agent 可用的创意媒体技能、适用任务和调用边界。执行前检查当前项目、Agent 环境和工具是否可用；不同 Agent 不一定共享本机应用或 MCP 连接。

## 按任务选择

| 任务 | 技能 / 工具 | 适合做什么 | 注意事项 |
|---|---|---|---|
| React 程序化视频 | Remotion + 官方 Remotion Skills | 创建、预览、字幕、动画、渲染与导出 | 技能是工作指引；项目仍需安装依赖。商用需核对许可 |
| 真实动态素材蒙太奇 | OpenMontage documentary-montage 工作流、video-edit、FFmpeg | 挑选真实影像、剪辑 B-roll、配旁白和音乐、做字幕与复核 | OpenMontage 全仓库为 AGPL-3.0；本机只安装了 Skills，未部署整套程序；素材许可逐条检查 |
| 动态字幕、标题和转场 | HyperFrames + hyperframes-core / hyperframes-creative / hyperframes-animation | 用 HTML/CSS/GSAP 制作可控的文字与图形动效、转场和时间线 | HyperFrames 是合成/动效工具，不负责提供实拍镜头或逼真人物素材 |
| 供应商视频 Agent 生成 | create-video | 用文本调用 HeyGen Video Agent 生成整条视频草稿 | 需要 `HEYGEN_API_KEY` 和可用的 HeyGen API；未配置时不可直接使用 |
| 选择场景动效、比较转场 | awesome-ai-motion | 查效果卡、参数和提示词，应用配方时间线，改 HTML 示例渲染 | 按场景意图选效果，避免堆叠无关动效 |
| 网页 UI 与布局动画 | Motion | 界面进入/退出、布局变化和交互动画 | 根据项目框架安装依赖 |
| DOM/SVG 时间线动画 | Anime.js | 编排网页元素、SVG 和时间线动作 | 适合网页内动画 |
| 播放矢量动效 | Lottie | 在网页或应用中播放已有动画 | 播放器不负责完整创作流程 |
| 网页 3D 场景 | Three.js | 场景、材质、灯光、相机和镜头运动 | 先检查目标设备性能 |
| 高质量路径追踪 | Three GPU Pathtracer | Three.js 场景的真实光照和反射 | 开销较高，按设备能力决定 |
| 3D 后期效果 | postprocessing | 泛光、景深、调色等效果 | 与 Three.js 配套 |
| 粒子特效 | Three.quarks | Three.js 粒子与实时特效 | 按项目集成 |
| 实时调参 | Tweakpane | 开发时调整场景参数 | 用于创作调试 |
| 物理模拟 | Jolt Physics | 碰撞、刚体等实时模拟 | 按目标运行环境集成 |
| 操作 Blender 场景 | Blender MCP | 通过 MCP 创建、检查和修改 Blender 场景 | 仅在配置了 Blender MCP 的 Agent 会话中可用 |
| 数学/图表解释动画 | Manim | 公式、图表和概念讲解视频 | 适合程序化数学动画 |
| 节拍与音频分析 | librosa | 提取节奏、音频特征并驱动画面 | Python 音频流程 |
| 旁白合成 | CosyVoice、hyperframes-media | 多语种语音生成和音频/字幕流程指引 | 本机 CosyVoice 尚无模型权重；HyperFrames 音频 skill 的云端 provider 需凭证，TTS 音色与情绪表现须试听验收 |
| 逐词字幕对齐 | WhisperX | 转录并生成词级时间戳 | 首次运行会下载语音/对齐模型 |
| 本地节点式素材生成 | ComfyUI | 组合图像/视频生成工作流 | 需要相应模型，模型可能很大 |
| 录屏 | OBS Studio | 屏幕采集与直播 | macOS 可能要求录屏权限 |
| 无损快速剪辑 | LosslessCut | 快速切片、合并等无损剪辑 | 适合避免重新编码的处理 |
| 编码和最终导出 | FFmpeg | 转码、滤镜、合成、音视频处理 | 检查格式、帧率、分辨率和音轨 |

## Agent 工作流程

1. 先检查当前项目已有框架、依赖、媒体素材和导出要求。
2. 从上表选最少的一组工具；网页库应加到具体项目依赖中。
3. 检查当前 Agent 能否访问目标应用/MCP。不要假设另一台机器或另一 Agent 有相同安装。
4. 需要生成模型时先检查模型大小、磁盘、内存和设备支持，再开始下载。
5. 交付源文件和可复现的预览/导出方式；核对视频尺寸、帧率、音频和字幕。

## 当前个人 Mac 的部署提示

Apple Silicon，8 GB 统一内存。Remotion、网页动效与 3D 库、Manim、librosa、FFmpeg、WhisperX、CosyVoice 运行环境、Blender/OBS/LosslessCut 和 ComfyUI 已安装。ComfyUI 服务已启动，但没有生成模型；CosyVoice 推理环境已装好，但没有语音模型。Blender MCP 已配置；新 Codex 会话通常需要读取该 MCP 配置。详细版本、新装的 OpenMontage/HyperFrames skills 和开源路线见[本机工具链记录](./creative-media-toolchain.md)。Codex 私有技能目录（~/.codex/skills）只存在于个人 Mac，不属于这个 Git 仓库。

