---
name: "mail-relay-monitor"
description: "Check if mail relay and mail server ports are reachable. Use when user asks about email status, mail server health, or why email isn't working."
---

# Mail Relay Monitor

## Purpose
Quickly diagnose mail connectivity by checking if key ports are open on Beijing relay (120.48.25.99) and US mail server (104.249.156.137).

## Workflow
1. Check Beijing relay ports (143 IMAP, 2525 SMTP, 8443 AnyTLS):
   ```bash
   for p in 143 2525 8443; do timeout 5 bash -c "echo > /dev/tcp/120.48.25.99/$p" 2>/dev/null && echo "$p OK" || echo "$p FAIL"; done
   ```
2. Check US mail server ports (25 SMTP, 587 Submission, 993 IMAPS, 143 IMAP):
   ```bash
   for p in 25 587 993 143; do timeout 5 bash -c "echo > /dev/tcp/104.249.156.137/$p" 2>/dev/null && echo "$p OK" || echo "$p FAIL"; done
   ```
3. If Beijing 143 FAILs but service is running, check ufw:
   ```bash
   # User runs on Beijing via Termux `bj`:
   ufw status | grep -E "143|2525|8443"
   ```
4. Report which segment is broken:
   - Beijing ports FAIL → firewall (ufw) or socat relay down
   - US ports FAIL → Postfix/Dovecot down or network issue
   - All OK → problem is client config or DNS

## Operating Rules
- Run port checks from sandbox first (fast, no auth needed).
- If Beijing ports fail, ask user to run ufw check via `bj` in Termux.
- Do not restart services without user confirmation.
- DNS may resolve mail.yousj.cc to 198.18.x.x (sandbox blackhole); always use direct IPs for port checks.
