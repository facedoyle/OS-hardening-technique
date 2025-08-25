# Security Incident Report

## Section 1: Identify the network protocol involved in the incident
- **DNS (Domain Name System):** Resolves domain names (yummyrecipesforme.com and greatrecipesforme.com) to IP addresses.  
- **HTTP (Hypertext Transfer Protocol):** Used by the browser to request web pages and download the malicious file. *(Observed in logs.)*  
- **HTTPS (TLS):** Not observed in this incident, but should be enforced to protect integrity and confidentiality in transit.  

## Section 2: Document the incident
Security team were made aware of an incident where owner of **yummyrecipesforme.com** stated they’ve been receiving complaints from customers that are being redirected to **greatrecipesforme.com**. They are then being prompted to download a free recipe, and after opening it they complain of their devices slowing down.  
The owner also stated that having been alerted to this, they attempted to log into their admin panel and were unable to.  

The responding team created a sandbox environment and ran network protocol analyzer **tcpdump**, and visited **www.yummyrecipesforme.com**. The website prompts the user to download a free recipe. The file was executed and the browser then redirects to a malicious domain, **www.greatrecipesforme.com**, where additional malware was hosted.  

**Network logs confirmed the following sequence:**
1. Browser issued a **DNS request** for yummyrecipesforme.com.  
2. DNS server returned the legitimate IP address.  
3. Browser issued an **HTTP request** to retrieve the webpage.  
4. Browser initiated download of the malicious executable.  
5. Browser issued a **DNS request** for greatrecipesforme.com.  
6. DNS server returned the IP address.  
7. Browser issued an **HTTP request** to the malicious site.  

**Root cause:** Poor password hygiene (default admin password retained) and lack of brute-force safeguards. The attacker also locked out legitimate administrators by resetting the admin password.  

## Section 3: Recommended remediations
- **Enforce HTTPS-only (TLS) with HSTS.** Redirect HTTP→HTTPS; disable plaintext auth; prefer TLS 1.2+.  
- **Eliminate default/weak credentials.** Unique, strong admin passwords; store in a password manager.  
- **Require MFA for all admin access.**  
- **Rate-limit and lockouts.** Throttle login attempts; temporary account lock and IP back-off; optional CAPTCHA.  
- **Harden admin access.** Restrict by VPN/IP allowlist; disable public exposure of admin endpoints where possible.  
- **Patch and maintain.** Keep OS/CMS/plugins updated; remove unused components; monitor integrity (CSP/SRI where applicable).  

