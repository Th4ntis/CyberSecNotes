# Methodology, Attack and Remediation

### Typical methodology

Most tests follow a similar flow (PTES, OWASP, NIST SP 800-115):

1. **Scoping and rules of engagement**
2. **Reconnaissance** (passive and active)
3. **Scanning and enumeration**
4. **Exploitation**
5. **Post-exploitation** (privilege escalation, lateral movement, persistence)
6. **Reporting and remediation verification**

## Common attack paths

### 1. External network and perimeter

* **Typical weaknesses:** exposed management interfaces (RDP, SSH, VPN portals), unpatched edge devices, default credentials, weak TLS, forgotten subdomains and services
* **Remediation:** reduce attack surface, put admin interfaces behind VPN or zero-trust access, patch edge devices quickly, enforce MFA, monitor external asset inventory
* **Tools:** Nmap, Masscan, Shodan, Amass, Subfinder, Nessus, OpenVAS, Nuclei, testssl.sh

### 2. Web applications

* **Typical weaknesses (OWASP Top 10):** SQL injection, XSS, broken access control/IDOR, authentication and session flaws, SSRF (Server-Side Request Forgery), insecure deserialization, security misconfiguration, vulnerable components
* **Remediation:** parameterized queries, output encoding, server-side authorization checks on every request, secure session handling, input validation, dependency scanning, security headers, WAF as defense in depth
* **Tools:** Burp Suite, OWASP ZAP, sqlmap, ffuf/Gobuster, Nikto, Wappalyzer, Nuclei

### 3. APIs

* **Typical weaknesses:** broken object-level authorization, excessive data exposure, missing rate limiting, mass assignment, weak token handling
* **Remediation:** object-level authorization checks, schema validation, response filtering, rate limiting, short-lived scoped tokens
* **Tools:** Postman, Burp Suite (with extensions), ZAP, Kiterunner

### 4. Phishing and social engineering

* **Typical weaknesses:** credential harvesting, malicious attachments, vishing, weak MFA (push fatigue, adversary-in-the-middle)
* **Remediation:** phishing-resistant MFA (FIDO2/passkeys), email filtering and DMARC/SPF/DKIM, user training and easy reporting, conditional access
* **Tools:** GoPhish, Evilginx (for authorized simulations), SET

### 5. Internal network and Active Directory

This is often where the biggest findings come from. For the full stage-by-stage chain, see the AD attack chain below.

* **Typical weaknesses:** LLMNR/NBT-NS/mDNS poisoning, SMB signing disabled, Kerberoasting and AS-REP roasting, weak or reused passwords, excessive privileges, misconfigured AD CS (certificate services), unconstrained delegation, credential exposure in shares or GPP
* **Remediation:** disable LLMNR/NBT-NS, enforce SMB and LDAP signing, long random service-account passwords or gMSAs, tiered admin model, LAPS, AD CS hardening, least privilege, remove stored credentials from shares
* **Tools:** BloodHound, Responder, Impacket, NetExec (CrackMapExec successor), Certipy, Rubeus, Mimikatz, Hashcat, John the Ripper

### 6. Privilege escalation

* **Windows weaknesses:** unquoted service paths, weak service/file permissions, AlwaysInstallElevated, token privileges, unpatched local vulnerabilities
* **Linux weaknesses:** SUID misuse, sudo misconfigurations, writable cron jobs, kernel vulnerabilities, exposed secrets
* **Remediation:** least privilege, patch management, remove unnecessary SUID/sudo rights, harden service configurations, CIS benchmarks
* **Tools:** WinPEAS, LinPEAS, PowerUp, Seatbelt, GTFOBins/LOLBAS (reference), Metasploit

### 7. Cloud (AWS, Azure, GCP)

* **Typical weaknesses:** over-permissive IAM roles, public storage buckets, exposed metadata services (IMDSv1), leaked keys in repos, misconfigured security groups, missing logging
* **Remediation:** least-privilege IAM, block public storage by default, enforce IMDSv2, secrets scanning, CSPM tooling, enable and monitor audit logs
* **Tools:** ScoutSuite, Prowler, Pacu, CloudFox, ROADtools, Trivy, TruffleHog

### 8. Wireless and physical

* **Typical weaknesses:** weak WPA2-PSK passphrases, rogue AP exposure, unprotected network ports, tailgating, unlocked workstations
* **Remediation:** WPA3 or WPA2/3-Enterprise with certificate auth, NAC (802.1X), port security, badge controls, screen lock policies
* **Tools:** Aircrack-ng, Kismet, Wifite, hardware devices (Flipper Zero, Wi-Fi Pineapple)

### 9. Containers and CI/CD

* **Typical weaknesses:** exposed Docker/Kubernetes APIs, privileged containers, secrets in images or pipelines, vulnerable base images, overly trusted build systems
* **Remediation:** image scanning, non-root and read-only containers, network policies, RBAC, secrets management, pipeline hardening and signed artifacts
* **Tools:** Trivy, Grype, kube-hunter, kube-bench, Peirates, Checkov, Semgrep

### Tools by phase (quick reference)

| Phase                  | Common tools                                           |
| ---------------------- | ------------------------------------------------------ |
| Recon / OSINT          | theHarvester, Amass, Recon-ng, Maltego, Shodan, Censys |
| Scanning / enumeration | Nmap, Nessus, OpenVAS, Nuclei, enum4linux-ng           |
| Web/API testing        | Burp Suite, ZAP, sqlmap, ffuf                          |
| Exploitation           | Metasploit, manual PoCs, Impacket                      |
| Password attacks       | Hashcat, John, Hydra, CeWL                             |
| Post-exploitation / C2 | Cobalt Strike, Sliver, Havoc, Mythic, Empire           |
| AD analysis            | BloodHound, PingCastle, Certipy                        |
| Reporting              | Dradis, PlexTrac, Faraday, SysReptor                   |

### Remediation principles that cover most findings

* **Patch and configure well:** vulnerability management with risk-based prioritization (CVSS plus exploitability, such as EPSS and CISA KEV)
* **Identity first:** MFA everywhere, least privilege, strong credential hygiene, privileged access management
* **Segment the network** to limit lateral movement
* **Detect and respond:** EDR, centralized logging, alerting tuned to the techniques testers use (map to MITRE ATT\&CK)
* **Secure development:** threat modeling, code review, SAST/DAST/SCA in CI
* **Retest:** verify fixes and run purple-team exercises so defenders learn from the findings

***

## Full Active Directory Attack Chain with Defenses

A realistic AD engagement usually starts with **zero domain credentials** and ends with **Domain Admin or Enterprise Admin**. Below is a typical chain, stage by stage, with the defense for each step.

### Stage 1: Initial foothold (no credentials)

**Attack**

* Connect to the internal network (onsite, VPN, or compromised laptop)
* Run **Responder** to poison LLMNR/NBT-NS/mDNS broadcast name resolution requests, capturing NTLMv2 hashes when a workstation mistypes a share name
* Alternatively, use **NetExec (formerly CrackMapExec)** or **enum4linux-ng** to enumerate SMB null sessions, open shares, and user lists
* Relay captured hashes with **ntlmrelayx** (Impacket) to a machine with SMB signing disabled, potentially gaining a shell without ever cracking a password

**Tools:** Responder, Impacket (ntlmrelayx, secretsdump), NetExec, enum4linux-ng

**Defenses**

* Disable LLMNR and NBT-NS via Group Policy
* Disable mDNS where not required
* Enforce SMB signing on all workstations and servers (not just domain controllers)
* Enforce LDAP signing and LDAP channel binding
* Segment network access so arbitrary workstations can't reach each other over SMB (host-based firewalls, east-west segmentation)

### Stage 2: Credential access and cracking

**Attack**

* Crack captured NTLMv2 hashes offline with **Hashcat** or **John the Ripper** (see cracking commands)
* Password spray common/seasonal passwords against the domain using **NetExec** or **Kerbrute**, staying under lockout thresholds
* Harvest credentials from unsecured shares, GPO preferences (cpassword in SYSVOL), scripts, or config files

**Tools:** Hashcat, John the Ripper, Kerbrute, NetExec, grep/ripgrep for secrets in shares

**Defenses**

* Enforce long passphrases (14+ characters) or passwordless/MFA-backed auth
* Remove Group Policy Preferences credentials (patch MS14-025 era issue, but still found in legacy GPOs)
* Set account lockout policies (or smart lockout) to blunt spraying
* Alert on authentication spikes (SIEM detection for spray patterns)
* Scan shares and repos for stored secrets regularly

### Stage 3: Kerberos abuse (with any valid domain account)

**Attack**

* **Kerberoasting:** request service tickets (TGS) for accounts with SPNs set, then crack the ticket offline with Hashcat since service account passwords are often weak and never rotated
* **AS-REP Roasting:** target accounts with "Do not require Kerberos preauthentication" set, grab the AS-REP, crack offline
* Tools: **Rubeus**, **Impacket's GetUserSPNs.py / GetNPUsers.py**

**Defenses**

* Use Group Managed Service Accounts (gMSAs) for services - passwords are long, random, and auto-rotated
* If gMSA isn't possible, enforce 25+ character random passwords on service accounts
* Ensure Kerberos pre-authentication is enabled for all accounts unless there's a specific legacy reason
* Monitor for abnormal volumes of TGS requests (Event ID 4769), especially RC4 encryption requests, which are a Kerberoasting red flag

### Stage 4: Enumeration and attack path mapping

**Attack**

* Dump the domain with **BloodHound** (via SharpHound collector) to map users, groups, sessions, ACLs, and trust relationships
* Identify shortest paths to Domain Admin - often through nested group memberships, GenericAll/GenericWrite ACL abuse, or a helpdesk account with unexpected rights over a privileged group
* Identify computers where a Domain Admin has an active logon session, enabling credential theft via lateral movement

**Tools:** BloodHound/SharpHound, PlumHound (reporting), ADRecon

**Defenses**

* Regularly run BloodHound yourself (purple-team it) to find and fix excessive ACLs and nested group paths before attackers do
* Implement a tiered administration model (Tier 0/1/2) so Domain Admins never log on to lower-tier workstations
* Audit and minimize "dangerous" ACEs (GenericAll, WriteDacl, WriteOwner, ForceChangePassword) on sensitive objects
* Use the Protected Users group and dedicated admin workstations (PAWs) for privileged accounts

### Stage 5: Lateral movement

**Attack**

* Use harvested credentials or hashes to move to additional hosts
* **Pass-the-Hash** with NTLM hash (no plaintext needed) via Impacket's psexec.py or wmiexec.py
* **Pass-the-Ticket** using Kerberos tickets extracted with Rubeus or Mimikatz
* **OverPass-the-Hash** to convert an NTLM hash into a Kerberos TGT

**Tools:** Impacket suite, Mimikatz, Rubeus, NetExec

**Defenses**

* Enable Credential Guard on workstations to protect LSASS secrets
* Disable NTLM where feasible; enforce Kerberos-only authentication
* Use unique local admin passwords per machine via **LAPS** (Local Administrator Password Solution) so one compromised local admin hash doesn't work everywhere
* Restrict admin logon rights (deny workstation RDP/local logon for Domain Admins)
* Monitor Event ID 4624/4625 logon types (especially Type 3 and Type 9) for anomalies

### Stage 6: Privilege escalation to Domain Admin

**Attack**

* Abuse **unconstrained delegation**: if a compromised server has unconstrained delegation enabled, coerce a Domain Controller to authenticate to it (using **PetitPotam**, **PrinterBug/SpoolSample**, or **Coercer**) and capture its TGT, then impersonate the DC
* Abuse **AD CS (Certificate Services)** misconfigurations (ESC1–ESC14 as cataloged by Certipy/SpecterOps) to request certificates that allow authenticating as any user, including Domain Admins
* Exploit **constrained delegation** misconfigurations for similar impersonation attacks

**Tools:** PetitPotam, Coercer, Certipy, Rubeus, Impacket

**Defenses**

* Avoid unconstrained delegation entirely; use constrained delegation or resource-based constrained delegation instead
* Patch/mitigate PrinterBug and PetitPotam coercion vectors (disable Print Spooler on DCs, enable EPA on AD CS endpoints)
* Audit and harden AD CS templates - disable or restrict any template allowing low-privileged enrollment combined with "supply subject in request" or client authentication EKU
* Enable Extended Protection for Authentication (EPA) on CA web enrollment endpoints

### Stage 7: Domain dominance and persistence

**Attack**

* Dump the NTDS.dit database (via **secretsdump.py** or volume shadow copy) to get every domain password hash
* Create a **Golden Ticket** (forged TGT using the krbtgt hash) for persistent, nearly undetectable domain-wide access
* Create a **Silver Ticket** for persistent access to a specific service
* Install backdoor accounts, Skeleton Key, or DCSync rights on a seemingly low-privileged account for stealthy re-entry

**Tools:** Mimikatz, Impacket (secretsdump, ticketer.py)

**Defenses**

* Rotate the krbtgt account password **twice** (back-to-back) after any suspected compromise - this invalidates all Golden Tickets
* Restrict and monitor accounts with DCSync rights (Replicating Directory Changes permissions) - very few accounts should have this
* Deploy DC hardening baselines, restrict RDP/logon to DCs, and use dedicated admin forests/PAWs for Tier 0 operations
* Enable advanced auditing (4662, 4670, 5136) to detect DCSync and ACL tampering
* Use deception (honeytoken accounts) to detect lateral movement and ticket forgery attempts early

### Summary defense priorities

1. Disable LLMNR/NBT-NS, enforce SMB/LDAP signing
2. Deploy LAPS for unique local admin passwords
3. Implement a tiered admin model with PAWs for Tier 0
4. Use gMSAs and strong passwords for service accounts
5. Run BloodHound against your own environment regularly and fix excessive ACLs
6. Harden AD CS templates and disable unconstrained delegation
7. Enable Credential Guard, restrict NTLM, monitor Kerberos ticket anomalies
8. Rotate krbtgt after any compromise; restrict DCSync rights

### MITRE ATT\&CK mapping (for reporting/detection)

Most of this chain maps cleanly to:

* **TA0006 Credential Access** (T1557 relay, T1558 Kerberoasting, T1003 OS Credential Dumping)
* **TA0008 Lateral Movement** (T1550 Pass the Hash/Ticket)
* **TA0004 Privilege Escalation** (T1484 Domain Policy Modification, T1649 Steal/Forge Certificates)
* **TA0003 Persistence** (T1558.001 Golden Ticket)
