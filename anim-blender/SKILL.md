---
name: anim-blender
description: Blender（blender/blender 官方镜像）调用路线技能：专业 3D 建模/绑定/角色动画软件，本技能只写用途与无头脚本调用路线，不下载安装本体。在动画视频流水线里属于「制作」环节的重型 3D 与角色动画层。需要骨骼绑定、角色表演、电影级渲染时用。
---

# Blender — 重型 3D 与角色动画（仅文档路线）

一句话：这批工具里唯一能做骨骼绑定和角色表演的专业软件；仓库 blender/blender 只是源码镜像，**不要 clone 它当安装包**。

- 仓库：https://github.com/blender/blender（C++ 源码镜像，约 22k stars）
- 流水线位置：制作（重型 3D/角色）。网页引擎（Three.js/Babylon）做不了的骨骼动画、毛发、流体在这里做。

## 调用路线（需要时安装官方发行版）

无头脚本渲染是自动化出片的正道——用 Python（bpy）生成/修改场景，命令行渲染：

```bash
# 渲染已有 .blend 的动画
blender -b scene.blend -o //render/frame_#### -a

# 脚本建场景再渲染
blender -b -P build_scene.py -o //out -a
```

`build_scene.py` 骨架：

```python
import bpy
bpy.ops.wm.read_factory_settings(use_empty=True)
bpy.ops.mesh.primitive_cube_add(location=(0, 0, 1))
cube = bpy.context.active_object
cube.keyframe_insert(data_path="rotation_euler", frame=1)
cube.rotation_euler.z = 6.283
cube.keyframe_insert(data_path="rotation_euler", frame=90)
scene = bpy.context.scene
scene.frame_start, scene.frame_end = 1, 90
scene.render.filepath = "//out.mp4"   # 或输出 PNG 序列后用 ffmpeg 合成（更稳）
```

## 注意事项

- 输出 PNG 序列＋ffmpeg 合成比直出 MP4 更稳、断点可续；Eevee 渲染无显卡时用 CPU 会慢，Cycles 更慢，先低采样验证。
- 安装方式：官网发行版解压即可（约数百 MB），装前先确认磁盘空间充足；本技能只提供调用路线，不负责自动安装。
- 学习成本是这批工具里最高的；没有角色动画需求时，Three.js/Babylon 已够用。
