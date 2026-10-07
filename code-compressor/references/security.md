# 安全红线

压缩时**绝不删除**以下代码，即使看起来"没用"：

1. 输入验证（validate、sanitize、escape）
2. 权限检查（auth、authorize、isAdmin）
3. CSRF/XSS 防护
4. 速率限制
5. 加密/哈希调用
6. 安全 headers 设置

如不确定某段代码是否安全相关，保留它。
