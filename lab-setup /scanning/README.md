# Scanning & Enumeration

## Gobuster

- Tool: Gobuster 3.8.2
- Mode: Directory enumeration
- Target: http://192.168.128.2
- Wordlist: /usr/share/wordlists/dirb/common.txt

### Key Findings

- `/phpinfo.php` → HTTP 200
- `/phpMyAdmin/` → HTTP 301
- `/dav/` → HTTP 301
- `/twiki/` → HTTP 301
- `/test/` → HTTP 301
- `/server-status` → HTTP 403
