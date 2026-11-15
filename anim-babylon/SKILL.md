---
name: anim-babylon
description: Babylon.js（BabylonJS/Babylon.js）包装技能：功能完整的 WebGL 游戏/渲染引擎，自带动画系统、物理、粒子与场景编辑器。在动画视频流水线里属于「制作」环节的 3D 引擎层。做较重的 3D 场景、需要现成动画混合与编辑器生态时用。
---

# Babylon.js — 全功能 WebGL 引擎

一句话：Three.js 是库，Babylon.js 是引擎——动画混合、粒子、物理、Inspector 调试工具一整套都配齐了。

- 仓库：https://github.com/BabylonJS/Babylon.js（TypeScript，约 26.4k stars）
- 流水线位置：制作（3D）。适合场景较重、要现成动画系统的 3D 片段。

## 安装与调用

```bash
npm install @babylonjs/core    # 版本 9.36.0
```

最小骨架：

```js
import {Engine, Scene, ArcRotateCamera, Vector3, HemisphericLight, MeshBuilder, Animation} from '@babylonjs/core';

const engine = new Engine(canvas, true);
const scene = new Scene(engine);
const camera = new ArcRotateCamera('cam', Math.PI / 2, Math.PI / 3, 10, Vector3.Zero(), scene);
scene.addLight(new HemisphericLight('light', new Vector3(0, 1, 0), scene));
const box = MeshBuilder.CreateBox('box', {size: 2}, scene);

const anim = new Animation('spin', 'rotation.y', 30, Animation.ANIMATIONTYPE_FLOAT, Animation.ANIMATIONLOOPMODE_CYCLE);
anim.setKeys([{frame: 0, value: 0}, {frame: 90, value: Math.PI * 2}]);
box.animations.push(anim);
scene.beginAnimation(box, 0, 90, true);
engine.runRenderLoop(() => scene.render());
```

## 注意事项

- 与 Three.js 二选一：轻量嵌片选 Three.js，要引擎级功能（动画混合、现成粒子、Inspector）选 Babylon.js。
- 逐帧导出同样用固定步进：停掉 runRenderLoop，手动逐帧 `scene.render()` 后抓 canvas 像素。
- 包体积大，无头软件渲染时控制场景复杂度。
