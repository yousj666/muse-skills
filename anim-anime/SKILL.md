---
name: anim-anime
description: Anime.js（juliangarnier/anime）包装技能：轻量 JS 动画引擎，时间线、错峰（stagger）、SVG 路径动画是强项。在动画视频流水线里属于「动起来」环节。做 DOM/SVG 时间线动画、网页成片逐帧导出时用。
---

# Anime.js — 时间线与错峰动效引擎

一句话：一条时间线管全部元素，错峰、交叠、SVG 描边动画都是一行配置的事。

- 仓库：https://github.com/juliangarnier/anime（JavaScript，约 74.7k stars）
- 流水线位置：动起来。网页动效选型里的常客。

## 安装与调用

```bash
npm install animejs    # 版本 4.5.0，注意包名是 animejs
```

最小骨架（v4 API）：

```js
import {animate, createTimeline, stagger} from 'animejs';

animate('.dot', {x: 250, duration: 800, ease: 'outQuad', delay: stagger(60)});

const tl = createTimeline({defaults: {duration: 600}});
tl.label('start')
  .add('.title', {opacity: [0, 1], y: [20, 0]})
  .add('.bar', {scaleX: [0, 1]}, '<<200');   // 与上一段交叠 200ms
```

## 注意事项

- v4 的 API 与 v3 完全不同：没有默认导出的 `anime()` 函数，改用具名导入 `animate/createTimeline`；网上老教程多为 v3，照抄会报错。
- 出 MP4 同样要走无头 Chromium 逐帧截图＋ffmpeg，或作为 Remotion 里的驱动层。
- 与 Motion/GSAP 三选一，别在同一项目里混用多个主动效引擎。
