---
name: anim-twojs
description: Two.js（jonobr1/two.js）包装技能：渲染器无关的 2D 绘图 API，同一套代码可输出 SVG/Canvas/WebGL。在动画视频流水线里属于「制作」环节的 2D 图形层。画矢量场景、示意图动画时用。
---

# Two.js — 2D 矢量绘图与动画

一句话：用统一 API 画圆、路径、文字，底层渲染器（SVG/Canvas/WebGL）随你换。

- 仓库：https://github.com/jonobr1/two.js（JavaScript，约 8.7k stars）
- 流水线位置：制作（2D 图形）。常与 Shifty/Anime.js 搭配驱动。

## 安装与调用

```bash
npm install two.js    # 版本 0.8.24
```

最小骨架：

```js
import Two from 'two.js';

const two = new Two({width: 1280, height: 720, type: Two.Types.svg}).appendTo(document.body);
const circle = two.makeCircle(640, 360, 80);
circle.fill = '#e13238'; circle.noStroke();

two.bind('update', frameCount => {
  circle.scale = 1 + 0.1 * Math.sin(frameCount / 20);
}).play();
```

## 注意事项

- 本身只有简易的 update 循环，复杂时间线交给 Anime.js/Shifty 驱动它的属性。
- SVG 渲染器方便逐帧导出帧图（序列化 SVG → 转 PNG → ffmpeg 合成），是无头环境出 2D 矢量动画片的稳妥路线。
