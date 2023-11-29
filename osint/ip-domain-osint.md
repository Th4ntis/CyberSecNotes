# IP/Domain OSINT

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
* [Cisco Talos Intelligence](https://talosintelligence.com/) - "Search by IP, domain, or network owner for real-time threat data."
* [IBM X-Force](https://exchange.xforce.ibmcloud.com/) - Scan for a multitude of things such as IP/Domain, File Hash, Vulnerabilities, upload files for analysis, etc. A Threat intelligence sharing platform enabling research on security threats, aggregation of intelligence, and collaboration with peers
* [IP.Teoh.io](https://ip.teoh.io/vpn-detection) - VPN & Proxy IP Detection Tool. Check if an IP is currently blacklisted or is using a VPN/proxy
* [IPVoid](https://www.ipvoid.com/) - Various tools for IP information. WHOIS, DNS, DNSDIG, MX Record, Blaklisted by any services, etc.
* [ViewDNS](https://viewdns.info/) - Huge toolbox with various utilities for enumerating information about a domain.
* [DNSDumpster](https://dnsdumpster.com/) - Free domain research tool that can discover hosts related to a domain.&#x20;
* [MXToolbox ](https://mxtoolbox.com/)-  Checks MX information for the given domain
* [DNSLytics](https://dnslytics.com/) - Find out everything about a domain name, IP address or provider. Discover relations between them and see historical data. Use it for your digital investigation, fraud prevention or brand protection.
* [HostSpider](https://github.com/h3x0crypt/HostSpider) - Command line tool that gathers tons of information about a domain including DNS records, subdomains, WHOIS, Cloudflare IP, and more!
* [OmnisintLabs](https://omnisint.io/) - Project Crobat: Rapid7's DNS Database easily searchable via a lightening fast API, with domains available in milliseconds.
* [Sublist3r](https://github.com/aboul3la/Sublist3r) - Sublist3r is a python tool designed to enumerate subdomains of websites using OSINT. It helps penetration testers and bug hunters collect and gather subdomains for the domain they are targeting. Sublist3r enumerates subdomains using many search engines.
  * [https://tryhackme.com/room/rpsublist3r](https://tryhackme.com/room/rpsublist3r)
