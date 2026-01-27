# Week 4 Cybersecurity Lab Reports & Capstone Project

## 📄 Overview
[cite_start]This document compiles a series of advanced cybersecurity lab reports and a final Capstone project conducted by CYART[cite: 1]. [cite_start]The reports cover various domains including web application exploitation, API security, privilege escalation, network protocol attacks, and mobile application testing[cite: 5, 329, 610, 703, 769, 824].

---

## 🛠️ Table of Contents

1.  [Advanced Exploitation Lab (Mr. Robot VM)](#1-advanced-exploitation-lab-mr-robot-vm)
2.  [API Security Testing Lab (DVWA)](#2-api-security-testing-lab-dvwa)
3.  [Privilege Escalation and Persistence Lab](#3-privilege-escalation-and-persistence-lab)
4.  [Network Protocol Attacks Lab](#4-network-protocol-attacks-lab)
5.  [Mobile Application Testing Lab](#5-mobile-application-testing-lab)
6.  [Capstone Project: Full VAPT Engagement](#6-capstone-project-full-vapt-engagement)

---

## 1. Advanced Exploitation Lab (Mr. Robot VM)
[cite_start]**Target:** 192.168.87.53 [cite: 5]
[cite_start]**Date:** January 23, 2026 [cite: 5]

### Summary
[cite_start]A comprehensive penetration test identifying critical vulnerabilities in the WordPress CMS[cite: 7, 8]. [cite_start]The attack chain involved credential enumeration and shell upload to achieve Remote Code Execution (RCE)[cite: 9].

### Key Findings
* [cite_start]**Credential Access:** Brute-forced WordPress administrative credentials (`elliot` / `ER28-0652`)[cite: 14].
* [cite_start]**RCE:** Uploaded a malicious PHP payload via the WordPress plugin manager using Metasploit (`exploit/unix/webapp/wp_admin_shell_upload`)[cite: 151].
* [cite_start]**Privilege Escalation:** Exploited a SUID misconfiguration in the `nmap` binary to escalate privileges from `daemon` to `root`[cite: 251, 252].

---

## 2. API Security Testing Lab (DVWA)
[cite_start]**Target:** DVWA (Simulated API Endpoints) & Postman Local [cite: 330]
[cite_start]**Date:** January 26, 2026 [cite: 330]

### Summary
[cite_start]Security testing evaluated resilience against OWASP API Top 10 vulnerabilities[cite: 332]. [cite_start]Critical flaws were found in object-level authorization and schema exposure[cite: 333, 334].

### Key Findings
* [cite_start]**Broken Object Level Authorization (BOLA):** Exploited an ID parameter to access unauthorized user profiles (e.g., accessing User ID 2 "Gordon Brown" as User ID 1)[cite: 445, 447].
* [cite_start]**GraphQL Introspection:** Identified potential schema exposure through introspection queries[cite: 334, 519].
* [cite_start]**Token Manipulation:** Session management was found to be secure; token tampering attempts were redirected to the login page[cite: 335, 549].

---

## 3. Privilege Escalation and Persistence Lab
[cite_start]**Target:** 192.168.87.53 [cite: 611]
[cite_start]**Date:** January 27, 2026 [cite: 611]

### Summary
[cite_start]Focusing on post-exploitation, this lab utilized LinPEAS for enumeration and established persistence after gaining root access[cite: 616, 619].

### Key Findings
* [cite_start]**Enumeration:** LinPEAS identified `/usr/local/bin/nmap` with SUID permissions[cite: 625].
* [cite_start]**Exploitation:** Used Nmap's "Interactive Mode" to spawn a root shell (`!sh`)[cite: 680].
* [cite_start]**Persistence:** Created a hidden script (`.backdoor.sh`) and configured a system-wide cron job to execute a reverse shell every minute[cite: 699, 700].

---

## 4. Network Protocol Attacks Lab
[cite_start]**Target:** 192.168.87.149 (Metasploitable 2) [cite: 705]
[cite_start]**Date:** January 27, 2026 [cite: 705]

### Summary
[cite_start]Assessment of local network protocols to identify flaws in name resolution services[cite: 707].

### Key Findings
* [cite_start]**LLMNR/NBT-NS Poisoning:** Successfully used **Responder** to intercept broadcast requests[cite: 708].
* [cite_start]**Traffic Interception:** Spoofed the identity of a trusted network resource, redirecting the victim to the attacker machine[cite: 708, 723].

---

## 5. Mobile Application Testing Lab
[cite_start]**Target:** `test.apk` (Beta Build) [cite: 770]
[cite_start]**Date:** January 27, 2026 [cite: 770]

### Summary
[cite_start]A hybrid assessment using Static Analysis (MobSF) and Dynamic Instrumentation (Frida)[cite: 773].

### Key Findings
* [cite_start]**Static Analysis:** Identified high-severity vulnerabilities including "Insecure Data Storage" (plain text credentials in `SharedPreferences.xml`) and hardcoded API keys[cite: 779, 784].
* [cite_start]**Authentication Bypass:** Used a Frida script to hook the `checkPin()` function, forcing it to return `true` and bypass the login screen[cite: 795, 811].
* [cite_start]**IPC Analysis:** Drozer revealed exported activities (e.g., `PostLoginAdminActivity`) that could be launched directly to skip authentication[cite: 823].

---

## 6. Capstone Project: Full VAPT Engagement
[cite_start]**Target:** HackTheBox "Lame" (10.10.10.3) [cite: 825]
[cite_start]**Date:** January 27, 2026 [cite: 825]

### Summary
[cite_start]A simulated full penetration test against a legacy server[cite: 830]. [cite_start]The primary breach exploited a critical RCE vulnerability in the file-sharing service[cite: 832].

### Attack Timeline
1.  [cite_start]**Reconnaissance:** Nmap scan identified `vsftpd 2.3.4` and `Samba 3.0.20` on ports 21 and 445[cite: 837].
2.  [cite_start]**Vulnerability Analysis:** Identified `Samba 3.0.20` as vulnerable to the "Username Map Script" exploit (CVE-2007-2447)[cite: 879, 880].
3.  [cite_start]**Exploitation:** Executed `exploit/multi/samba/usermap_script` via Metasploit to gain a reverse shell[cite: 899, 908].
4.  [cite_start]**Post-Exploitation:** Confirmed `root` access (`uid=0`) and exfiltrated user and root flags[cite: 936, 938, 939].

### Remediation
* [cite_start]Upgrade Samba to a supported version (4.x+)[cite: 1002].
* [cite_start]Disable unused services like `distccd`[cite: 1004].
* [cite_start]Restrict SMB traffic (Port 445) to trusted internal subnets[cite: 1006].

---

## 📞 Contact Information
* [cite_start]**Email:** inquiry@cyart.io [cite: 2]
* [cite_start]**Website:** www.cyart.io [cite: 3]