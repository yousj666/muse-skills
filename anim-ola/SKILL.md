---
name: anim-ola
description: Ola（franciscop/ola）包装技能：实时数值平滑插值小库，让数字、坐标、仪表读数像被弹簧牵着一样平滑追赶目标值。在动画视频流水线里属于「动起来」环节的数值层。做数据动画、计数器、图表动态数值时用。
---

# Ola — 数值平滑插值

一句话：你只管不断改目标值，它负责让当前值平滑地追上去，天生适合跳动的数字和仪表。

- 仓库：https://github.com/franciscop/ola（JavaScript，约 1.8k stars）
- 流水线位置：动起来（数值层）。常和 Canvas/图表/Three.js 搭配。

## 安装与调用

```bash
npm install ola    # 版本 1.2.2
```

最小骨架：

```js
import Ola from 'ola';

const pos = Ola({y: 0, value: 0});   // 被追踪的数值组
pos.y = 300;                          // 随时改目标，越频繁越平滑
pos.value = 98.6;

function frame() {
  draw(pos.y, pos.value.toFixed(1));  // 每帧读当前平滑值去画
  requestAnimationFrame(frame);
}
frame();
```

## 注意事项

- 只有数值插值，不碰 DOM、不管渲染；要配合自己的绘制循环。
- 追赶速度由内部插值时长决定，高频改目标时最平滑；一次性跳变会有一个平滑过程，不是瞬移。
- 体积极小，适合塞进数据新闻、实时仪表、计分牌类动画。
