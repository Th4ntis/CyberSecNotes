---
description: Helpful links and resources for SOC Analysts
---

# SOC Tools

Here's a list of helpful tools that can be used for [OSINT](../osint/) and Sandboxing for SOC Analysts. These tools can be used to looking up information on Domains, IPs, URLs, File Hashes, etc.

{% hint style="warning" %}
No one tool is the end all-be-all, please make sure to use multiple resources to gather and collect information.
{% endhint %}

* [URLScan](https://urlscan.io/)
  * "_A sandbox for the web"_ Scans submitted URL website for malicious intent details in [their about page](https://urlscan.io/about/).
* [AbuseIPDB](https://www.abuseipdb.com/)
  * IP/Domain Information - Able to see if other users have reported the ip/domain for malicious activity recently and what for.
* [VirusTotal](https://www.virustotal.com/gui/home/upload)
  * Analyze suspicious files, domains, IPs and URLs to detect malware and other breaches. Able to see if other users have reported the ip/domain for malicious activity recently and what for.
* [CyberChef](https://gchq.github.io/CyberChef/)
  * [Decode Base64](https://icyberchef.com/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true\)\&input=U0dGamF5QjBhR1VnVUd4aGJtVjBJUT09), [Convert data from a hexdump, then decompress](https://icyberchef.com/#recipe=From\_Hexdump\(\)Gunzip\(\)\&input=MDAwMDAwMDAgIDFmIDhiIDA4IDAwIDEyIGJjIGYzIDU3IDAwIGZmIDBkIGM3IGMxIDA5IDAwIDIwICB8Li4uLi6881cu/y7HwS4uIHwKMDAwMDAwMTAgIDA4IDA1IGQwIDU1IGZlIDA0IDJkIGQzIDA0IDFmIGNhIDhjIDQ0IDIxIDViIGZmICB8Li7QVf4uLdMuLsouRCFb/3wKMDAwMDAwMjAgIDYwIGM3IGQ3IDAzIDE2IGJlIDQwIDFmIDc4IDRhIDNmIDA5IDg5IDBiIDlhIDdkICB8YMfXLi6%2BQC54Sj8uLi4ufXwKMDAwMDAwMzAgIDRlIGM4IDRlIDZkIDA1IDFlIDAxIDhiIDRjIDI0IDAwIDAwIDAwICAgICAgICAgICB8TshObS4uLi5MJC4uLnw), [Decrypt and disassemble shellcode](https://icyberchef.com/#recipe=RC4\(%7B'option':'UTF8','string':'secret'%7D,'Hex','Hex'\)Disassemble\_x86\('64','Full%20x86%20architecture',16,0,true,true\)\&input=MjFkZGQyNTQwMTYwZWU2NWZlMDc3NzEwM2YyYTM5ZmJlNWJjYjZhYTBhYWJkNDE0ZjkwYzZjYWY1MzEyNzU0YWY3NzRiNzZiM2JiY2QxOTNjYjNkZGZkYmM1YTI2NTMzYTY4NmI1OWI4ZmVkNGQzODBkNDc0NDIwMWFlYzIwNDA1MDcxMzhlMmZlMmIzOTUwNDQ2ZGIzMWQyYmM2MjliZTRkM2YyZWIwMDQzYzI5M2Q3YTVkMjk2MmMwMGZlNmRhMzAwNzJkOGM1YTZiNGZlN2Q4NTlhMDQwZWVhZjI5OTczMzYzMDJmNWEwZWMxOQ), and more.
* [Shodan](https://www.shodan.io/)
  * IP/Domain Information but can be _**MUCH**_ more powerful. More information found [here](../osint/shodan.md).
* [Browserling](https://www.browserling.com/)
  * Sandbox URLs on various browsers and interact with them in a live secure environment.
* [Cisco Talos Intelligence](https://talosintelligence.com/)
  * "Search by IP, domain, or network owner for real-time threat data."
* [URLHaus](https://urlhaus.abuse.ch/)
  * Search IP/Domain, URL, MD5, SHA256, and more to see if they have been flagged as malicious/suspicious.
* [URLVoid](https://www.urlvoid.com/)
  * Website reputation checker. Shows information of location, IP, WHOIS, DNS Records, and if various services have blacklisted the URL or not.
* [IPVoid](https://www.ipvoid.com/)
  * Various tools for IP information. WHOIS, DNS, DNSDIG, MX Record, Blaklisted by any services, etc.
* [IBM X-Force](https://exchange.xforce.ibmcloud.com/)
  * Scan for a multitude of things such as IP/Domain, File Hash, Vulnerabilities, upload files for analysis, etc.
* [URL2PNG](https://www.url2png.com/)
  * Get a screenshot of a website rather than browsing to it.
* [Any.run](https://any.run/)
  * Cloud based sandbox for URLs, Files, etc.
* [Hybrid-Analysis](https://hybrid-analysis.com/)
  * Malware Analysis Service
* [Joes Sandbox](https://www.joesandbox.com/)
  * "Detects and analyzes potential malicious files and URLs" on various OS
* [Bash.ws](https://bash.ws/)
  * Whois, host, dig, nslookup, ping, traceroute, and geoiplookup tool on IPs and Domains
* [Triage](https://tria.ge/)
  * Malware Analysis Sandbox
* [Malware Bazaar](https://bazaar.abuse.ch/)
  * Search file hashes to see if they have been flagged as malicious.
* [RDAP](https://client.rdap.org/)
  * WHOIS sucessor - Provides access to information about Internet resources
* [DNSDumpster](https://dnsdumpster.com/)
  * "Domain research tool that can discover hosts related to a domain"
* [Whois](https://www.whois.com/whois)
  * Domain/IP Information lookup
* [HaveIBeenPwned](https://haveibeenpwned.com/?ref=websitehunt)
  * Check if your email or phone is in a data breach
