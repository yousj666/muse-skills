---
name: "server-health"
description: "Check health of Beijing and US servers: CPU, memory, disk, key services. Use when user asks about server status, why server is slow, or after a crash."
---

# Server Health Check

## Purpose
Quickly diagnose Beijing (120.48.25.99) and US (104.249.156.137) server health.

## Workflow
User runs these via Termux (`bj` for Beijing, `us` for US via ProxyJump).

### Quick check (one-liner)
```bash
echo "=== CPU ==="; uptime; echo "=== MEM ==="; free -m | head -2; echo "=== DISK ==="; df -h / | tail -1; echo "=== SERVICES ==="; systemctl is-active mail-relay-143 mail-relay-2525 anytls-relay-8443 2>/dev/null || systemctl is-active postfix dovecot 2>/dev/null
```

### Thresholds
- **Memory**: Available < 100MB = warning, < 60MB = critical (softdog reboots at 60MB)
- **Disk**: Use > 85% = warning, > 95% = critical
- **Load**: 1-min load > CPU cores = high load

### Key services
**Beijing** (120.48.25.99):
- `mail-relay-143` — IMAP relay to US
- `mail-relay-2525` — SMTP relay to US
- `anytls-relay-8443` — AnyTLS proxy to US:443
- `xray` — check if needed

**US** (104.249.156.137):
- `postfix` — mail sending
- `dovecot` — mail receiving
- `xray` — proxy

## Operating Rules
- Assistant cannot SSH directly (sandbox proxy blocks); user runs via Termux.
- If memory is low, check what's eating it: `ps aux --sort=-%mem | head -10`
- If disk is full, check: `du -sh /* 2>/dev/null | sort -hr | head -10`
- Do not restart services without user confirmation.
- See `references/` for detailed troubleshooting.
