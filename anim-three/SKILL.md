---
name: anim-three
description: Three.js（mrdoob/three.js）包装技能：最主流的 WebGL 3D 库，场景/相机/光影/模型/后期全套。在动画视频流水线里属于「制作」环节的 3D 主力。做 3D 场景动画、产品旋转展示、数据可视化 3D 时用。
---

# Three.js — WebGL 3D 主力

一句话：网页 3D 的事实标准——从旋转的产品模型到完整的 3D 短片场景，都在这一套里。

- 仓库：https://github.com/mrdoob/three.js（JavaScript，约 118k stars）
- 流水线位置：制作（3D）。Remotion 里做 3D 片段也多是嵌它（见同仓库 remotion-markup 技能的 3d.md）。

## 安装与调用

```bash
npm install three    # 版本 0.187.0
```

最小骨架：

```js
import * as THREE from 'three';

const renderer = new THREE.WebGLRenderer({antialias: true, preserveDrawingBuffer: true});
renderer.setSize(1280, 720);
document.body.appendChild(renderer.domElement);

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, 1280 / 720, 0.1, 1000);
camera.position.set(0, 2, 8);
scene.add(new THREE.DirectionalLight(0xffffff, 2));
const cube = new THREE.Mesh(new THREE.BoxGeometry(2, 2, 2), new THREE.MeshStandardMaterial({color: 0xe13238}));
scene.add(cube);

// 逐帧导出：固定步进，不用真实时钟
for (let f = 0; f < 90; f++) {
  cube.rotation.y = f * 0.02;
  renderer.render(scene, camera);
  saveFrame(renderer.domElement.toDataURL(), f);   // 存 PNG 后 ffmpeg 合成 MP4
}
```

## 注意事项

- 出视频必须固定步进逐帧渲染，别用 requestAnimationFrame 的真实时间，否则帧率漂移、画面抖。
- 无头 Chromium 里的 WebGL 通常走软件渲染，复杂场景会慢；先小分辨率验证再上正式尺寸。
- 模型加载（GLTF）用 `three/addons/loaders/GLTFLoader.js`；后期合成用 EffectComposer（同在 addons）。
