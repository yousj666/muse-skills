# Python 压缩指南

## 基础
```bash
pip install python-minifier
python-minifier -o output.min.py input.py
```

## 激进模式（重命名全局变量）
```bash
python-minifier --rename-globals -o output.min.py input.py
```

## 注意
- Python 压缩收益不如 JS（解释型，无变量混淆优势）
- 确保测试通过，动态特性（eval、getattr）可能受影响
