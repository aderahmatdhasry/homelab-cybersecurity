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


## HTTP TRACE Method Enabled

- Target: `http://192.168.128.2/`
- Method: `TRACE`
- Result: HTTP 200 OK
- Content-Type: `message/http`

### Finding

The HTTP TRACE method is enabled on the Apache web server. The server reflects the HTTP request back to the client.

### Security Impact

An enabled TRACE method may increase the attack surface and has historically been associated with Cross-Site Tracing (XST) attacks.

### Recommendation

Disable the HTTP TRACE method unless it is explicitly required.


## Apache MultiViews Enabled

- Target: `http://192.168.128.2/index`
- Result: `/index` resolves to `index.php`
- HTTP Status: 200 OK

### Finding

Apache MultiViews/content negotiation is enabled. A request to `/index` is resolved to `index.php`, as indicated by the `Content-Location`, `Vary`, and `TCN` response headers.

### Security Impact

MultiViews can make resource discovery easier by allowing requests without explicit file extensions to resolve to available resources.

### Recommendation

Disable MultiViews if it is not required by the application.


## vsFTPd 2.3.4 Vulnerability Validation

- Target: `192.168.128.2`
- Service: FTP
- Port: `21`
- Version: `vsFTPd 2.3.4`
- Vulnerability: `CVE-2011-2523`
- Metasploit Module: `exploit/unix/ftp/vsftpd_234_backdoor`

### Validation

The FTP service was manually validated using Netcat.

The vsFTPd 2.3.4 backdoor was triggered through the FTP service, resulting in a command shell being exposed on TCP port `6200`.

### Evidence

The obtained shell returned:

- `whoami` → `root`
- `id` → `uid=0(root) gid=0(root)`
- `uname -a` → `Linux metasploitable 2.6.24-16-server ... i686 GNU/Linux`

This confirms remote command execution with root privileges on the target.

### Security Impact

Successful exploitation provides remote command execution with root-level privileges.

This could allow an attacker to fully compromise the vulnerable system.

### Recommendation

Upgrade or remove the vulnerable vsFTPd version and ensure vulnerable FTP services are not exposed to untrusted networks.
