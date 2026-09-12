# Metasploitable 2 Pentesting Lab

A controlled cybersecurity lab for practicing penetration testing and vulnerability assessment against the intentionally vulnerable Metasploitable 2 virtual machine.

## Objective

The objective of this lab is to practice the basic penetration testing methodology in an isolated virtual environment:

- Network configuration and isolation
- Reconnaissance and service enumeration
- Web enumeration
- Vulnerability identification
- Manual vulnerability validation
- Exploitation
- Security impact analysis
- Mitigation recommendations

## Lab Environment

| Component | Role |
|---|---|
| Kali Linux | Attacker |
| Metasploitable 2 | Vulnerable Target |
| UTM | Virtualization Platform |
| Network | Host-Only / Isolated |

## Network

```text
Kali Linux
192.168.128.3
     |
     | Host-Only Network
     |
Metasploitable 2
192.168.128.2
```

The target VM was isolated from external networks to ensure that all testing was performed within the controlled lab environment.

## Methodology

The assessment followed this workflow:

```text
Lab Setup
    ↓
Reconnaissance
    ↓
Service Enumeration
    ↓
Vulnerability Identification
    ↓
Manual Validation
    ↓
Exploitation
    ↓
Impact Analysis
    ↓
Mitigation
```

## Key Findings

The assessment identified several security issues, including:

- Outdated Apache and PHP versions
- Exposed `phpinfo()` page
- Directory indexing
- Exposed phpMyAdmin interface
- HTTP TRACE method enabled
- Apache MultiViews enabled
- Vulnerable vsFTPd 2.3.4 service

The vsFTPd 2.3.4 backdoor vulnerability was manually validated and resulted in remote command execution with root privileges within the isolated lab.

## Repository Structure

```text
├── lab-setup/
│   ├── kali-linux/
│   ├── metasploitable/
│   ├── network/
│   └── scanning/
│
├── exploitation/
│   ├── README.md
│   └── vsftpd-cve-2011-2523.png
│
└── README.md
```

## Disclaimer

This project was conducted exclusively against an intentionally vulnerable virtual machine in an isolated lab environment for educational purposes.

Do not perform security testing against systems without explicit authorization.
