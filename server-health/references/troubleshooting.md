# Troubleshooting

## High memory
```bash
ps aux --sort=-%mem | head -10
```
Look for runaway processes. Common culprits: Baota panel, Python scripts.

## High disk
```bash
du -sh /* 2>/dev/null | sort -hr | head -10
du -sh /var/log/* 2>/dev/null | sort -hr | head -5
```
Clear old logs: `journalctl --vacuum-time=7d`

## Service won't start
```bash
systemctl status <service> --no-pager | head -20
journalctl -u <service> --no-pager | tail -20
```

## After force reboot
1. Check all relay services are active
2. Check ufw rules survived: `ufw status | grep -E "143|2525|8443"`
3. Test relay: `timeout 5 bash -c 'echo > /dev/tcp/120.48.25.99/143' && echo OK`
