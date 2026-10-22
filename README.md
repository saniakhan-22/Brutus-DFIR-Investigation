# Brutus-DFIR-Investigation
Digital Forensics &amp; Incident Response (DFIR) investigation analyzing Linux auth logs and brute-force attacks in the HTB Brutus Sherlock.

## Executive Summary
A Linux web server was targeted by a threat actor attempting unauthorized access via SSH. Through analysis of the authentication logs (auth.log) and active session records (wtmp), I identified an SSH brute-force attack originating from an external IP, tracked the successful compromised user account, and determined the threat actor's post exploitation activities.

## Investigation Details
* **Platform:** Hack The Box
* **Category:** Digital Forensics & Incident Response (DFIR) / SOC
* **Environment:** Linux (Ubuntu/Debian Log Artifacts)
* **Malware Analyzed:** /var/log/auth.log. wtmp
* **MITRE ATT&CK Framework:**
  * **T1110.001** - Brute Force: Password Guessing
  * **T1078.003** - Valid Accounts: Local Accounts

 
## Investigation Methodology & Log Analysis
### 1. Identifying the Attacker IP & Initial Brute-Force Activity
* **Objective:** Determine the source IP address conducting the SSH brute-force campaign.
* **Command / Tool Used:**
```bash
grep "Filed Password" auth.log | awk '{print$11}' | sort | uniq -c | sort -nr
