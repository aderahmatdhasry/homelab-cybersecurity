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


# Scanning & Enumeration

## Gobuster

- Tool: Gobuster 3.8.2
- Mode: Directory enumeration
- Target: `http://192.168.128.2`
- Wordlist: `/usr/share/wordlists/dirb/common.txt`

### Key Findings

- `/phpinfo.php` → HTTP 200
- `/phpMyAdmin/` → HTTP 301
- `/dav/` → HTTP 301
- `/twiki/` → HTTP 301
- `/test/` → HTTP 301
- `/server-status` → HTTP 403

## PHPInfo Enumeration

- Target: `http://192.168.128.2/phpinfo.php`
- Result: HTTP 200
- PHP Version: `5.2.4-2ubuntu5.10`
- OS: Linux Ubuntu
- Kernel: `2.6.24-16-server`
- Server API: CGI/FastCGI

### Finding

The exposed `phpinfo()` page discloses detailed PHP and server configuration information.

### Security Impact

An attacker can use the disclosed information to fingerprint the server and identify potential attack surface.
