---
name: anim-lume
description: LUME（lume/lume）包装技能：用 HTML 自定义元素写 GPU 加速的 2D/3D 场景，像写标签一样摆 3D 物体。在动画视频流水线里属于「制作」环节的 3D 场景层。想快速搭 3D 场景又不想写 Three.js 命令式代码时用。
---

# LUME — 用 HTML 标签做 3D 场景

一句话：`<lume-box>` 就是一个 3D 方块——场景、相机、光影全是 HTML 元素，CSS 式思维摆 3D。

- 仓库：https://github.com/lume/lume（TypeScript，约 1.5k stars，底层基于 Three.js）
- 流水线位置：制作（3D 场景）。适合快速原型和网页 3D 展示。

## 安装与调用

```bash
npm install lume    # 版本 0.3.0-alpha.46（仍是 alpha）
```

最小骨架：

```html
<script type="module">
  import 'lume';  // 注册全部自定义元素
</script>
<lume-scene>
  <lume-camera-rig align-point="0.5 0.5" min-distance="200" max-distance="1000"></lume-camera-rig>
  <lume-point-light intensity="900" position="200 -200 300"></lume-point-light>
  <lume-box id="box" size="120 120 120" align-point="0.5 0.5" mount-point="0.5 0.5 0.5"
            color="#e13238"></lume-box>
</lume-scene>
<script type="module">
  const box = document.getElementById('box');
  (function loop(t) { box.rotation.y = t / 20; requestAnimationFrame(loop); })(0);
</script>
```

## 注意事项

- 仍是 alpha 版本，API 可能变动；正式 3D 项目优先 Three.js/Babylon.js，LUME 只适合快速搭景验证想法。
- 动画靠改元素属性（position/rotation/size 都是响应式属性），配 Motion/Shifty 驱动数值即可。
