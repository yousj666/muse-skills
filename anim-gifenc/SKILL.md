---
name: anim-gifenc
description: gifenc（mattdesl/gifenc）包装技能：纯 JS 的高速 GIF 编码器，把逐帧像素数据直接编码成 GIF，浏览器和 Node 都能跑。在动画视频流水线里属于「导出」环节。把 Canvas 动画、逐帧渲染结果导成 GIF 时用。
---

# gifenc — GIF 导出编码器

一句话：喂给它一帧帧的像素，它吐出一个 GIF 文件——纯 JS、无原生依赖、速度快。

- 仓库：https://github.com/mattdesl/gifenc（JavaScript，约 360 stars）
- 流水线位置：导出。Canvas/Two.js/Konva 逐帧渲染的天然搭档。

## 安装与调用

```bash
npm install gifenc    # 版本 1.0.3
```

最小骨架（Node/浏览器通用）：

```js
import {GIFEncoder, quantize, applyPalette} from 'gifenc';

const gif = GIFEncoder();
for (const frame of frames) {                    // frame = Uint8Array RGBA 像素
  const palette = quantize(frame, 256);
  const index = applyPalette(frame, palette);
  gif.writeFrame(index, width, height, {palette, delay: 40});  // delay 单位 ms
}
gif.finish();
const bytes = gif.bytes();                        // 写文件或下载
```

## 注意事项

- 量化（quantize）是画质关键：默认算法够用，色彩丰富的帧可试 `format: 'rgb444'` 等选项换速度/体积平衡。
- GIF 体积膨胀快：长动画控制在几秒内、降分辨率或降帧率；长片请走 MP4（ffmpeg），别硬塞 GIF。
