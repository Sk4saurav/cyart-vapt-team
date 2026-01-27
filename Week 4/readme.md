# Cybersecurity Lab Reports & Capstone Project

## 📄 Project Overview
This repository contains the complete documentation for the Week 4 Advanced Cybersecurity Engagement conducted by **CYART**. The project encompasses a series of penetration tests, vulnerability assessments, and a final Capstone engagement, demonstrating proficiency in web exploitation, API security, privilege escalation, network attacks, and mobile application testing.

* **Organization:** CYART
* **Website:** www.cyart.io
* **Contact:** inquiry@cyart.io

---

## 🛠️ Table of Contents
1.  [Advanced Exploitation Lab (Mr. Robot)](#1-advanced-exploitation-lab-mr-robot)
2.  [API Security Testing (DVWA)](#2-api-security-testing-dvwa)
3.  [Privilege Escalation & Persistence](#3-privilege-escalation--persistence)
4.  [Network Protocol Attacks](#4-network-protocol-attacks)
5.  [Mobile Application Testing](#5-mobile-application-testing)
6.  [Capstone Project: Full VAPT Engagement](#6-capstone-project-full-vapt-engagement)

---

## 1. Advanced Exploitation Lab (Mr. Robot)
* **Target:** Mr. Robot VM (`192.168.87.53`)
* **Date:** January 23, 2026
* **Tools:** Hydra, Metasploit Framework

### Engagement Summary
A black-box penetration test targeting a vulnerable WordPress instance. The assessment successfully chained a brute-force attack with an arbitrary file upload vulnerability to achieve Remote Code Execution (RCE).

### Key Findings
* **Credential Access:** Successfully recovered administrative credentials (`elliot` / `ER28-0652`) using a dictionary attack.
* **Remote Code Execution:** Exploited the `wp_admin_shell_upload` vulnerability to upload a malicious PHP payload, establishing a reverse TCP connection.
* **Outcome:** Gained initial shell access as the `daemon` user.

---

## 2. API Security Testing (DVWA)
* **Target:** DVWA (Simulated API Endpoints)
* **Date:** January 26, 2026
* **Tools:** Burp Suite Professional, Postman, Gobuster

### Engagement Summary
Security testing focused on the OWASP API Top 10. The assessment revealed critical flaws in authorization mechanisms while verifying the robustness of session management.

### Key Findings
* **Broken Object Level Authorization (BOLA):** Exploited an IDOR vulnerability to access unauthorized user profiles (e.g., "Gordon Brown") by manipulating the User ID parameter.
* **GraphQL Introspection:** Identified a potential information leak where the API schema could be mapped using introspection queries.
* **Token Security:** Validated that the application correctly rejects tampered session tokens, redirecting unauthorized requests to the login page.

---

## 3. Privilege Escalation & Persistence
* **Target:** Mr. Robot VM (`192.168.87.53`)
* **Date:** January 27, 2026
* **Tools:** LinPEAS, Nmap (SUID), Cron

### Engagement Summary
Following the initial compromise, this phase focused on vertical privilege escalation and maintaining long-term access to the target system.

### Key Findings
* **Root Compromise:** Exploited a misconfigured SUID binary (`/usr/local/bin/nmap`) using "Interactive Mode" to spawn a root shell (`!sh`).
* **Persistence:** Established a mechanism to regain access by creating a hidden script (`.backdoor.sh`) and scheduling a system-wide Cron job to execute a reverse shell every minute.

---

## 4. Network Protocol Attacks
* **Target:** Metasploitable 2 (`192.168.87.149`)
* **Date:** January 27, 2026
* **Tools:** Responder, Telnet, Wget

### Engagement Summary
An assessment of local network protocols to identify and exploit flaws in name resolution services (LLMNR/NBT-NS).

### Key Findings
* **LLMNR Poisoning:** Successfully configured **Responder** to intercept broadcast name resolution requests.
* **Credential Capture:** Spoofed a trusted network resource, poisoning the target's traffic and redirecting it to the attacker machine for potential credential harvesting.

---

## 5. Mobile Application Testing
* **Target:** `test.apk` (Beta Build)
* **Date:** January 27, 2026
* **Tools:** MobSF, Frida, Drozer

### Engagement Summary
A hybrid security assessment of an Android application, combining static analysis of the source code with dynamic runtime manipulation.

### Key Findings
* **Insecure Data Storage:** Static analysis (MobSF) revealed sensitive credentials stored in plain text within `SharedPreferences.xml`.
* **Authentication Bypass:** Used **Frida** to hook the `checkPin()` function at runtime, forcing it to return `true` and successfully bypassing the login screen.
* **Exported Activities:** **Drozer** identified exposed application components (e.g., `PostLoginAdminActivity`) that allowed direct access to privileged areas without authentication.

---

## 6. Capstone Project: Full VAPT Engagement
* **Target:** HackTheBox "Lame" (`10.10.10.3`)
* **Date:** January 27, 2026
* **Tools:** Nmap, Metasploit, Searchsploit

### Engagement Summary
A full-lifecycle penetration test against a legacy Linux server. The engagement followed the PTES standard, moving from reconnaissance to root-level compromise.

### Key Findings
* **Reconnaissance:** Identified `vsftpd 2.3.4` (Port 21) and `Samba 3.0.20` (Port 445) as high-value targets.
* **Exploitation:** Exploited the critical **Samba "Username Map Script" vulnerability (CVE-2007-2447)** using Metasploit to achieve Remote Code Execution.
* **Post-Exploitation:** Confirmed `root` access (`uid=0`) and successfully exfiltrated both the user and root flags as proof of compromise.
