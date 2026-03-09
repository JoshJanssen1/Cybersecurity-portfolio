# Findings: Network Enumeration Lab (Kali → Ubuntu)

## Overview
This lab used Kali Linux to perform network reconnaissance on an Ubuntu VM.  
The goal was to identify active hosts, open ports, running services, and the operating system, providing insight into potential attack surfaces.

The Ubuntu VM was configured with SSH, FTP, and Apache web server to simulate a small server environment.  

---

## 1. Open Ports and Services

| Port | Service | Version | Security Notes / Risk |
|------|---------|---------|----------------------|
| 21   | FTP     | vsftpd 3.0.3 | Transmits credentials in plaintext. Risk of unauthorized access if anonymous login is enabled. Consider using SFTP or disabling FTP entirely. |
| 22   | SSH     | OpenSSH 8.9 | Allows remote login. Risk of brute-force attacks if strong passwords or key authentication are not enforced. Root login should be disabled. |
| 80   | HTTP    | Apache 2.4.52 | Exposed web server may have outdated components or misconfigurations. Potential web vulnerabilities (directory traversal, XSS, etc.). Keep software updated and configure security headers. |

---

## 2. Operating System and Network Observations

- Ubuntu VM detected as **Linux kernel 5.x**.  
- OS information is critical for attackers to select applicable exploits or tools.  
- Host responded to ICMP ping, indicating network visibility.  
- All services were reachable from Kali, showing no firewall restrictions between the VMs.

---

## 3. Potential Vulnerabilities / Risks

1. **SSH (Port 22)**  
   - Risk: Brute-force attacks possible if weak passwords are used.  
   - Mitigation: Disable root login, enforce key-based authentication, and configure Fail2Ban to block repeated failed attempts.

2. **FTP (Port 21)**  
   - Risk: Plaintext credentials and anonymous login vulnerability.  
   - Mitigation: Disable anonymous login, enable SFTP, or replace FTP with a secure alternative.

3. **HTTP (Port 80)**  
   - Risk: Exposed web server may allow information leakage or web attacks.  
   - Mitigation: Keep Apache up-to-date, configure security headers, and monitor logs for suspicious activity.

---

## 4. Key Takeaways

- Network enumeration reveals all publicly available services and version information without interacting with application logic.  
- Even simple scans expose critical system information that can be exploited if left unmonitored.  
- Documenting findings in a structured manner turns raw scan results into actionable security intelligence.  
- Understanding service exposure helps defenders anticipate attacker techniques and implement monitoring or mitigation.

---

## 5. References / Evidence

- Raw scan results: `scans/nmap_scan.txt`  
- Screenshots: `screenshots/nmap_results.png`, `screenshots/ubuntu_services.png`  
- Lab setup: Kali Linux (Attacker) → Ubuntu VM (Target) on Host-Only Virtual Network  

---

*This lab demonstrates the importance of reconnaissance in cybersecurity. Proper documentation and analysis of network enumeration can help organizations proactively secure their infrastructure.*
