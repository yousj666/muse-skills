---
name: "code-compressor"
description: "Compress and minify code: remove whitespace/comments, eliminate dead code, shorten safely. Use when user wants smaller code, asks to minify, or says 'ponytail'."
---

# Code Compressor

## Purpose
Shrink code to minimal size while preserving functionality and security. Removes dead code, strips comments/whitespace, shortens where safe.

## Workflow

### JavaScript/TypeScript
```bash
# Install once
npm install -g terser

# Minify (keeps functionality, removes dead code)
terser input.js -o output.min.js -c -m --toplevel

# Flags: -c=compress, -m=mangle, --toplevel=drop unused top-level
```

### Python
```bash
# Install once
pip install python-minifier

# Minify
python-minifier -o output.min.py input.py

# Aggressive (also renames locals, removes docs)
python-minifier --rename-globals -o output.min.py input.py
```

### CSS
```bash
npm install -g cssnano-cli
cssnano input.css output.min.css
```

### HTML
```bash
npm install -g html-minifier
html-minifier --collapse-whitespace --remove-comments -o output.min.html input.html
```

## Operating Rules
1. **Never change logic**: minification must be behavior-preserving. Test output if possible.
2. **Security first**: do not remove input validation, auth checks, or sanitization even if they look "unused".
3. **Dead code**: remove only provably unreachable code (unused functions, unreachable branches). When unsure, keep it.
4. **Source maps**: for production JS, generate with `--source-map` for debugging.
5. **Keep originals**: never overwrite source files; write to `.min.*` or `dist/`.
6. Ask which language if ambiguous. Default to JS for web code.

## Readable Mode (default)
User prefers compressed but readable output (not single-line). After terser, add line breaks:
```bash
# Minify then format with line breaks after statements
terser input.js -o tmp.min.js -c -m --toplevel
python3 -c "
import re
c = open('tmp.min.js').read().strip()
c = c.replace(';', ';\n')
c = re.sub(r'\n\s*\n+', '\n', c)
open('output.min.js','w').write(c)
"
```
This keeps variable mangling and dead-code removal but breaks lines at statement boundaries.

## File Layout
- `bin/compress` — 一键压缩脚本：`./bin/compress input.js [output.min.js]`
- `references/javascript.md` — JS 压缩详细选项
- `references/python.md` — Python 压缩指南
- `references/security.md` — 安全红线（绝不删除的代码）
- `assets/terser-config.json` — terser 配置模板
