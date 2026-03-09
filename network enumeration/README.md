# Network Enumeration Lab (Kali Linux → Ubuntu)

## Overview

This lab demonstrates network reconnaissance techniques used during the initial phase of a security assessment.
Using Kali Linux as the attacker machine, I enumerated services running on an Ubuntu server.

The objective was to identify:

* Active hosts
* Open ports
* Running services
* Service versions
* Operating system details

---

## Lab Environment

| System     | Role     | OS           |
| ---------- | -------- | ------------ |
| Kali Linux | Attacker | Kali 2024    |
| Ubuntu VM  | Target   | Ubuntu 22.04 |

Both machines were connected via a Host-Only virtual network.

---

## Target Information

```
Target IP: 192.168.01.204
```

Services installed on the Ubuntu machine:

* OpenSSH
* Apache2
* vsftpd

---

## Tools Used

* Nmap
* Linux networking tools

---

## Step 1 — Host Discovery

Command used:

```
nmap -sn 192.168.01.204
```

Result:

The Ubuntu machine was identified as an active host.

---

## Step 2 — Port Scanning

Command used:

```
nmap 192.168.01.204
```

Open ports discovered:

| Port | Service |
| ---- | ------- |
| 21   | FTP     |
| 22   | SSH     |
| 80   | HTTP    |

---

## Step 3 — Service Enumeration

Command used:

```
nmap -sV 192.168.01.204
```

Results showed the following software versions:

* vsftpd 3.0.3
* OpenSSH 8.9
* Apache 2.4.52

---

## Step 4 — Operating System Detection

Command used:

```
nmap -O 192.168.01.204
```

Nmap identified the system as a Linux-based operating system.

---

## Security Analysis

The following services may represent potential attack vectors:

### SSH (Port 22)

Commonly targeted for brute-force attacks.

Mitigation:

* Disable root login
* Implement Fail2Ban
* Use SSH key authentication.

### FTP (Port 21)

FTP can expose credentials if not properly secured.

Mitigation:

* Disable anonymous login
* Use SFTP instead.

### HTTP (Port 80)

Web servers may expose vulnerabilities if outdated.

Mitigation:

* Maintain regular patching
* Implement web application firewalls.

---

## Conclusion

This lab demonstrates how attackers gather information about target systems during the reconnaissance phase.
Even simple scans reveal valuable details about system architecture and potential vulnerabilities.

Understanding this process helps defenders better monitor networks and detect malicious scanning activity.

