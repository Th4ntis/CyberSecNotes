# Assessment Methodologies

## Passive Information Gathering

Passive Information Gathering is looking at tools/techniques to obtain information of a target through publicly available information through the internet.

### Website Recon & Footprinting

### Looking for:

* IP Addresses
* Directories hidden from search engines
* Names
* Email Addresses
* Phone Numbers
* Physical Address
* Web technologies being used

Using command `host` to find IP address of a website/domain

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

2 IPs usually means they a behind a proxy

* robot.txt file (https://hackersploit.org/robots.txt) - Tells search engine what directories of the website it is allowed and not allowed to crawl and grab information on.
* sitemap.xml (https://hackersploit.org/sitemap\_index.xml) - Used to provide search engine a way to index a website.

### Helpful addons for FF/Chrome

* [Builtwith](https://addons.mozilla.org/en-US/firefox/addon/builtwith/?utm\_source=addons.mozilla.org\&utm\_medium=referral\&utm\_content=search) - Shows details and information such as Widgets, and plugins are installed, subdomains, and more.
* [Wappalyzer](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/) - Another way to identify technologies used on website.
* [Whatweb](https://www.kali.org/tools/whatweb/) - Use command `whatweb` that is built into Kali, to help obtain information as well.
* Download the website - Use [HTTRack](https://www.httrack.com/) - This can be installed on your machine and used to

### Whois Enumeration

WHOIS is a query and response protocol used to quey databases that store the registered users or assignees of a resource, such as domain names, IP address blocks, etc.

* Commandline utility for `whois`.

```bash
whois hackersploit.org
Domain Name: hackersploit.org
Registry Domain ID: 77f8fe62a425487cbefef4bf7e27d2ec-LROR
Registrar WHOIS Server: whois.namecheap.com
Registrar URL: http://www.namecheap.com
Updated Date: 2022-12-22T11:20:08Z
Creation Date: 2018-04-05T11:27:07Z
Registry Expiry Date: 2024-04-05T11:27:07Z
Registrar: NameCheap, Inc.
Registrar IANA ID: 1068
Registrar Abuse Contact Email: abuse@namecheap.com
Registrar Abuse Contact Phone: +1.6613102107
Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
Registry Registrant ID: REDACTED FOR PRIVACY
Registrant Name: REDACTED FOR PRIVACY
Registrant Organization: Privacy service provided by Withheld for Privacy ehf
Registrant Street: REDACTED FOR PRIVACY
Registrant City: REDACTED FOR PRIVACY
Registrant State/Province: Capital Region
Registrant Postal Code: REDACTED FOR PRIVACY
[...]
```

* [Whois Website utility](https://who.is/) - Can also be used on IP addresses or domains

### Website footprinting with Netcraft

[Netcraft](https://www.netcraft.com/) is used to gateher information about a target domain, such as email, registrar, technologies, etc.

### DNS Recon

DNS - Domain Name Service

* [DNSRecon](https://github.com/darkoperator/dnsrecon) - Built into Kali - DNSRecon is a Python script that provides the ability to perform: Check all NS Records for Zone Transfers. Enumerate General DNS Records for a given Domain (MX, SOA, NS, A, AAAA, SPF and TXT). Perform common SRV Record Enumeration. Top Level Domain (TLD) Expansion.

```bash
dnsrecon -d hackersploit.org
[*] std: Performing General Enumeration against: hackersploit.org...
[-] All nameservers failed to answer the DNSSEC query for hackersploit.org
[*] 	 SOA dee.ns.cloudflare.com 172.64.32.93
[*] 	 SOA dee.ns.cloudflare.com 173.245.58.93
[*] 	 SOA dee.ns.cloudflare.com 108.162.192.93
[*] 	 SOA dee.ns.cloudflare.com 2803:f800:50::6ca2:c05d
[*] 	 SOA dee.ns.cloudflare.com 2a06:98c1:50::ac40:205d
[*] 	 SOA dee.ns.cloudflare.com 2606:4700:50::adf5:3a5d
[*] 	 NS jim.ns.cloudflare.com 173.245.59.125
[*] 	 NS jim.ns.cloudflare.com 108.162.193.125
[*] 	 NS jim.ns.cloudflare.com 172.64.33.125
[...]
```

* [DNSDumpster](https://dnsdumpster.com/) - "A FREE domain research tool that can discover hosts related to a domain. Finding visible hosts from the attackers perspective is an important part of the security assessment process."

### WAF with wafw00f

WAF is a Web Application Firewall.

* [wafw00f](https://github.com/EnableSecurity/wafw00f) - The Web Application Firewall Fingerprinting Tool.
  * Tells the Web Application Firewall being used to protect the site.

### Subdomain Enumeration With Sublist3r

* [Sublist3r](https://github.com/aboul3la/Sublist3r) - is a python tool designed to enumerate subdomains of websites using OSINT. It helps penetration testers and bug hunters collect and gather subdomains for the domain they are targeting. Sublist3r enumerates subdomains using many search engines such as Google, Yahoo, Bing, Baidu and Ask.
  * This can be used but can be limited due to rate limiting.

### Google Dorking

Google dorking is a way of using google searches for more potentially hidden info.

* Limit results to a domain: `site:[domain]`
  * `site:ine.com`
* Limit results to URL: `inurl:[word]`
  * `inurl:admin`
* Limit results to subdomains: `site:*.[domain]`
  * `site:*.ine.com`
* Limit results to site title: `intitle:[word]`
  * `intitle:admin`
* Limit results to file type: `filetype:[file type]`
  * `filetype:pdf`
* Limit results to indexs: `intitle:index of`
  * Let users view results for an index for a website.
* FInd older, cached versions of website: `cache:[domain]`
  * `cache:ine.com`
* Waybackmachine(archive.org) That has snapshots of older version of websites.
* [ExploitDB Google Hacking Database](https://www.exploit-db.com/google-hacking-database) - A database of google dorks that have found useful info such as "juicy" information, users, password, etc.

### Email Harvesting with theHarvester

[TheHarvester](https://github.com/laramies/theHarvester) - Similar to Sublist3r uses OSINT tools, but finds emails that belong to a domain that may be publically available or have been leaked.

* `theHarvester -d [domain] -b [databases`
  * `theHarvester -d pm.me -b google,linkedin,dnsdumpster,duckduckgo`

### Leaked Password Databases

* [HaveIBeenPwned](https://haveibeenpwned.com/) - Check if your email or phone is in a data breach

## Active Information Gathering

Active Information Gathering is actively interacting with the targets systems to gather information.

### DNS Zone Transfers

DNS(Domain Name System) Servers, or name servers, are used to resolve domain names to IP addresses. DNS is setup by a number of companies, like Google(8.8.8.8) and Cloudflare(1.1.1.1).

In certain cases. DNS server admins may want to copy or transfer zone files from one DNS server to another. This process is known as a Zone Transfer. If this is misconfigured and left unsecured, this funcationality can be abused by attackers to copy the zone file from the primary DNS server to another. This can provide penetration testeres with a wode view of an organizations network layout. It can also in some cases, internal network addresses may be found on an organizations DNS server.

### DNS Records

* A - Resolves a hostname or domain to an IPv4 Address
* AAAA - Resolves a hostname or domain to an IPv6 Address
* NS - Refers to the domains nameserver
* MX - Refers a domain to a mail server
* CNAME - Used for domain aliases
* TXT - Text record
* HINFO - Host information
* SOA - Domain Authority
* SRV - Service Records
* PRT - Resolves and IP address to a hostname

### DNS Interrogation

DNS interrogation is the process of enumerating DNS Records for a speficic domain.T he objective of the this is to the probe a DNS Server to provide us weith DNS record for the specified domain. This can provide us with important information such as the IP address, subdomains, mail server addresses, etc.

## Demo

[Zonetransfer.me](https://zonetransfer.me)

[DNSDumpster](https://dnsdumpster.com)&#x20;

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

#### DNSRecon:

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### DNSEnum:

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

This is for active recon. This can enumerate publically available records, as well as it can perform Zone Transfer automatically, DNS BruteForce to identify record and subdomains. &#x20;

#### DIG

DIG is a DNS Lookup Utility

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

#### fierce

A DNS reconnaissance tool for locating non-contiguous IP space. Can be used to BruteForce DNS records and/or subdomains.&#x20;

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Host Discovery with NMap

Finding your IP address and subnet of the network youre on `ip a`&#x20;

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

With Nmap we use the `-sn` argument, for no port scan. This is just to discover hosts that are online and is known as a ping scan or ping sweep. &#x20;

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### Netdiscover

`sudo apt install -y netdiscover` &#x20;

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Port scanning with NMap

The target of this is to obtain as much info on a speficic host on services, versions, OS, etc. with both TCP and UPD scanning.

In my example above, I will have 3 machines I can/will be targeting. .81, .82, and .116.

Default scan of nmap `nmap 192.178.1.81` does a defauly SYN scan