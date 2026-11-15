---
name: anim-konva
description: Konva（konvajs/konva）包装技能：带场景图的交互式 Canvas 2D 框架，图形可拖拽、可点选、自带动画与补间。在动画视频流水线里属于「制作＋修改」环节。做可视化编辑器、交互图解、可拖拽排版工具时用。
---

# Konva — 可交互的 Canvas 场景图

一句话：Canvas 上的图形都是「对象」——能拖、能点、能变形，还能一键导出成图。

- 仓库：https://github.com/konvajs/konva（TypeScript，约 15k stars）
- 流水线位置：制作＋修改。它是这批库里最适合做「可视化编辑器」的，改稿环节靠它。

## 安装与调用

```bash
npm install konva    # 版本 10.9.1
```

最小骨架：

```js
import Konva from 'konva';

const stage = new Konva.Stage({container: 'stage', width: 1280, height: 720});
const layer = new Konva.Layer();
stage.add(layer);

const rect = new Konva.Rect({x: 100, y: 100, width: 200, height: 120, fill: '#e13238', draggable: true});
layer.add(rect);

new Konva.Tween({node: rect, duration: 1, x: 800, rotation: 360}).play();
// 导出当前帧：stage.toDataURL() 或 layer.toCanvas()
```

## 注意事项

- 自带 Tween 够做简单动效，复杂时间线仍建议外挂 Anime.js 驱动属性。
- 逐帧导出：暂停交互循环，逐帧改属性后 `stage.draw()` 再取像素，喂给 gifenc 或 ffmpeg。
- Node 端无头使用需要额外的 canvas 原生包；无头出片时优先在无头 Chromium 里跑。
