# Week 3 – Advanced Exploitation & Full VAPT Cycle
### Vulnerability Assessment & Penetration Testing (VAPT) Internship

![Status](https://img.shields.io/badge/Status-Completed-success)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue)
![Target](https://img.shields.io/badge/Target-Metasploitable%202-red)
![Methodology](https://img.shields.io/badge/Standard-PTES%20%7C%20OWASP-orange)

---

## 📌 Overview
This repository contains the deliverables for **Week 3** of the VAPT internship. The focus of this module is **Advanced Exploitation Techniques** and the execution of a **Full VAPT Lifecycle** within a controlled laboratory environment.

The assessment demonstrates proficiency in:
* Multi-stage exploit chaining.
* Customization of public exploits.
* Web application penetration testing (OWASP Top 10).
* Post-exploitation and forensic evidence collection.
* Professional reporting aligned with **PTES** and **OWASP WSTG** standards.

> **⚠️ Disclaimer:** All testing was conducted with explicit authorization on intentionally vulnerable systems for educational purposes only.

---

## 🎯 Objectives
* **Simulate Advanced Attacks:** Chain web vulnerabilities to achieve full system compromise (Web → RCE).
* **Custom Exploitation:** Modify public `Exploit-DB` Proof-of-Concepts (PoCs) to fit specific target environments.
* **Web App Security:** Perform manual and automated testing on DVWA.
* **Post-Exploitation:** Escalate privileges to root and capture forensic evidence.
* **Reporting:** Map findings to PTES phases and produce executive/technical reports.

---

## 🧭 Methodology & Standards
The assessment followed industry-standard frameworks:
* **PTES** (Penetration Testing Execution Standard)
* **OWASP WSTG** (Web Security Testing Guide)
* **OWASP Top 10** (2021 Edition)
* **CVSS v4.0** for Risk Scoring
* **NIST SP 800-115** (Reference Guidance)

---

## 🛠 Tools Used

| Category | Tools |
| :--- | :--- |
| **Operating System** | Kali Linux |
| **Reconnaissance** | WHOIS, Sublist3r, WhatWeb |
| **Scanning** | OpenVAS (Greenbone), Nmap, Nikto |
| **Exploitation** | Metasploit Framework, Exploit-DB, SQLMap, Burp Suite |
| **Post-Exploitation** | Meterpreter, Wireshark, Hashcalc (SHA256) |

---

## 🎯 Target Environment

| Component | Details |
| :--- | :--- |
| **Primary Target** | Metasploitable 2 |
| **Target IP** | `192.168.56.105` |
| **Web Application** | DVWA (Damn Vulnerable Web App) |
| **Simulation Context** | Internal / Host-only Lab Network |
| **Attack Scenario** | Legacy Samba & Web App Compromise |

---

## 🔐 Key Activities Performed

### 1️⃣ Advanced Exploitation Lab
* **Exploit Chain:** Stored XSS $\rightarrow$ Session Hijacking $\rightarrow$ Tomcat Manager Access $\rightarrow$ WAR Upload $\rightarrow$ **RCE**.
* **Payload:** `java/meterpreter/reverse_tcp`
* **Customization:** Modified a Python PoC for **vsftpd 2.3.4 (CVE-2011-2523)** to replace a benign check with a functional reverse shell.
* **Impact:** Full Remote Code Execution on the target server.

### 2️⃣ Web Application Testing Lab (DVWA)
* Identified **SQL Injection** vulnerabilities using manual payloads and **SQLMap**.
* Exploited **Reflected XSS** to demonstrate client-side risks.
* Analyzed session handling using **Burp Suite** (captured `PHPSESSID` exposure).
* Mapped findings to the **OWASP Top 10**.

### 3️⃣ Reporting Practice
* Developed a **Findings Table** with CVSS risk scoring.
* Created **Attack Path Visualizations** (Draw.io) to illustrate the kill chain.
* Drafted both **Technical Findings** for developers and **Executive Briefings** for management.

### 4️⃣ Post-Exploitation & Evidence Collection
* **Privilege Escalation:** Escalated from low-level user to `root` using the **Linux udev_netlink** exploit.
* **Session Management:** Maintained persistence via Meterpreter.
* **Forensics:** Captured network traffic with **Wireshark** and verified evidence integrity using **SHA256 hashing**.

### 5️⃣ Capstone – Full VAPT Cycle
* **Detection:** Identified vulnerabilities using **OpenVAS**.
* **Exploitation:** Confirmed and exploited **Samba Username Map Script RCE (CVE-2007-2447)**.
* **Execution:** Gained root access using the Metasploit module `multi/samba/usermap_script`.
* **Remediation:** Provided actionable patching and configuration recommendations.

---

## 📊 Notable Findings

| Severity | Vulnerability | CVE / Type |
| :--- | :--- | :--- |
| 🔴 **Critical** | Samba Username Map Script RCE | CVE-2007-2447 |
| 🔴 **Critical** | SQL Injection (Blind & Boolean) | Injection (A03:2021) |
| 🟠 **High** | VSFTDP Backdoor Command Execution | CVE-2011-2523 |
| 🟡 **Medium** | Reflected Cross-Site Scripting (XSS) | Injection (A03:2021) |

---




