---
name: anim-proton
description: Proton（drawcall/Proton，npm 包名 proton-engine）包装技能：JS 粒子动画引擎，发射器＋行为（重力、吸引、碰撞、透明度）的组合式粒子系统。在动画视频流水线里属于「动起来」环节的特效层。做粒子背景、火花、星尘、爆炸类特效时用。
---

# Proton — 粒子特效引擎

一句话：定义「粒子从哪生、活多久、受什么力、怎么死」，成千上万个粒子自己就演起来了。

- 仓库：https://github.com/drawcall/Proton（JavaScript，约 2.5k stars）
- 流水线位置：动起来（特效）。常叠在 Two.js/Konva/Three.js 场景之上做氛围与爆点。

## 安装与调用

```bash
npm install proton-engine    # 版本 7.1.5，注意包名不是 proton
```

最小骨架（Canvas 渲染器）：

```js
import Proton from 'proton-engine';

const proton = new Proton();
const emitter = new Proton.Emitter();
emitter.rate = new Proton.Rate(new Proton.Span(10, 20), new Proton.Span(0.1, 0.25));
emitter.addInitialize(new Proton.Mass(1));
emitter.addInitialize(new Proton.Life(2, 4));
emitter.addInitialize(new Proton.Position(new Proton.CircleZone(0, 0, 10)));
emitter.addInitialize(new Proton.Velocity(new Proton.Span(1, 3), new Proton.Span(0, 360), 'polar'));
emitter.addBehaviour(new Proton.Alpha(1, 0));
emitter.addBehaviour(new Proton.Gravity(0.5));
emitter.p.x = 640; emitter.p.y = 360;
emitter.emit();
proton.addEmitter(emitter);
proton.addRenderer(new Proton.CanvasRenderer(canvas));
(function loop() { proton.update(); requestAnimationFrame(loop); })();
```

## 注意事项

- 粒子贴图（Body）可省略用默认圆点，也可传入图片 URL 做火花/雪花质感。
- 逐帧导出时用 `proton.update(1/30)` 手动步进固定帧长，别依赖真实时间。
- 版本间 API 大体稳定，但细节以官方 demo 为准；粒子数上万时注意性能，先压测再定量。
