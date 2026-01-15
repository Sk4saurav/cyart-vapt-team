# Week 2: VAPT Internship - Laboratory & Capstone Project

**Repository:** cyart-vapt-team
**Folder:** Week 2
**Analyst:** [Your Name]
**Date:** January 2026
**Target Environment:** Metasploitable 2 (Local VM)
**Target IP:** 192.168.56.105

---

## 📌 Project Overview
This repository contains the documentation, logs, and evidence for Week 2 of the VAPT internship. The objective was to execute a full penetration testing lifecycle—from Reconnaissance to Post-Exploitation—against a vulnerable Linux target. The week concluded with a Capstone Project focusing on SQL Injection and data exfiltration.

## 🛠️ Tools Used
* **Operating System:** Kali Linux 2024.x
* **Network Scanning:** Nmap 7.95
* **Web Scanning:** Nikto, WhatWeb
* **OSINT:** WHOIS, Sublist3r
* **Exploitation:** Metasploit Framework (MSF)
* **Database Attack:** SQLMap

---

## 🔄 Workflow & Methodology

### Phase 1: Reconnaissance (OSINT & Fingerprinting)
**Objective:** Map the attack surface of external and internal targets.

* **Domain Intelligence:**
    * Target: `nmap.org`
    * Tool: `whois`, `sublist3r`
    * *Finding:* Identified Registrar (Dynadot) and subdomains (`scanme`, `svn`).
* **Internal Fingerprinting:**
    * Target: `192.168.56.105`
    * Tool: `whatweb 192.168.56.105`
    * *Finding:* Detected Apache 2.2.8 (Ubuntu) and PHP 5.2.4 (End-of-Life versions).

### Phase 2: Vulnerability Scanning
**Objective:** Identify active services and prioritize critical vulnerabilities.

* **Network Scan:**
    * Command: `nmap -sV 192.168.56.105`
    * *Critical Findings:*
        * **Port 21:** vsftpd 2.3.4 (Backdoor present)
        * **Port 1524:** Bindshell (Root access)
        * **Port 8180:** Apache Tomcat
* **Web Vulnerability Scan:**
    * Command: `nikto -h http://192.168.56.105`
    * *Findings:* Exposed `/phpMyAdmin` directory, outdated Apache server, HTTP TRACE enabled.

### Phase 3: Exploitation (System Compromise)
**Objective:** Gain unauthorized remote access to the target.

* **Target:** Apache Tomcat Manager (Port 8180)
* **Technique:** Credential Brute-Force & Malicious File Upload
* **Steps:**
    1.  Used Metasploit `auxiliary/scanner/http/tomcat_mgr_login` to discover credentials: `tomcat:tomcat`.
    2.  Used `exploit/multi/http/tomcat_mgr_upload` to deploy a generic WAR payload (`java/shell_reverse_tcp`).
    3.  **Result:** Successfully opened a remote shell (Session 1) as user `tomcat55`.

### Phase 4: Post-Exploitation (Privilege Escalation)
**Objective:** Escalate privileges to Root and collect forensic evidence.

* **Exploit Used:** Linux Kernel `udev` Netlink Exploit
* **Metasploit Module:** `exploit/linux/local/udev_netlink`
* **Process:**
    1.  Backgrounded the initial Tomcat session.
    2.  Ran the local kernel exploit against the session.
    3.  **Result:** Escalated to **Root (UID 0)**.
* **Evidence Collection:**
    * Verified identity with `whoami` and `id`.
    * Generated integrity hash of the shadow file: `sha256sum /etc/shadow`.

### Phase 5: Capstone Project (Web Application Attack)
**Objective:** Demonstrate data exfiltration via SQL Injection on DVWA.

* **Target App:** Damn Vulnerable Web App (DVWA)
* **Vulnerability:** SQL Injection (Union-Based) in `id` parameter.
* **Tool:** SQLMap
* **Command:**
    ```bash
    sqlmap -u "[http://192.168.56.105/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit](http://192.168.56.105/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit)" \
    --cookie="security=low; PHPSESSID=..." --dbs --batch
    ```
* **Results:**
    * Enumerated 7 databases (including `dvwa`, `metasploit`, `mysql`).
    * Dumped the `users` table, revealing administrative password hashes.

---

## 📂 Repository Structure
* **`/Week 2/`**
    * `README.md`: This workflow documentation.
    * `VAPT_Report_Week2.pdf`: The complete, formal PDF report.
    * `/Screenshots/`: Raw evidence images (Nmap, Metasploit, etc.).
    * `/Scans/`: Raw text output files (`nmap_results.txt`, `nikto_results.txt`).

---

## ⚠️ Disclaimer
This project was conducted in a controlled, isolated laboratory environment using a dedicated vulnerable Virtual Machine (Metasploitable 2). All offensive activities were performed with authorization for educational purposes only. Unauthorized access to computer systems is illegal.
