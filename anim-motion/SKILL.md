---
name: anim-motion
description: Motion（motiondivision/motion，原 Framer Motion / Motion One）包装技能：React 与原生 JS 的声明式动效库，擅长画面切换、入场编排、手势与滚动动效。在动画视频流水线里属于「动起来」环节。做网页动效、给 Remotion/网页成片加转场时用。
---

# Motion — 声明式动效与画面切换

一句话：给 DOM 元素写「从哪到哪、多久、什么曲线」，剩下的交给它——React/JS 通用的现代动效库。

- 仓库：https://github.com/motiondivision/motion（TypeScript，约 35.2k stars）
- 流水线位置：动起来。尤其擅长场景切换、元素入场/退场编排。

## 安装与调用

```bash
npm install motion    # 版本 14.14.0
```

最小骨架（原生 JS）：

```js
import {animate, stagger} from 'motion';

animate('.card', {opacity: [0, 1], y: [24, 0]}, {duration: 0.6, delay: stagger(0.08)});
// 场景切换：先退场再入场
await animate('#scene-a', {opacity: 0, x: -40}, {duration: 0.35});
animate('#scene-b', {opacity: [0, 1], x: [40, 0]}, {duration: 0.35});
```

React 里用 `motion/react` 的 `<motion.div animate={...} />` 组件式写法。

## 注意事项

- 它是网页动效库，不是视频渲染器；要出 MP4，把页面放进无头 Chromium 逐帧截图再用 ffmpeg 合成，或在 Remotion 里借它驱动元素。
- 选型原则：一个项目只选一个主动效引擎，别和 GSAP/Anime.js 混着上。
