# 🛠 Tools

This section will cover various attack tools, vectors, methods, and how we can use them, as well as what to look for to defend against them.

Many tools can be used both offensively and defensively, so seeing one being used should not immediately indicate malicious intent. For example, [Nessus](https://www.tenable.com/products/nessus), is a vulnerability scanner and it can be used offensively to see what services are running, what version they are running on, and if they have any immediate known vulnerabilities and how they can be exploited. In the same, this can be used defensively to know what is vulnerable in your network and can tell you how to patch the vulnerability so it may not be exploited in that manor.

{% hint style="warning" %}
No one tool is a end all be all. There is no "One Tool to Rule Them All". Use multiple tools for the job. They can all do things differently and give information in various ways.
{% endhint %}

## Terminology

APT is an acronym for Advanced Persistent Threat. This can be considered a team/group (_**threat group**_), or even country (_**nation-state group**_), that engages in long-term attacks against organizations and/or countries. FireEye's current list of APT groups can be found [**here**](https://www.fireeye.com/current-threats/apt-groups.html).  \


TTP is an acronym for Tactics, Techniques, and Procedures:

* The Tactic is the adversary's goal or objective.
* The Technique is how the adversary achieves the goal or objective.
* The Procedure is how the technique is executed.

## Master list of Tools

[A list of OSINT Tools can be found here](../osint/osint-tools.md)

### Exploitation Framework

* [Metasploit](https://www.metasploit.com/) - C2/Exploitation Framework
* [Sliver](https://github.com/BishopFox/sliver) - C2/Exploitation Framework
* [Mythic](https://docs.mythic-c2.net/) - C2/Exploitation Framework
* [Cobalt Strike](https://www.cobaltstrike.com/)
* [Havoc](https://github.com/HavocFramework/Havoc) - malleable post-exploitation command and control framework

### Post Exploitation

* [GraphRunner](https://github.com/dafthack/GraphRunner/) - Post-exploitation toolset for interacting with the Microsoft Graph API
  * [Intro to GraphRunner by BHIS](https://www.blackhillsinfosec.com/introducing-graphrunner/)
* [Crackmapexec](https://github.com/byt3bl33d3r/CrackMapExec) - post-exploitation tool
* [NetExec](https://github.com/Pennyw0rth/NetExec) - Another CrackMapExec

### WiFi

* [Aircrack](https://github.com/aircrack-ng/aircrack-ng) - WiFi penetration testing
* [Kismet](https://github.com/kismetwireless/kismet) - wireless network and device detector, sniffer, wardriving tool, and WIDS (wireless intrusion detection) framework
* [Bettercap](https://github.com/bettercap/bettercap) -  [WiFi](https://www.bettercap.org/modules/wifi/), [Bluetooth Low Energy](https://www.bettercap.org/modules/ble/), wireless [HID hijacking](https://www.bettercap.org/modules/hid/) and [IPv4 and IPv6](https://www.bettercap.org/modules/ethernet) networks reconnaissance and MITM attacks.
* [HCXDumptool](https://github.com/ZerBea/hcxdumptool) -  capture packets from wlan devices and to discover potential weak points within WiFi networks
* [WiFite](https://github.com/kimocoder/wifite2) - WiFi penetration testing

### Enumeration

* [GoBuster](https://github.com/OJ/gobuster) - Directory/File, DNS and VHost busting tool written in Go
* Dirb/Dirbuster - Busting Tool for Web Directories
* [Enum4Linux](https://www.kali.org/tools/enum4linux/) - Enumerating information from Windows and Samba systems
* [OneDrive UserEnum](https://github.com/nyxgeek/onedrive\_user\_enum) - Enumerates valid OneDrive accounts
* [Bloodhound](https://github.com/BloodHoundAD/BloodHound) - Active Directory Attacks
  * [Cypheroth](https://github.com/seajaysec/cypheroth) - Runs cypher queries against Bloodhound's Neo4j backend and saves output to spreadsheets.
* [Ldeep](https://github.com/franc-pentest/ldeep) - ldap enumeration utility
* [SUCC](https://github.com/puzzlepeaches/succ) - Queries Microsoft for a list of domains associated with an Office 365 tenant
* [Certipy](https://github.com/ly4k/Certipy) - Tool for Active Directory Certificate Services enumeration and abuse
* [Legba](https://github.com/evilsocket/legba) - A multiprotocol credentials bruteforcer / password sprayer and enumerator.
* [FFUF](https://github.com/ffuf/ffuf) - Fast web fuzzer written in Go
* [Dome](https://github.com/v4d1/Dome) - Subdomain Enumeration

### Hash Cracking

* [Hashcat](https://github.com/hashcat/hashcat) - Open-source hash cracking tool
* [JohnTheRipper](https://github.com/openwall/john) - Open-source hash cracking tool

### Vulnerability Scanners

* [Nessus](https://www.tenable.com/products/nessus) - Vulnerability Scanner
* [OpenVAS](https://openvas.org/) - Vulnerability Scanner

### Web App

* [BurpSuite](https://portswigger.net/burp) - WebApp Pentesting Framework
* [OWASP Zap](https://www.zaproxy.org/) - WebApp Pentesting Framework

### Brute Force

* [Hydra](https://github.com/vanhauser-thc/thc-hydra) - Parallelized login cracker
* [BruteMap](https://github.com/brutemap-dev/brutemap) - BruteForce site login pages
* [Legba](https://github.com/evilsocket/legba) - A multiprotocol credentials bruteforcer / password sprayer and enumerator.

### Credential Dumping

* [Mimikatz](https://github.com/gentilkiwi/mimikatz) - Post Exploitation Credential Dump
* [Pcredz](https://github.com/lgandx/PCredz) - Extracts hashes from a pcap or live interface
* [DonPapi](https://github.com/login-securite/DonPAPI) - Dumps DPAPI Creds
* [ldapdomaindump](https://github.com/dirkjanm/ldapdomaindump) - Active Directory information dumper via LDAP
* [Responder](https://github.com/lgandx/Responder) - LLMNR, NBT-NS and MDNS poisoner

### MitM

* [SETH](https://github.com/SySS-Research/Seth) - RDP MiTM Tool
* [MiTM6](https://github.com/dirkjanm/mitm6) - Replys to DHCPv6
* [NetNTLMtoSilverTicket](https://github.com/NotMedic/NetNTLMtoSilverTicket) - SpoolSample -> NetNTLMv1 -> NTLM -> Silver Ticket

### Payload Generation

* [Freeze.rs](https://github.com/Tylous/Freeze.rs) - Payload toolkit for bypassing EDRs using suspended processes, direct syscalls written in RUST
* [Scarecrow](https://github.com/Tylous/ScareCrow) - Payload creation framework designed around EDR bypass
* [URU](https://github.com/guervild/uru) - Payload generation
* [MSFVenom](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom/29d7dfecc8a10b4390d1d796125da4a2cd0cb8e8) - Combination of payload generation and encoding
* [Mangle](https://github.com/Tylous/Mangle) - manipulates aspects of compiled executables (.exe or DLL) to avoid detection from EDRs

### Process Injection/Shellcode Loaders

* [Bankai](https://github.com/bigb0sss/Bankai) - Go Shellcode loader using Windows API
* [ShhhLoader](https://github.com/icyguider/Shhhloader) - Syscall Shellcode Loader
* [Unicorn](https://github.com/trustedsec/unicorn) - PowerShell downgrade attack and inject shellcode straight into memory
* [TikiTorch](https://github.com/rasta-mouse/TikiTorch) - Process Injection
* [Archeron](https://github.com/f1zm0/acheron) - Indirect syscalls for AV/EDR evasion in Go assembly
* [Win11-OneDrive-DLL-Injection](https://github.com/ras-it/Win11-OneDrive-DLL-injection-vulnerability/)
* [LdrLibraryEx](https://github.com/Cracked5pider/LdrLibraryEx) - A small x64 library to load dll's into memory.

### Wordlists

* [VX-Underground](https://github.com/0xsyr0/vx-underground-wordlist)
* [Hashmob](https://hashmob.net/resources/hashmob)
* [Seclists](https://github.com/danielmiessler/SecLists)

### Other

* [Impacket](https://github.com/SecureAuthCorp/impacket) - A collection of Python classes for working with network protocols
* [Social-Engineer Toolkit(SET)](https://github.com/trustedsec/social-engineer-toolkit) - Open-source penetration testing framework designed for social engineering
* [WolfPack](https://github.com/RoseSecurity-Research/WolfPack) -&#x20;
* [HellsGate](https://github.com/am0nsec/HellsGate) - Original C Implementation of the Hell's Gate VX Technique
* [QuickCert](https://github.com/c3l3si4n/quickcert) - Querying certificate transparency logs
* [TLOSINT](https://github.com/tracelabs/tlosint-vm) - Trace Labs OSINT VM
* [DeHashed API Tool](https://github.com/hmaverickadams/DeHashed-API-Tool) - CLI tool to query the DeHashed API
* [autoNTDS](https://github.com/hmaverickadams/autoNTDS) - automation script designed to simplify the process of dumping and cracking NTDS hashes using secretsdump.py and hashcat
* [PSPY](https://github.com/DominicBreuker/pspy) - Monitor linux processes without root permissions
* [ROADtools](https://github.com/dirkjanm/ROADtools) - A collection of Azure AD tools for offensive and defensive security purposes
* [Dumpert](https://github.com/outflanknl/Dumpert) - LSASS memory dumper using direct system calls and API unhooking.
