---
name: anim-motion-canvas
description: Motion Canvas（motion-canvas/motion-canvas）包装技能：用 TypeScript 代码写图解/讲解动画（场景、信号、生成器时间线），适合把概念、流程、公式讲清楚的动画视频。在动画视频流水线里属于「制作＋编排」环节。做图解动画、讲解视频时用。
---

# Motion Canvas — 代码图解动画

一句话：用代码声明场景、用生成器（generator）写时间线的讲解动画框架，专为「把想法可视化」而生。

- 仓库：https://github.com/motion-canvas/motion-canvas（TypeScript，约 19.9k stars）
- 流水线位置：制作＋编排。时间线是代码本身，改参数即改片。

## 安装与调用

```bash
npm init @motion-canvas@latest my-project   # 脚手架（含 @motion-canvas/core、2d、ui、vite-plugin）
cd my-project && npm install
npm start                                    # 打开编辑器预览/导出
```

核心包版本：`@motion-canvas/core` 3.17.2。

最小场景骨架（`src/scenes/example.tsx`）：

```tsx
import {makeScene2D, Circle, Txt} from '@motion-canvas/2d';
import {all, createRef} from '@motion-canvas/core';

export default makeScene2D(function* (view) {
  const circle = createRef<Circle>();
  view.add(<Circle ref={circle} size={140} fill={'#e13238'} />);
  yield* all(circle().size(280, 1), circle().fill('#ffa726', 1));
});
```

## 注意事项

- 导出 MP4 走它自带的 FFmpeg 导出器（编辑器内渲染）；无头批量渲染不是开箱即用，做正式片前先用小样验证导出链路。
- 动画逻辑全是 `yield*` 生成器，帧精确、可复现，适合数据/概念讲解；不适合做角色表演类动画。
- 与 Remotion 二选一即可：讲解图解选 Motion Canvas，React 生态拼装成片选 Remotion。
