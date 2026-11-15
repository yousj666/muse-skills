---
name: anim-tweenjs
description: TweenJS（CreateJS/TweenJS）包装技能：链式补间库，一串 .to().wait().to() 把顺序动画写成流水账。在动画视频流水线里属于「动起来」环节。写严格先后顺序的分步动画（教程步骤、演示流程）时用。
---

# TweenJS — 链式顺序补间

一句话：动画是一串命令排队执行——动到哪、等多久、再动到哪，链式写完就是一条时间线。

- 仓库：https://github.com/CreateJS/TweenJS（JavaScript，约 3.6k stars）
- 流水线位置：动起来。强项是「按顺序」的分步演示动画。

## 安装与调用

```bash
npm install @createjs/tweenjs    # 版本 2.0.0-beta.4
```

最小骨架：

```js
import {Tween, Ticker} from '@createjs/tweenjs';

Ticker.timingMode = Ticker.RAF;
const target = {x: 0, y: 0, alpha: 1};
Tween.get(target, {onUpdate: () => draw(target)})
  .to({x: 300}, 400)        // 400ms 移过去
  .wait(200)                // 停 200ms
  .to({y: 120, alpha: 0.3}, 300)
  .call(() => console.log('done'));
```

## 注意事项

- CreateJS 全家桶已进入低维护状态（仓库 2023 年后基本停更），新项目优先 Anime.js/Motion；TweenJS 只在需要它这种链式写法时用。
- npm 包是 beta 标记但 API 已多年稳定；Ticker 要自己接到渲染循环上，别忘了启动。
