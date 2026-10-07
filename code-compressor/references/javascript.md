# JavaScript 压缩指南

## 基础压缩
```bash
terser input.js -o output.min.js -c -m
```

## 完整优化（含顶层死代码删除）
```bash
terser input.js -o output.min.js -c -m --toplevel
```

## 可读模式（默认）
压缩后按语句换行，保留可读性：
```bash
terser input.js -o tmp.js -c -m --toplevel
python3 -c "
import re
c = open('tmp.js').read().strip()
c = c.replace(';', ';\n')
c = re.sub(r'\n\s*\n+', '\n', c)
open('output.min.js','w').write(c)
"
```

## 选项说明
- `-c` / `--compress`: 启用压缩（删除死代码、合并变量等）
- `-m` / `--mangle`: 混淆变量名（缩短）
- `--toplevel`: 删除顶层未使用的函数/变量
- `--source-map`: 生成 source map 用于调试
