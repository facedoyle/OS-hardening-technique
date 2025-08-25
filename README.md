# Security Incident Report – yummyrecipesforme.com

## Overview
This repository documents a security incident affecting **yummyrecipesforme.com**, where an attacker exploited weak admin credentials and modified the website’s source code to deliver malware.

## Incident Summary
- Customers reported being **redirected to greatrecipesforme.com** and prompted to download a “free recipe.”  
- Downloaded file caused **slow system performance** and **redirected browsers** to a malicious domain.  
- Website owner was **locked out of the admin panel** after the attacker reset the password.  
- Sandbox testing with **tcpdump** confirmed the malicious behavior.

## Network Protocols Observed
- **DNS** – Resolved yummyrecipesforme.com and greatrecipesforme.com to IP addresses.  
- **HTTP** – Used to request web pages and download the malicious executable.  
- **HTTPS** – Not enforced; should be implemented to protect against tampering.  

## Attack Sequence
1. DNS request for yummyrecipesforme.com  
2. DNS reply with legitimate IP  
3. HTTP request for webpage  
4. Download of malicious executable  
5. DNS request for greatrecipesforme.com  
6. DNS reply with IP address  
7. HTTP request to malicious site  

**Root Cause:** Default admin password + no brute force protections → attacker gained access, embedded malicious JavaScript, and reset credentials.  

## Recommended Remediations
- Enforce **HTTPS-only (TLS + HSTS)**  
- Remove all **default/weak credentials**  
- Require **multi-factor authentication (MFA)**  
- Apply **rate-limiting & account lockouts** for failed logins  
- **Restrict admin panel access** (VPN/IP allowlists)  
- Regular **patching & updates** (OS, CMS, plugins)  
- Implement **monitoring & integrity controls** (e.g., CSP, SRI)  

## 📝 Note
End-user awareness messaging (e.g., “We will never ask you to download executables”) can be useful, but **secure web design and server hardening** are the primary defenses.  
