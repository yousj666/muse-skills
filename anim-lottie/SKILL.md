---
name: anim-lottie
description: Lottie Web（airbnb/lottie-web）包装技能：播放 After Effects 经 Bodymovin 导出的 Lottie JSON 矢量动画。在动画视频流水线里属于「动起来＋资产播放」环节。用现成 Lottie 资产（图标动效、加载动画、贴纸）做视频或网页时用。
---

# Lottie Web — AE 矢量动画播放器

一句话：设计师在 AE 里做好的矢量动画导出成一个 JSON，这个库负责在网页里原样播出来。

- 仓库：https://github.com/airbnb/lottie-web（JavaScript，约 32.5k stars）
- 流水线位置：动起来（资产播放）。它只播不做，资产来自 AE 导出或 LottieFiles 等资产站。

## 安装与调用

```bash
npm install lottie-web    # 版本 5.13.0
```

最小骨架：

```js
import lottie from 'lottie-web';

const anim = lottie.loadAnimation({
  container: document.getElementById('stage'),
  renderer: 'svg',          // svg / canvas / html
  loop: false,
  autoplay: false,          // 逐帧导出时关掉自动播，用 goToAndStop 定位
  path: 'animation.json',   // 或 animationData: {...}
});
anim.goToAndStop(42, true); // 定位到第 42 帧（逐帧截图导出用）
```

## 注意事项

- 逐帧导出视频：关 autoplay，用 `goToAndStop(frame, true)` 逐帧定位＋无头 Chromium 截图＋ffmpeg 合成，帧精确。
- 资产质量取决于 AE 导出设置；带表达式/遮罩的复杂合成可能有兼容差异，先小样验证再批量用。
- Remotion 里用 Lottie 资产另有官方路线，见同仓库 `remotion-markup` 技能里的 lottie.md。
