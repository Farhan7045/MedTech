# MedTech - Active Directory Lab Exploitation Walkthrough

This repository provides a full-scope penetration test report of the **MedTech** Active Directory lab. The objective was to simulate adversarial behavior across a Windows-based enterprise environment and perform a complete compromise of the domain through technical enumeration, exploitation, lateral movement, and post-exploitation.

## 🧠 Lab Objective

To emulate a red team attack chain in a controlled environment that includes:
- Discovery of misconfigurations and vulnerable services
- Gaining initial access through various entry points
- Privilege escalation across Windows environments
- Lateral movement and domain compromise
- Complete domain administrator access

## 🔧 Tools & Utilities

- `nmap`, `crackmapexec`, `evil-winrm`, `impacket`, `secretsdump.py`
- `bloodhound`, `SharpHound`, `winPEASx64.exe`, `mimikatz`
- `John the Ripper`, `hashcat`, `lsass` dump analysis
- `Metasploit`, `msfvenom`, reverse shell payloads
- PowerShell post-exploitation and enumeration scripts

## 🧭 Attack Path Overview

### 1. 📡 Reconnaissance & Enumeration
- Scanned the subnet for live hosts and open ports using `nmap`
- Identified services like WinRM, SMB, LDAP, and RDP
- Enumerated usernames and shares via SMB

### 2. 🕳 Initial Access
- Credential spraying using `crackmapexec`
- Gained access via valid SMB and WinRM logins
- Reverse shell obtained through fileless PowerShell payload

### 3. 📈 Privilege Escalation
- Used `winPEAS` to identify:
  - SeImpersonate privileges
  - Stored credentials in config files and registry
- Token impersonation via Juicy Potato / Rogue Potato
- Extracted credentials from memory using `mimikatz` and `lsass`

### 4. 🔁 Lateral Movement
- Pivoted using `evil-winrm` and valid credentials
- Abused Active Directory delegation and service misconfigurations
- Explored AD relationships using BloodHound and Neo4j

### 5. 🏴 Domain Compromise
- Obtained `krbtgt` and `Administrator` NTLM hashes via DCSync
- Deployed Golden Ticket for persistence
- Extracted and exfiltrated sensitive information

## 🧾 Captured Flags

Each compromised host yielded one or more flags proving access or privilege level:
Flag1: 3dc178ba131a2f5198960a3bfb97f9a7 # Initial foothold
Flag2: 71c865fc303b928f527b9ab3a76d1a5e # Privilege escalation
Flag3: 1af6d26bda728edb368209f6df82f716 # Domain admin compromise

## 🧬 Key Takeaways

- Credential reuse and weak passwords were a major attack vector
- SeImpersonate privilege was consistently exploitable
- Misconfigured SMB shares and AD delegation introduced significant risk
- PowerShell remains a powerful post-exploitation tool

**Author:** Farhanahmad Quraishi
