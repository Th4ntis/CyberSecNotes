---
description: Helpful links and resources for Cyber Security Analysts and Researchers
---

# OSINT Tools

Here's a list of helpful tools that can be used for [OSINT](./) and Sand-boxing for Cyber Security Analysts and Researchers. These tools can be used to looking up information on Domains, IPs, URLs, File Hashes, etc.

{% hint style="warning" %}
No one tool is the end all-be-all, please make sure to use multiple resources to gather and collect information.
{% endhint %}

## Go To's

* [URLScan](https://urlscan.io/) - "_A sandbox for the web"_ Scans submitted URL website for malicious intent details in [their about page](https://urlscan.io/about/).
* [CyberChef](https://gchq.github.io/CyberChef/) - [Decode Base64](https://icyberchef.com/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true\)\&input=U0dGamF5QjBhR1VnVUd4aGJtVjBJUT09), [Convert data from a hexdump, then decompress](https://icyberchef.com/#recipe=From\_Hexdump\(\)Gunzip\(\)\&input=MDAwMDAwMDAgIDFmIDhiIDA4IDAwIDEyIGJjIGYzIDU3IDAwIGZmIDBkIGM3IGMxIDA5IDAwIDIwICB8Li4uLi6881cu/y7HwS4uIHwKMDAwMDAwMTAgIDA4IDA1IGQwIDU1IGZlIDA0IDJkIGQzIDA0IDFmIGNhIDhjIDQ0IDIxIDViIGZmICB8Li7QVf4uLdMuLsouRCFb/3wKMDAwMDAwMjAgIDYwIGM3IGQ3IDAzIDE2IGJlIDQwIDFmIDc4IDRhIDNmIDA5IDg5IDBiIDlhIDdkICB8YMfXLi6%2BQC54Sj8uLi4ufXwKMDAwMDAwMzAgIDRlIGM4IDRlIDZkIDA1IDFlIDAxIDhiIDRjIDI0IDAwIDAwIDAwICAgICAgICAgICB8TshObS4uLi5MJC4uLnw), [Decrypt and disassemble shellcode](https://icyberchef.com/#recipe=RC4\(%7B'option':'UTF8','string':'secret'%7D,'Hex','Hex'\)Disassemble\_x86\('64','Full%20x86%20architecture',16,0,true,true\)\&input=MjFkZGQyNTQwMTYwZWU2NWZlMDc3NzEwM2YyYTM5ZmJlNWJjYjZhYTBhYWJkNDE0ZjkwYzZjYWY1MzEyNzU0YWY3NzRiNzZiM2JiY2QxOTNjYjNkZGZkYmM1YTI2NTMzYTY4NmI1OWI4ZmVkNGQzODBkNDc0NDIwMWFlYzIwNDA1MDcxMzhlMmZlMmIzOTUwNDQ2ZGIzMWQyYmM2MjliZTRkM2YyZWIwMDQzYzI5M2Q3YTVkMjk2MmMwMGZlNmRhMzAwNzJkOGM1YTZiNGZlN2Q4NTlhMDQwZWVhZjI5OTczMzYzMDJmNWEwZWMxOQ), and more.
* [Shodan](https://www.shodan.io/) - IP/Domain Information but can be _**MUCH**_ more powerful. More information found [here](shodan.md).
* [Cisco Talos Intelligence](https://talosintelligence.com/) - "Search by IP, domain, or network owner for real-time threat data."
* [TorWhoIs](https://torwhois.com/) - Look up an .onion address and see basic information such as date last seen, open ports, running software and banners
* [URLHaus](https://urlhaus.abuse.ch/) - Search IP/Domain, URL, MD5, SHA256, and more to see if they have been flagged as malicious/suspicious.
* [URLVoid](https://www.urlvoid.com/) - Website reputation checker. Shows information of location, IP, WHOIS, DNS Records, and if various services have blacklisted the URL or not.
* [IPVoid](https://www.ipvoid.com/) - Various tools for IP information. WHOIS, DNS, DNSDIG, MX Record, Blaklisted by any services, etc.
* [GreyNoise](https://viz.greynoise.io/) - Search for devices connected to the internet
* [IBM X-Force](https://exchange.xforce.ibmcloud.com/) - Scan for a multitude of things such as IP/Domain, File Hash, Vulnerabilities, upload files for analysis, etc.
* [Ultimate Windows Security](https://www.ultimatewindowssecurity.com/) - View Windows Event codes, CVE's, and multiple other tools relating to WIndows Security.
* [AlienVaultOTX](https://otx.alienvault.com/) - Extensive threat intelligence feed
* [Censys](https://search.censys.io/) - Assessing attack surface for internet connected devices
* [URL2PNG](https://www.url2png.com/) - Get a screenshot of a website rather than browsing to it.
* [IP.Teoh.io](https://ip.teoh.io/vpn-detection) - VPN & Proxy IP Detection Tool. Check if an IP is currently blacklisted or is using a VPN/proxy
* [DNSChecker](https://dnschecker.org/all-tools.php) - A wide variety of DNS, IP, and other tools.
* [Bash.ws](https://bash.ws/) - Whois, host, dig, nslookup, ping, traceroute, and geoiplookup tool on IPs and Domains
* [NSLookup.io](https://www.nslookup.io/ns-lookup/) - Find all name servers for a domain name with this online DNS NS checker
* [Malware Bazaar](https://bazaar.abuse.ch/) - Search file hashes to see if they have been flagged as malicious.
* [DNSDumpster](https://dnsdumpster.com/) - "Domain research tool that can discover hosts related to a domain"
* [RDAP](https://client.rdap.org/) - WHOIS sucessor - Provides access to information about Internet resources
* [Whois](https://www.whois.com/whois) - Domain/IP Information lookup
* [HaveIBeenPwned](https://haveibeenpwned.com/?ref=websitehunt) - Check if your email or phone is in a data breach
* [Dehashed](https://dehashed.com/) - View leaked credentials and compromised assets
* [DorkSearch](https://dorksearch.com/) - Faster Google dorking.
* [ExploitDB](https://www.exploit-db.com/) - Archive of various exploits
* [WayBackMachine](https://web.archive.org/) - View content from edited, deleted and older websites

## IP/Domain OSINT

When researching IP addresses, it is important we know the context of the search we are performing. There are a multitude of sources to research IP addresses and they can vary depending on what information we want to learn about them.&#x20;

For offensive security, threat hunting, and attack surface mapping, we want current registration data, and any associated data points that our searches may return. These can include hosted domains, ASN, associated network artifacts, etc.

For defensive operations, such as those of the security blue team, we are looking for historical data and activity data of the IP address.

Domains, more than almost any other target, have one of the largest assortments of associated data points. The most important that we will look for out of this section is the Registration data, the hosting data, site information, archived data, and analytics

There are tons of highly effective tools for subdomain enumeration and brute forcing, but they can be quite noisy. During the Passive Recon phase of a penetration test, we can start with any subdomains recorded by other sources to plan out our attack/test.

* [RDAP](https://client.rdap.org/) - **Registration Data Access Protocol** is the successor to WHOIS. Like WHOIS, RDAP provides access to information about Internet resources (domain names, autonomous systems, and IP addresses). Unlike WHOIS, RDAP provides:
  * A machine-readable representation of registration data;
  * Differentiated access;
  * Structured request and response semantics;
  * Internationalisation;
  * Extensibility.
* [Whois](https://www.whois.com/whois) - A Whois domain lookup allows you to trace the ownership and tenure of a domain name.
* [Shodan.io](https://www.shodan.io/) - Shodan is a search engine that lets users search for various types of servers connected to the internet using a variety of filters.
* [VirusTotal](https://www.virustotal.com/gui/home/upload) - Analyze suspicious files, domains, IPs and URLs to detect malware and other breaches, automatically share them with the security community
* [AbuseIPDB](https://www.abuseipdb.com/) - AbuseIPDB is a project dedicated to helping combat the spread of hackers, spammers, and abusive activity on the internet.
* [IBM X-Force](https://exchange.xforce.ibmcloud.com/) - Scan for a multitude of things such as IP/Domain, File Hash, Vulnerabilities, upload files for analysis, etc. A Threat intelligence sharing platform enabling research on security threats, aggregation of intelligence, and collaboration with peers
* [IPVoid](https://www.ipvoid.com/) - Various tools for IP information. WHOIS, DNS, DNSDIG, MX Record, Blaklisted by any services, etc.
* [ViewDNS](https://viewdns.info/) - Huge toolbox with various utilities for enumerating information about a domain.
* [DNSDumpster](https://dnsdumpster.com/) - Free domain research tool that can discover hosts related to a domain.&#x20;
* [MXToolbox ](https://mxtoolbox.com/)-  Checks MX information for the given domain
* [DNSLytics](https://dnslytics.com/) - Find out everything about a domain name, IP address or provider. Discover relations between them and see historical data. Use it for your digital investigation, fraud prevention or brand protection.
* [HostSpider](https://github.com/h3x0crypt/HostSpider) - Command line tool that gathers tons of information about a domain including DNS records, subdomains, WHOIS, Cloudflare IP, and more!
* [OmnisintLabs](https://omnisint.io/) - Project Crobat: Rapid7's DNS Database easily searchable via a lightening fast API, with domains available in milliseconds.
* [Sublist3r](https://github.com/aboul3la/Sublist3r) - Sublist3r is a python tool designed to enumerate subdomains of websites using OSINT. It helps penetration testers and bug hunters collect and gather subdomains for the domain they are targeting. Sublist3r enumerates subdomains using many search engines.
  * [https://tryhackme.com/room/rpsublist3r](https://tryhackme.com/room/rpsublist3r)

## Sandboxing

* [Browserling](https://www.browserling.com/) - Sandbox URLs on various browsers and interact with them in a live secure environment.
* [Wannabroswer](https://www.wannabrowser.net/) - Simulate any Browser
* [Hybrid-Analysis](https://hybrid-analysis.com/) - Malware Analysis Service
* [Joes Sandbox](https://www.joesandbox.com/) - "Detects and analyzes potential malicious files and URLs" on various OS
* [Triage](https://tria.ge/) - Malware Analysis Sandbox
* [Any.run](https://any.run/) - An "Interactive online malware analysis service for dynamic and static research of most types of threats using any environments. Replaces a set of tools for research". Free to use and sign up for. Can be used for "a convenient in-depth analysis of new (unidentified) malicious objects, as well as for the investigation of cyber incidentals."

## Additional

* [Maltiverse](https://maltiverse.com/collection) - Search for indicators of compromise or something related
* [HoneyDB](https://honeydb.io/) - Provides real time data of honeypot activity.
* [SecurityTrails](https://securitytrails.com/dns-trails) - Extensive and historical DNS data
* [ZoomEye](https://www.zoomeye.org/) - Gather information about targets
* [Pulsedive](https://pulsedive.com/) - Search for threat intelligence
* [GrayHatWarfare](https://grayhatwarfare.com/) - Search public S3 buckets
* [MHA Azure Websites](https://mha.azurewebsites.net/) - Message Head Analyzer
* [PolySwarm](https://polyswarm.network/) - Scans files and URLs for threats
* [LeakIX](https://leakix.net/) - Search publicly indexed information
* [FullHunt](https://fullhunt.io/) - Search and discovery attack surfaces
* [ONYPHE](https://www.onyphe.io/) - Collects cyber-threat intelligence data
* [Grep App](https://grep.app/) - Git repository search
* [Vulners](https://vulners.com/search) - Search vulnerabilities in a large database
* [Netlas](https://app.netlas.io/host/) - Search and monitor internet connected assets
* [CRT sh](https://crt.sh/) - Search for certs that have been logged by CT
* [Wigle](https://wigle.net/) - Database of wireless networks, with statistics
* [PublicWWW](https://publicwww.com/) - Marketing and affiliate marketing research
* [Binary Edge](https://www.binaryedge.io/) - Scans the internet for threat intelligence
* [Hunter.io](https://hunter.io/) - Search for email addresses belonging to a website
* [IntelligenceX](https://intelx.io/) - Search Tor, I2P, data leaks, domains, and emails
* [Packet Storm Security](https://packetstormsecurity.com/) - Browse latest vulnerabilities and exploits
* [SearchCode](https://searchcode.com/) - Search 75 billion lines of code from 40 million projects
