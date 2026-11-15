---
name: anim-shifty
description: Shifty（jeremyckahn/shifty）包装技能：极轻量高性能 TypeScript 补间引擎，只管数值补间与缓动，不管渲染。在动画视频流水线里属于「动起来」环节的最底层。给自研 Canvas/WebGL 渲染循环配补间时用。
---

# Shifty — 底层补间引擎

一句话：只做一件事——把一组数从 A 平滑补间到 B，每帧把当前值交给你，画什么你自己决定。

- 仓库：https://github.com/jeremyckahn/shifty（TypeScript，约 1.6k stars）
- 流水线位置：动起来（引擎层）。适合给自研渲染器、游戏循环、逐帧导出器当心脏。

## 安装与调用

```bash
npm install shifty    # 版本 3.0.9
```

最小骨架：

```js
import {tween} from 'shifty';

tween({
  from: {x: 0, opacity: 0},
  to: {x: 300, opacity: 1},
  duration: 900,
  easing: 'easeOutQuad',
  render: state => draw(state.x, state.opacity),  // 每帧回调
});
```

链式与编排用 `Tweenable` 实例的 `.then()` / `.play()` / `.pause()` 控制。

## 注意事项

- 没有 DOM 概念、没有时间线 UI，编排复杂场景要自己搭调度；简单补间它比谁都快都稳。
- 逐帧导出视频时可关掉它的内部时钟，改用手动步进到指定毫秒，保证帧精确。
