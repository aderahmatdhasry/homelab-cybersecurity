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


## Directory Indexing

- Target: `http://192.168.128.2/doc/`
- Result: Directory listing exposed
- HTTP Status: 200 OK

### Finding

The `/doc/` directory allows directory listing, exposing the names of files and directories to unauthenticated users.

### Security Impact

Directory indexing can disclose information about installed packages, server components, and directory structure. This information may help an attacker fingerprint the system and identify potential attack surfaces.

### Security Impact


## Directory Indexing - /icons/

- Target: `http://192.168.128.2/icons/`
- Result: Directory listing exposed
- HTTP Status: 200 OK

### Finding

The `/icons/` directory allows directory listing, exposing files and resources to unauthenticated users.

### Security Impact

The exposed directory primarily contains Apache default icon resources. While the direct impact is low, directory indexing can disclose server structure and should generally be disabled when not required.

An attacker can use the disclosed information to fingerprint the server and identify potential attack surface.


## phpMyAdmin Exposure

- Target: `http://192.168.128.2/phpMyAdmin/`
- Result: phpMyAdmin login interface exposed
- HTTP Status: 200 OK

### Finding

The phpMyAdmin administrative interface is accessible through the web server and exposes a login interface to unauthenticated users.

### Security Impact

Exposing database administration interfaces increases the attack surface. If authentication or access controls are weak, an attacker may attempt to gain unauthorized access to the underlying database.

### Recommendation

Restrict access to phpMyAdmin using network controls, authentication, or an allowlist of authorized hosts.
