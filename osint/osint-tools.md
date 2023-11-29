---
description: Helpful links and resources for Cyber Security Analysts and Researchers
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# OSINT Tools

Here's a list of helpful tools that can be used for [OSINT](./) and Sand-boxing for Cyber Security Analysts and Researchers. These tools can be used to looking up information on Domains, IPs, URLs, File Hashes, etc.

A good resource to find various OSINT platforms is [OSINT4ALL](https://start.me/p/L1rEYQ/osint4all), as well as [OSHINT](https://ohshint.gitbook.io/oh-shint-its-a-blog/).

{% hint style="warning" %}
No one tool is the end all-be-all, please make sure to use multiple resources to gather and collect information.
{% endhint %}

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

## Email/Username OSINT

Corporate usernames can be obnoxiously easy to guess and build. The standard of FIRSTNAME.LASTNAME@CORP.com is so common, it's ridiculous. Even more so when account management tools will simply take the first half of the email and reuse it as a username. We can use schemes like this to our advantage to search for a multitude of treasures like accounts on other services with the same username, credentials found in breaches, and associated sites or tools. When searching for usernames, you can uncover linked social media accounts and tons of relevant intelligence.

### Email Search Tools

* [MXToolBox](https://mxtoolbox.com/) - Collection of online tools that can gather multiple points of data surrounding an email address or domain
* [Seon.io](https://seon.io/intelligence-tool/#email-analysis-module) - Enrich user data based on a single email address
* [Epieos](https://tools.epieos.com/) - Enter an email address and see which sites the email address has been used.&#x20;
* [HoleHE](https://github.com/megadose/holehe) - CLI Tool to check if an email is attached to an account on sites like twitter, instagram, imgur and more than 120 others

### Email Discovery Tools

* [Hunter.io](https://hunter.io/) - Discover email addresses by company name
* [Phonebook.cz](https://phonebook.cz/) - Phonebook lists all domains, email addresses, or URLs for the given input domain.
* [Voilanorbert](https://www.voilanorbert.com/) - Discover email addresses by company name
* [Connect.Clearbit](https://connect.clearbit.com/) - Email discovery tool, only works in chrome.
* [Email Format ](https://www.email-format.com/)- Find the email address format for a given company or domain.
* [Snov.io](https://snov.io/email-finder) - Locate employee email addresses via domain name.
* [TheHarvester](https://github.com/laramies/theharvester) - This tool is the defacto standard for email intelligence gathering. It checks a large array of sources to pull together information. It can leverage APIs of other services such as Spyse or Shodan to improve the search. Remember these will require an API key to use. I have found that between the above html tools and this, it will satisfy your email searching needs.

### Username Search Tools

* [WhatsMyName](https://whatsmyname.app/) - This tool allows you to enumerate usernames across many different websites.
  * [WhatsMyName Github](https://github.com/WebBreacher/WhatsMyName)
* [UserSearch](https://usersearch.org/index.php) - Search Engine for Usernames
* [Name Check](https://namechk.com/) - See if a username is available across multiple platforms
* [Sherlock](https://github.com/sherlock-project/sherlock) - Hunt down social media accounts by username across social networks
* [SocialCcan](https://github.com/iojw/socialscan) - Python library and CLI for accurately querying username and email usage on online platforms
* [AnalyzeID](https://analyzeid.com/username/) - Social media username checker. Gather information on the taken username and get a summary of who the person is
* [IDCrawl](https://www.idcrawl.com/) - A free people search engine that organizes social network information, deep web information, phone numbers, email addresses and more

## Social Media OSINT

Social Media is huge a huge part of the internet now, from personal accounts, businesses, news outlets, to bots, it's very helpful to find information on them. This doesn't include just Facebook or Twitter, this can include things like Discord, Telegram, Snapchat, and others.

### Facebook

* [Codeofaninja](https://www.codeofaninja.com/tools/find-facebook-id/) - This tool called "Get Facebook ID" provides an easy and fast way to find a Facebook page's or Facebook profile's numeric ID.
* [CSE Facebook Image Search](https://cse.google.com/cse?cx=013991603413798772546:jyvyp2ppxma#gsc.tab=0) - Use Keywords to search Facebook for images.
* [CSE Facebook Search](https://cse.google.com/cse?cx=016621447308871563343:vylfmzjmlti#gsc.tab=0) - Obtain overall Results, Pages, Groups & Photos.
* [Intelligence X](https://intelx.io/tools?tab=facebook) - Facebook Graph Searcher.
* [Intelltechniques](https://inteltechniques.com/tools/Facebook.html) - Facebook Search Tool.
* [Lookup-ID](https://lookup-id.com/) - Facebook profile ID / Group ID / Page ID lookup resource.
* [Osint Combine](https://www.osintcombine.com/social-geo-lens) - Social Geo Lens, this tool is designed to provide a map based interface for geo searching on social media platforms.
* [Osint Combine](https://www.osintcombine.com/facebook-search-tools) - This tool is a simple way to quickly search for multiple keywords from a list or open mutual friends for multiple profiles at the same time.
* [Plessas Facebook Matrix](https://plessas.net/facebookmatrix) - This page contains Kirby Plessas Formulas for Searching Facebook.
* [Socmint Tool](http://socmint.tools/) - Graph Search Tool.
* [Sowdust Graph Tips](https://www.sowsearch.info/) - Replacement Graph Search developed by Sowdust.
* [Who Posted What](https://www.whopostedwhat.com/) - Whopostedwhat.com is a non public Facebook keyword search for people who work in the public interest. It allows you to search keywords on specific dates.

### Twitter

* [Nixintel How to find timestamps](https://nixintel.info/osint/how-to-find-timestamps-for-verification/) - Nixintel blog on how to find timestamps for verification (2022).
* [Analyze Words](https://liwc.net/analyzewords/index.php)
* [Aware-Online](http://aware-online.com/en/osint-tools/twitter-search-tool/)
* [Birdhunt](https://birdhunt.co/)
* [Botometre](https://botometer.osome.iu.edu/)
* [Codeofaninja](https://www.codeofaninja.com/tools/find-twitter-id/) - Easy way for you to get a Twitter profile's numeric ID.
* [Foller](https://foller.me/)
* [Followerwonk](https://followerwonk.com/)
* [Geo Social Footprint](http://geosocialfootprint.com/)
* [Hash At It](https://hashatit.com/)
* [Inteltechniques](https://inteltechniques.com/tools/Twitter.html)
* [Intelx](https://intelx.io/tools?tab=twitter)
* [Make Adverbs Great Again](https://makeadverbsgreatagain.org/allegedly/)
* [One Million Tweet Map](https://onemilliontweetmap.com/)
* [Osint Conbine](https://osintcombine.com/social-geo-lens)
* [Real Top Tweeps](https://realtoptweeps.com/rankings/)
* [Social Bearing](https://socialbearing.com/)
* [Spoonbill](http://spoonbill.io/)
* [Tinfoleak](https://tinfoleak.com/)
* [Tweet Beaver](https://tweetbeaver.com/)
* [Tweep Diff](https://tweepdiff.com/)
* [Tweet Map](https://www.heavy.ai/demos/tweetmap)
* [Tweet Tunnel](https://tweettunnel.com/reverse.php)
* [Twint](https://github.com/twintproject/twint)
* [Twitter's Advanced Search](https://twitter.com/search-advanced)
* [Twopcharts](https://twopcharts.com/)

Tools

* [Treeverse](https://treeverse.app/%3E)
* [Twitter Video Downloader](https://www.downloadtwittervideo.com/)
* [Twitter Video Downloader](https://twittervideodownloader.com/)
* [Twitter Video Downloader](https://savetweetvid.com/)

### Linked In

* [Are You Linked in?](https://www.cqcore.uk/are-you-linked-in/) - Blog by Ginger T & Ritu Gill on how to search linked without being logged in (2021).
* [Free Person Search Tool](https://freepeoplesearchtool.com/) - Find people easily on Linkedin.
* [Custom Search Engine](https://cse.google.com/cse?cx=006639709984028990467:nl9wxsfepb0#gsc.tab=0) - UK Linkedin Search (1).
* [Custom Search Engine](https://cse.google.co.nz/cse?cx=014394093098352383268:w7sqo\_x4rb0) - UK Linkedin Search (2).
* [Inteltechniques](https://inteltechniques.com/tools/Linkedin.html) - LinkedIn Search Tool.
* [Recruitment Geek](https://recruitmentgeek.com/tools/linkedin/?sthash.Ls1u5yzO.mjjo#gsc.tab=0) - LinkedIn Xray Search.

### Instagram

* [Nixintel How to find timestamps](https://nixintel.info/osint/how-to-find-timestamps-for-verification/) - Nixintel's blog on how to find timestamps for verification (2022).
* [Nixintel Instagram Osint](https://nixintel.info/osint-tools/instagram-osint-a-promising-new-python-tool/) - Nixintel's tutorial on how to install InstaScraper.
* [TOCP How to search Instagram part 1](https://osintcurio.us/2019/07/16/searching-instagram/) - Technisette talks through how to search Instagram, for people, stories, keywords, hashtags, locations (2019).
* [TOCP How to search Instagram part 2](https://osintcurio.us/2019/10/01/searching-instagram-part-2/) - Technisette continues her tutorial searching Instagram, for businessess, deleted content and tracking followers (2019).
* [Codeofaninja](https://www.codeofaninja.com/tools/find-instagram-user-id/) - Easy way for developers and designers to get Instagram account numeric ID by username.
* [Download Gram](https://downloadgram.app/) - Instagram downloader tool, it helps you to download Instagram photos and videos.
* [Imginn](https://imginn.com/) - Download instagram photos, videos and stories highlights.
* [Instaloader](https://github.com/instaloader/instaloader) - Download pictures (or videos) along with their captions.
* [Inteltechniques](https://inteltechniques.com/tools/Instagram.html) - Inteltechniques Instagram search tool.
* [Instalooter](https://github.com/althonos/InstaLooter) - API-less Instagram pictures and videos downloader.
* [iZuum](https://izuum.net/) - Instagram profile downloader.
* [Osint Combinne](https://www.osintcombine.com/instagram-explorer) - Find images by date on Instagram at particular locations easier and more efficient.
* [Picnob](https://www.picnob.com/) - Enables you to browse Instagram profiles without the need of an account.
* [Picuki](https://www.picuki.com/) - Instgram Editor & Viewer.
* [Toutatis](https://github.com/megadose/toutatis) - Extract information from instagrams accounts such as e-mails & phone numbers.
* [Who Posted What](https://www.whopostedwhat.com/) - Finds Posts on Date Tagged With Location, for people who work in the public interest

### Discord

A helpful resource on how to perform OSINT on Discord can be found [here](https://osintcurio.us/2021/05/06/investigating-discord-a-primer/). Credit to [BOstintBlanc](https://twitter.com/bosintblanc).

* [Disboard, Discord Servers](https://disboard.org/)
* [Discord Bee](https://discordbee.com/)
* [Discord Bot List](https://discordbotlist.com/)
* [Discord Centre](https://discord.center/)
* [Discord.com, Discord Bots](https://discord.com/invite/0cDvIgU2voWn4BaD)
* [Discord History Tracker](https://dht.chylex.com/)
* [Discord Hub](https://discordhub.com/user/search)
* [Discord ID Creation Date Checker](https://hugo.moe/discord/discord-id-creation-date.html)
* [Discord ID Lookup](https://discord.id/)
* [Discord Servers](https://discordservers.com/)
* [Public Discord Bots & Servers](https://discord.me/servers)
* [Top.gg, Discord Bots & Servers](https://top.gg/)

## URL OSINT and Sandboxing

* [URLScan](https://urlscan.io/) - "_A sandbox for the web"_ Scans submitted URL website for malicious intent details in [their about page](https://urlscan.io/about/).
* [URLHaus](https://urlhaus.abuse.ch/) - Search IP/Domain, URL, MD5, SHA256, and more to see if they have been flagged as malicious/suspicious.
* [URLVoid](https://www.urlvoid.com/) - Website reputation checker. Shows information of location, IP, WHOIS, DNS Records, and if various services have blacklisted the URL or not.
* [Browserling](https://www.browserling.com/) - Sandbox URLs on various browsers and interact with them in a live secure environment.
* [Wannabroswer](https://www.wannabrowser.net/) - Simulate any Browser
* [Hybrid-Analysis](https://hybrid-analysis.com/) - Malware Analysis Service
* [Joes Sandbox](https://www.joesandbox.com/) - "Detects and analyzes potential malicious files and URLs" on various OS
* [Triage](https://tria.ge/) - Malware Analysis Sandbox
* [Any.run](https://any.run/) - An "Interactive online malware analysis service for dynamic and static research of most types of threats using any environments. Replaces a set of tools for research". Free to use and sign up for. Can be used for "a convenient in-depth analysis of new (unidentified) malicious objects, as well as for the investigation of cyber incidentals."

## Additional Tools

* [CyberChef](https://gchq.github.io/CyberChef/) - [Decode Base64](https://icyberchef.com/#recipe=From\_Base64\('A-Za-z0-9%2B/%3D',true\)\&input=U0dGamF5QjBhR1VnVUd4aGJtVjBJUT09), [Convert data from a hexdump, then decompress](https://icyberchef.com/#recipe=From\_Hexdump\(\)Gunzip\(\)\&input=MDAwMDAwMDAgIDFmIDhiIDA4IDAwIDEyIGJjIGYzIDU3IDAwIGZmIDBkIGM3IGMxIDA5IDAwIDIwICB8Li4uLi6881cu/y7HwS4uIHwKMDAwMDAwMTAgIDA4IDA1IGQwIDU1IGZlIDA0IDJkIGQzIDA0IDFmIGNhIDhjIDQ0IDIxIDViIGZmICB8Li7QVf4uLdMuLsouRCFb/3wKMDAwMDAwMjAgIDYwIGM3IGQ3IDAzIDE2IGJlIDQwIDFmIDc4IDRhIDNmIDA5IDg5IDBiIDlhIDdkICB8YMfXLi6%2BQC54Sj8uLi4ufXwKMDAwMDAwMzAgIDRlIGM4IDRlIDZkIDA1IDFlIDAxIDhiIDRjIDI0IDAwIDAwIDAwICAgICAgICAgICB8TshObS4uLi5MJC4uLnw), [Decrypt and disassemble shellcode](https://icyberchef.com/#recipe=RC4\(%7B'option':'UTF8','string':'secret'%7D,'Hex','Hex'\)Disassemble\_x86\('64','Full%20x86%20architecture',16,0,true,true\)\&input=MjFkZGQyNTQwMTYwZWU2NWZlMDc3NzEwM2YyYTM5ZmJlNWJjYjZhYTBhYWJkNDE0ZjkwYzZjYWY1MzEyNzU0YWY3NzRiNzZiM2JiY2QxOTNjYjNkZGZkYmM1YTI2NTMzYTY4NmI1OWI4ZmVkNGQzODBkNDc0NDIwMWFlYzIwNDA1MDcxMzhlMmZlMmIzOTUwNDQ2ZGIzMWQyYmM2MjliZTRkM2YyZWIwMDQzYzI5M2Q3YTVkMjk2MmMwMGZlNmRhMzAwNzJkOGM1YTZiNGZlN2Q4NTlhMDQwZWVhZjI5OTczMzYzMDJmNWEwZWMxOQ), and more.
* [TorWhoIs](https://torwhois.com/) - Look up an .onion address and see basic information such as date last seen, open ports, running software and banners
* [IntelligenceX](https://intelx.io/) - Search Tor, I2P, data leaks, domains, and emails
* [GreyNoise](https://viz.greynoise.io/) - Search for devices connected to the internet
* [Dehashed](https://dehashed.com/) - View leaked credentials and compromised assets
  * [DeHashed-API-Too](https://github.com/hmaverickadams/DeHashed-API-Tool)l by Heath Adams(TCM)
* [Ultimate Windows Security](https://www.ultimatewindowssecurity.com/) - View Windows Event codes, CVE's, and multiple other tools relating to WIndows Security.
* [AlienVaultOTX](https://otx.alienvault.com/) - Extensive threat intelligence feed
* [Censys](https://search.censys.io/) - Assessing attack surface for internet connected devices
* [URL2PNG](https://www.url2png.com/) - Get a screenshot of a website rather than browsing to it.
* [DNSChecker](https://dnschecker.org/all-tools.php) - A wide variety of DNS, IP, and other tools.
* [Bash.ws](https://bash.ws/) - Whois, host, dig, nslookup, ping, traceroute, and geoiplookup tool on IPs and Domains
* [NSLookup.io](https://www.nslookup.io/ns-lookup/) - Find all name servers for a domain name with this online DNS NS checker
* [Malware Bazaar](https://bazaar.abuse.ch/) - Search file hashes to see if they have been flagged as malicious.
* [HaveIBeenPwned](https://haveibeenpwned.com/?ref=websitehunt) - Check if your email or phone is in a data breach
* [DorkSearch](https://dorksearch.com/) - Faster Google dorking.
* [ExploitDB](https://www.exploit-db.com/) - Archive of various exploits
* [WayBackMachine](https://web.archive.org/) - View content from edited, deleted and older websites
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
* [Packet Storm Security](https://packetstormsecurity.com/) - Browse latest vulnerabilities and exploits
* [SearchCode](https://searchcode.com/) - Search 75 billion lines of code from 40 million projects
