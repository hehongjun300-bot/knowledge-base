---
title: "lemo-opuscar 实战踩坑记录（DSH 版）"
created: 2026-11-10
updated: 2026-11-10
tags: [references, skills, dsh, video, rendering]
status: active
lang: zh
---

# 实战踩坑记录

用 DSH 版 lemo-opuscar 完整做过一支 4:56 的音乐视频后留下的可复用结论。上游文档不会写这些，因为它们是**这台机器**和**这个版本**才暴露出来的。

## 1 · 渲染速度：默认参数会掉进软件渲染（最重要）

`paper-popup` 这类风格用无头 Chromium 逐帧渲染，启动参数不同，速度差 **27 倍**：

| 启动参数 | WebGL 后端 | 每帧耗时（1920×1080，本机） |
|---|---|---|
| `--use-angle=gl` | **SwiftShader（软件）** | ~2 600 ms |
| `--use-angle=metal` | ANGLE Metal（GPU） | ~236 ms |
| `--use-gl=angle` | ANGLE Metal（GPU） | **~48 ms** |

- 判断方法：在页面里读 `WEBGL_debug_renderer_info`，看 renderer 字符串里有没有 `SwiftShader`。
- 多开 worker **不会**改善软件渲染下的速度（GPU/CPU 争用），只会更慢；换成 GPU 后才值得并行。
- 一支 5 分钟、30 fps 的片子 = 8 900 帧：48 ms/帧 ≈ **7 分钟**；2 600 ms/帧 ≈ **6 小时**。

## 2 · 内存：页数多时要流式加载

页纸贴图约 11 MB/张（2048×1396），每页两张（天空 + 地面）。12 页一次建完 ≈ 275 MB，加 mipmap 超过 360 MB，8 GB 机器上多 worker 会抖。

- 按页**惰性创建 + 翻过后 dispose**，保留前后各一页即可。
- 页面贴图降到 1536 宽几乎看不出差别。

## 3 · 纸片是平片：机位有物理上限

- 与页面法线夹角 **≤ ±30°**、俯角 **18°–55°**；再大就看到卡片侧边，场景塌。
- 想要"环绕半圈"：两个 ±30° 机位接力 + 一次 `scale.x` 翻面，中间切一刀。
- 手持晃动 ≤ 0.6°，房间永远不动。

## 4 · 比例：先定角色身高，再给道具定尺寸

角色 4 cm 时按 1:40 换算道具：床 6 cm、店面 7.5 cm、路灯 10 cm。**先画大床（19 cm）再放人会立刻穿帮**——道具会像墙一样挡住角色。所有道具尺寸和站位都应按"能站几个角色"来定。

## 5 · 字幕/歌词载体的两个坐标 bug（血泪）

1. **页窗口算错一页**：`spread i` 的存活区间是 `[TURNS[i-1].end, TURNS[i].start]`；写成 `[TURNS[i-2].end, TURNS[i-1].start]` 会让"结束时间早于开始时间"，所有字全部不可见，而且**不报错**。
2. **世界坐标 vs 父级坐标**：文字卡挂在 `book.stage` 下，位置是父级局部坐标。把相机空间算出的世界坐标直接 `position.set()` 会被书页变换再叠一次，字会飘到画面外或半个字被切。修复：`book.stage.worldToLocal(p)`。

## 6 · 字号：按 4.4 px/mm 估可读性

整页入画（44 cm 铺满 1920 px）时 1 mm ≈ 4.4 px。**字高 < 5 mm 基本不可读**：

- 爆米花桶上的 18 个字贴纸 → 一个字约 10 px，必须拆行 / 放大载体 / 推近。
- 13 颗灯珠里各藏一个字 → 整页入画时约 30 px，建议两字一灯。

稳妥做法：给每张字卡解一个"距离"，让它恒定占画面 46% 宽 / 24% 高，再落在画面上三分之一——不管机位怎么推都读得清。

## 7 · 音频对齐：先量，不要猜

```bash
ffprobe -v error -show_entries format=duration -of default=nw=1 song.mp3
```

本机这支 296.61 s / 77.7 BPM / 4/4（一小节 3.0896 s，全曲 ≈96 小节）。用"每句歌词 2 小节"把 14 个乐句摊到 82 小节上，前奏 8 小节、尾声 5 小节，实测边界与推算误差 < 0.5 s。

## 8 · 交付前必查

```bash
ffmpeg -hide_banner -i out.mp4 -af ebur128 -f null -            # 集成响度 ≈ −14 LUFS
ffmpeg -hide_banner -i out.mp4 -vf blackdetect=d=0.1 -f null -   # 黑帧应为 0
grep -rniE "lemo ?lab|opus 5\.5" <project>                        # 不应有库署名
```

抽帧检查要**抽在字卡活着的时刻**（每张卡存活约 6 s），不要只抽首尾——否则"一句词没出来"这种全局故障会漏检。
