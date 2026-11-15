---
name: anim-godot
description: Godot（godotengine/godot）调用路线技能：开源 2D/3D 游戏引擎，自带动画编辑器与补间系统，还有官方 Movie Maker 模式可直接把场景录成视频。本技能只写用途与调用路线，不下载安装本体。在动画视频流水线里属于「制作＋导出」环节。做游戏式场景、可交互动画、需要时间轴编辑器的动画时用。
---

# Godot — 游戏引擎做动画（仅文档路线）

一句话：把动画当游戏场景来做——AnimationPlayer 管时间轴，Tween 管补间，还能一键把运行画面录成视频文件。

- 仓库：https://github.com/godotengine/godot（C++ 引擎源码，约 120k stars；仓库是源码，**不要 clone 当安装包**，用官网发行版二进制）
- 流水线位置：制作＋导出。Movie Maker 模式让它能脱离「游戏」身份直接产出视频。

## 调用路线（需要时安装官方发行版）

```bash
# Movie Maker：把工程运行过程逐帧录成视频（Godot 4 官方功能）
godot --write-movie out.avi --fixed-fps 30 --path ./my_project

# 无头导出/检查工程
godot --headless --export-release "Linux" ./build/game
```

GDScript 补间骨架（场景脚本）：

```gdscript
extends Node2D

func _ready() -> void:
    var tween := create_tween().set_loops()
    tween.tween_property($Sprite2D, "position:x", 800.0, 1.2).from(100.0)
    tween.tween_property($Sprite2D, "modulate:a", 0.2, 0.6)
```

关键帧动画用 AnimationPlayer 节点在编辑器里打关键帧，或代码 `Animation` 资源动态生成轨道。

## 注意事项

- `--write-movie` 输出 AVI/MJPEG 体积大，录完用 ffmpeg 转 MP4；录制是逐帧确定性的，适合无头出片。
- 引擎本体约百 MB 级，装前确认磁盘空间充足；本技能只提供调用路线，不负责自动安装。
- 只是网页里放个 3D/2D 动效时别动用它——Three.js/Anime.js 更轻；需要完整场景编辑器和时间轴时才值得。
