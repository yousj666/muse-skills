---
name: anim-manim
description: Manim（ManimCommunity/manim）包装技能：Python 数学动画框架，写代码生成公式推导、几何图形、函数图像动画（3Blue1Brown 同款）。在动画视频流水线里属于「制作＋导出」一体环节。做数学/物理讲解动画时用。
---

# Manim — 数学动画框架

一句话：用 Python 描述数学对象和变换，它直接渲染出讲解级 MP4——公式、图形、坐标系天生就是主角。

- 仓库：https://github.com/ManimCommunity/manim（Python，约 42.6k stars）
- 流水线位置：制作＋导出一体。自带渲染管线，出片不依赖浏览器。

## 安装与调用

```bash
python3 -m venv .venv-manim
.venv-manim/bin/pip install manim     # 依赖 cairo/pango 系统库，构建较重，预留磁盘空间与时间
.venv-manim/bin/manim -qm scene.py HelloScene    # -qm = 中等画质快速验证，正式出片用 -qh
```

最小骨架（`scene.py`）：

```python
from manim import *

class HelloScene(Scene):
    def construct(self):
        title = Text("Hello, Manim")
        formula = MathTex(r"e^{i\pi} + 1 = 0")
        self.play(Write(title))
        self.play(Transform(title, formula))
        self.wait(0.5)
```

产物在 `media/videos/scene/<quality>/HelloScene.mp4`。

## 注意事项

- 安装较重：依赖 cairo/pango 系统开发库，构建耗时且占用磁盘空间，装前先确认系统库齐备、空间充足，并预留构建时间。
- MathTex 需要 LaTeX 环境（texlive）才能渲染公式；纯图形/Text 场景可先绕开。
- 与 Motion Canvas 分工：纯数学推导选 Manim，通用图解讲解选 Motion Canvas。
