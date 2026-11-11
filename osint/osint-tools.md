---
description: Helpful links and resources for Cyber Security Analysts and Researchers
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# OSINT Tools

Resources to find various OSINT platforms:

* [OSINT4ALL](https://start.me/p/L1rEYQ/osint4all)
* [OHSHINT](https://ohshint.gitbook.io/oh-shint-its-a-blog/)
* [Awesome OSINT](https://github.com/jivoi/awesome-osint)

{% hint style="warning" %}
No one tool is the end all-be-all, please make sure to use multiple resources to gather and collect information.
{% endhint %}

### Contents

* Google and Google Dorking
* IP/Domain OSINT
* Email/Username OSINT
* Social Media OSINT
* Websites
* Business OSINT
* Wireless OSINT
* Frameworks
* Passwords
* Physical Location
* URL and URL Sandboxing
* Image
* People Search/PII
* Phone Numbers
* Additional OSINT

## Google and Google Dorking

We all know Google is a search engine that collects and indexes various websites from all over the internet, but some don't know how powerful it really is. Google hacking, also named Google dorking, is a technique that uses Google Search and other Google applications to find security holes in the configuration and computer code that websites are using.

#### Links

* [TryHackMe – Google Dorking Room](https://tryhackme.com/room/googledorking)
* [Fast-Google-Dorks-Scan GitHub](https://github.com/IvanGlinkin/Fast-Google-Dorks-Scan)

### What is Dorking

**Dorking** is basically an advanced search where we use operators that function as a filter to direct the search exactly where we want. We also use symbols to search for exact words or phrases. This helps us search almost any search engine on the internet. It involves making use of search engines to their complete potential to uncover outcomes that are not noticeable with a routine search. It enables us to refine our searches and dive deeper, and with better accuracy, right into web pages and files that are available online. Revealing hidden documents and security defects by dorking does not require a great deal of technical knowledge - it comes down to learning just a few search strategies and using them across a variety of search engines.

### Why we need Google dorks

Everyone can use Google dorks for a different purpose. Some of the most common reasons:

* Cyber security roles use Google dorks to find critical information that can be exposed by mistake, or knowingly, so that they can later hide or delete it before anyone can use it for the wrong purpose.
* Researchers, content writers, journalists, etc. use Google dorks to gather all the information available on a particular topic so they can use it to reach their own goals.
* Students use Google dorks to find answers to their questions, or to find leaked versions of a course or a book for free.
* Companies and their employees use Google dorks to gather information about their competitors and find honest reviews of their products or services, which in turn helps their company grow faster.

### What can we find from Google dorks

Google dorks can find a variety of information, but they are mainly used to find:

* Critical information about a website, company, organization, software, etc.
* Blogs, articles, research papers, etc. on a particular topic
* Leaked documents, courses, eBooks, etc.
* Reviews about a company and its products and services
* Solutions and answers to textbook questions

There are many other kinds of information that can be found via Google dorks very easily.

### Using Google Dorks

|                   Dork                  |                                                 Used for                                                 |                Example               |
| :-------------------------------------: | :------------------------------------------------------------------------------------------------------: | :----------------------------------: |
|    `"specified_phrase or statement"`    |                      Shows only those pages that contain the exact word or statement                     |        `"Is hacking illegal"`        |
|                 `site:`                 |                  Removes search results from all other websites except the specified one                 |       `site:github.com th4ntis`      |
|         `inurl:specified_phrase`        |                      Shows search results that contain the specified word in the URL                     |        `inurl:ethical hacking`       |
|           `inurl:word1 word2`           |                      Shows search results that contain either of the words, or both                      |      `inurl:hacking programming`     |
|          `allinurl:word1 word2`         |                       Shows search results that contain both of the specified words                      |    `allinurl:hacking programming`    |
|          `intitle:word1 word2`          | Shows results that mention the first word in their title and the specified word anywhere in the document |     `intitle:hacking networking`     |
|                 `cache:`                |                       Shows a cached version of the website if the website is down                       |          `cache:netflix.com`         |
|              `intext:word1`             |                  Shows only pages containing that specific word somewhere in the context                 |         `intext:bug hunting`         |
|         `allintext:word1 word2`         |                 Only shows pages containing the specified words somewhere in the context                 |    `allintext:hacking networking`    |
|           `intitle:"index of"`          |                                          Shows open FTP servers                                          | `intitle:"index of spiderman movie"` |
|         `inurl:view/index.shtml`        |                             Shows live cameras that don't have any protection                            |       `inurl:view/index.shtml`       |
| `filetype:pdf/doc/ppt specified_phrase` |   Shows only pages that contain a document of that type and contain the specific word in the file name   |    `filetype:pdf ethical hacking`    |
|                   `+`                   |                             Shows pages that must contain the specified word                             |    `ethical hacking + free course`   |
|                   `-`                   |                                Removes results that contain certain words                                |    `ethical hacking - paid course`   |
|                 `feed:`                 |                            Shows the specified RSS feed for the specified work                           |            `feed:hacking`            |
|                  `ip:`                  |                                 Finds websites organized by specified IP                                 |           `ip:54.239.28.85`          |

We can use Google's [normal search](https://www.google.com/) as well as their [Advanced Search page](https://www.google.com/advanced_search). Of course we can combine these searches as well.

We can also use BOOLEAN searches in Google by using AND / OR:

```
google dorking filetype:pdf OR filetype:doc OR filetype:docx
```

## IP/Domain OSINT

When researching IP addresses, it is important that we know the context of the search we are performing. There are a multitude of sources to research IP addresses, and they can vary depending on what information we want to learn about them.

For offensive security, threat hunting, and attack surface mapping, we want current registration data and any associated data points that our searches may return. These can include hosted domains, ASN, associated network artifacts, etc.

For defensive operations, such as those of the security blue team, we are looking for historical data and activity data of the IP address.

Domains, more than almost any other target, have one of the largest assortments of associated data points. The most important things we will look for out of this section are the registration data, the hosting data, site information, archived data, and analytics.

There are tons of highly effective tools for subdomain enumeration and brute forcing, but they can be quite noisy. During the passive recon phase of a penetration test, we can start with any subdomains recorded by other sources to plan out our attack/test.

* [RDAP](https://client.rdap.org/) - **Registration Data Access Protocol** is the successor to WHOIS. Like WHOIS, RDAP provides access to information about Internet resources (domain names, autonomous systems, and IP addresses). Unlike WHOIS, RDAP provides:
  * a machine-readable representation of registration data;
  * differentiated access;
  * structured request and response semantics;
  * internationalisation;
  * extensibility.
* [Whois](https://www.whois.com/whois) - a WHOIS domain lookup allows you to trace the ownership and tenure of a domain name.
* [Shodan.io](https://www.shodan.io/) - a search engine that lets users search for various types of servers connected to the internet using a variety of filters.
* [VirusTotal](https://www.virustotal.com/gui/home/upload) - analyze suspicious files, domains, IPs, and URLs to detect malware and other breaches, and automatically share them with the security community.
* [Web-Check.xyz](https://web-check.xyz) -
* [Fofa](https://en.fofa.info) -
* [Spur](https://spur.us/) -
* [AbuseIPDB](https://www.abuseipdb.com/) - a project dedicated to helping combat the spread of hackers, spammers, and abusive activity on the internet.
* [Cisco Talos Intelligence](https://talosintelligence.com/) - "Search by IP, domain, or network owner for real-time threat data."
* [IBM X-Force](https://exchange.xforce.ibmcloud.com/) - scan for a multitude of things such as IP/domain, file hash, vulnerabilities, upload files for analysis, etc. A threat intelligence sharing platform enabling research on security threats, aggregation of intelligence, and collaboration with peers.
* [IP.Teoh.io](https://ip.teoh.io/vpn-detection) - VPN & Proxy IP Detection Tool. Check if an IP is currently blacklisted or is using a VPN/proxy.
* [IPVoid](https://www.ipvoid.com/) - various tools for IP information: WHOIS, DNS, DNSDIG, MX record, blacklist checks, etc.
* [ViewDNS](https://viewdns.info/) - a huge toolbox with various utilities for enumerating information about a domain.
* [DNSDumpster](https://dnsdumpster.com/) - free domain research tool that can discover hosts related to a domain.
* [MXToolbox](https://mxtoolbox.com/) - checks MX information for the given domain.
* [DNSLytics](https://dnslytics.com/) - find out everything about a domain name, IP address, or provider. Discover relations between them and see historical data. Use it for digital investigation, fraud prevention, or brand protection.
* [HostSpider](https://github.com/h3x0crypt/HostSpider) - command-line tool that gathers tons of information about a domain, including DNS records, subdomains, WHOIS, Cloudflare IP, and more!
* [OmnisintLabs](https://omnisint.io/) - Project Crobat: Rapid7's DNS database, easily searchable via a lightning-fast API, with domains available in milliseconds.
* [Sublist3r](https://github.com/aboul3la/Sublist3r) - a Python tool designed to enumerate subdomains of websites using OSINT. It helps penetration testers and bug hunters collect subdomains for the domain they are targeting, using many search engines.
  * [TryHackMe – Sublist3r room](https://tryhackme.com/room/rpsublist3r)

## Email/Username OSINT

Corporate usernames can be obnoxiously easy to guess and build. The standard of `FIRSTNAME.LASTNAME@CORP.com` is so common it's ridiculous - even more so when account management tools simply take the first half of the email and reuse it as a username. We can use schemes like this to our advantage to search for a multitude of treasures like accounts on other services with the same username, credentials found in breaches, and associated sites or tools. When searching for usernames, you can uncover linked social media accounts and tons of relevant intelligence.

### Email Search Tools

* [MXToolBox](https://mxtoolbox.com/) - collection of online tools that can gather multiple points of data surrounding an email address or domain.
* [Seon.io](https://seon.io/intelligence-tool/#email-analysis-module) - enrich user data based on a single email address.
* [Epieos](https://tools.epieos.com/) - enter an email address and see which sites it has been used on.
* [HoleHE](https://github.com/megadose/holehe) - CLI tool to check if an email is attached to an account on sites like Twitter, Instagram, Imgur, and more than 120 others.

### Email Discovery Tools

* [Hunter.io](https://hunter.io/) - discover email addresses by company name.
* [Phonebook.cz](https://phonebook.cz/) - lists all domains, email addresses, or URLs for the given input domain.
* [Voila Norbert](https://www.voilanorbert.com/) - discover email addresses by company name.
* [Connect.Clearbit](https://connect.clearbit.com/) - email discovery tool, only works in Chrome.
* [Email Format](https://www.email-format.com/) - find the email address format for a given company or domain.
* [Snov.io](https://snov.io/email-finder) - locate employee email addresses via domain name.
* [TheHarvester](https://github.com/laramies/theharvester) - the de facto standard for email intelligence gathering. It checks a large array of sources to pull together information and can leverage APIs of other services such as Spyse or Shodan to improve the search (these require an API key). I have found that between the above HTML tools and this, it will satisfy your email searching needs.
* [Email Hippo](https://tools.verifyemailaddress.io/)
* [Email Checker](https://email-checker.net/validate)

### Tools

* [breach-parse](https://github.com/hmaverickadams/breach-parse)

```
breach-parse
```

[Breached password list from magnet link](https://magnet/?xt=urn:btih:7ffbcd8cee06aba2ce6561688cf68ce2addca0a3\&dn=BreachCompilation\&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80\&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969\&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969\&tr=udp%3A%2F%2Fglotorrents.pw%3A6969\&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337)

* [theHarvester](https://github.com/laramies/theHarvester)

```
theHarvester -d domain -b search
```

image 5.png

* [h8mail](https://github.com/khast3x/h8mail)

```
h8mail -t target@domain.com
```

image 6.png

### Username Search Tools

* [WhatsMyName](https://whatsmyname.app/) - enumerate usernames across many different websites.
  * [WhatsMyName GitHub](https://github.com/WebBreacher/WhatsMyName)
* [UserSearch](https://usersearch.org/index.php) - search engine for usernames.
* [Name Check](https://namechk.com/) - see if a username is available across multiple platforms.
* [NameCheckup](https://namecheckup.com/)
* [Sherlock](https://github.com/sherlock-project/sherlock) - hunt down social media accounts by username across social networks.
* [socialscan](https://github.com/iojw/socialscan) - Python library and CLI for accurately querying username and email usage on online platforms.
* [AnalyzeID](https://analyzeid.com/username/) - social media username checker. Gather information on the taken username and get a summary of who the person is.
* [IDCrawl](https://www.idcrawl.com/) - a free people search engine that organizes social network information, deep web information, phone numbers, email addresses, and more.

```
sherlock user
```

image 7.png

## Social Media OSINT

Social media is a huge part of the internet now - from personal accounts, businesses, and news outlets to bots, it's very helpful to find information on them. This doesn't include just Facebook or Twitter; it can include things like Discord, Telegram, Snapchat, and others.

### Facebook

* [Codeofaninja](https://www.codeofaninja.com/tools/find-facebook-id/) - "Get Facebook ID" provides an easy and fast way to find a Facebook page's or profile's numeric ID.
* [CSE Facebook Image Search](https://cse.google.com/cse?cx=013991603413798772546:jyvyp2ppxma#gsc.tab=0) - use keywords to search Facebook for images.
* [CSE Facebook Search](https://cse.google.com/cse?cx=016621447308871563343:vylfmzjmlti#gsc.tab=0) - obtain overall results, pages, groups & photos.
* [Intelligence X](https://intelx.io/tools?tab=facebook) - Facebook Graph Searcher.
* [IntelTechniques](https://inteltechniques.com/tools/Facebook.html) - Facebook search tool.
* [Lookup-ID](https://lookup-id.com/) - Facebook profile ID / group ID / page ID lookup resource.
* [OSINT Combine – Social Geo Lens](https://www.osintcombine.com/social-geo-lens) - a map-based interface for geo searching on social media platforms.
* [OSINT Combine – Facebook Search Tools](https://www.osintcombine.com/facebook-search-tools) - quickly search for multiple keywords from a list or open mutual friends for multiple profiles at the same time.
* [Plessas Facebook Matrix](https://plessas.net/facebookmatrix) - Kirby Plessas's formulas for searching Facebook.
* [Socmint Tool](http://socmint.tools/) - Graph search tool.
* [Sowdust GitHub](https://sowdust.github.io/fb-search/)
* [Sowdust Graph Tips](https://www.sowsearch.info/) - replacement Graph Search developed by Sowdust.
* [Who Posted What](https://www.whopostedwhat.com/) - a non-public Facebook keyword search for people who work in the public interest. Allows you to search keywords on specific dates.

### Twitter

* [Nixintel – How to find timestamps](https://nixintel.info/osint/how-to-find-timestamps-for-verification/) - blog on finding timestamps for verification (2022).
* [Analyze Words](https://liwc.net/analyzewords/index.php)
* [Aware-Online](http://aware-online.com/en/osint-tools/twitter-search-tool/)
* [Birdhunt](https://birdhunt.co/)
* [Botometer](https://botometer.osome.iu.edu/)
* [Codeofaninja](https://www.codeofaninja.com/tools/find-twitter-id/) - easy way to get a Twitter profile's numeric ID.
* [Foller](https://foller.me/)
* [Followerwonk](https://followerwonk.com/)
* [Geo Social Footprint](http://geosocialfootprint.com/)
* [Hash At It](https://hashatit.com/)
* [IntelTechniques](https://inteltechniques.com/tools/Twitter.html)
* [Intelx](https://intelx.io/tools?tab=twitter)
* [Make Adverbs Great Again](https://makeadverbsgreatagain.org/allegedly/)
* [Mentionmapp](https://mentionmapp.com/)
* [One Million Tweet Map](https://onemilliontweetmap.com/)
* [OSINT Combine – Social Geo Lens](https://osintcombine.com/social-geo-lens)
* [Real Top Tweeps](https://realtoptweeps.com/rankings/)
* [Sleeping Time](http://sleepingtime.org/)
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
* [Twitonomy](https://www.twitonomy.com/)

#### Tools

* [Treeverse](https://treeverse.app/)
* [Twitter Video Downloader](https://www.downloadtwittervideo.com/)
* [Twitter Video Downloader](https://twittervideodownloader.com/)
* [Twitter Video Downloader](https://savetweetvid.com/)

### LinkedIn

* [Are You Linked In?](https://www.cqcore.uk/are-you-linked-in/) - blog by Ginger T & Ritu Gill on how to search LinkedIn without being logged in (2021).
* [Free People Search Tool](https://freepeoplesearchtool.com/) - find people easily on LinkedIn.
* [Custom Search Engine](https://cse.google.com/cse?cx=006639709984028990467:nl9wxsfepb0#gsc.tab=0) - UK LinkedIn Search (1).
* [Custom Search Engine](https://cse.google.co.nz/cse?cx=014394093098352383268:w7sqo_x4rb0) - UK LinkedIn Search (2).
* [IntelTechniques](https://inteltechniques.com/tools/Linkedin.html) - LinkedIn search tool.
* [Recruitment Geek](https://recruitmentgeek.com/tools/linkedin/?sthash.Ls1u5yzO.mjjo#gsc.tab=0) - LinkedIn X-ray search.

### Instagram

* [Nixintel – How to find timestamps](https://nixintel.info/osint/how-to-find-timestamps-for-verification/) - blog on finding timestamps for verification (2022).
* [Nixintel – Instagram OSINT](https://nixintel.info/osint-tools/instagram-osint-a-promising-new-python-tool/) - tutorial on how to install InstaScraper.
* [TOCP – How to search Instagram, part 1](https://osintcurio.us/2019/07/16/searching-instagram/) - Technisette on searching Instagram for people, stories, keywords, hashtags, locations (2019).
* [TOCP – How to search Instagram, part 2](https://osintcurio.us/2019/10/01/searching-instagram-part-2/) - continues the tutorial: businesses, deleted content, tracking followers (2019).
* [Codeofaninja](https://www.codeofaninja.com/tools/find-instagram-user-id/) - get an Instagram account's numeric ID by username.
* [Download Gram](https://downloadgram.app/) - Instagram downloader for photos and videos.
* [InstaDP](https://www.instadp.com/)
* [Imginn](https://imginn.com/) - download Instagram photos, videos, and story highlights.
* [Instaloader](https://github.com/instaloader/instaloader) - download pictures (or videos) along with their captions.
* [IntelTechniques](https://inteltechniques.com/tools/Instagram.html) - Instagram search tool.
* [InstaLooter](https://github.com/althonos/InstaLooter) - API-less Instagram pictures and videos downloader.
* [iZuum](https://izuum.net/) - Instagram profile downloader.
* [OSINT Combine – Instagram Explorer](https://www.osintcombine.com/instagram-explorer) - find images by date on Instagram at particular locations.
* [Picnob](https://www.picnob.com/) - browse Instagram profiles without an account.
* [Picuki](https://www.picuki.com/) - Instagram editor & viewer.
* [Toutatis](https://github.com/megadose/toutatis) - extract information from Instagram accounts such as emails & phone numbers.
* [Who Posted What](https://www.whopostedwhat.com/) - finds posts on a date tagged with a location, for people who work in the public interest.
* [Wopita](https://wopita.com/)

### Discord

A helpful resource on how to perform OSINT on Discord can be found [here](https://osintcurio.us/2021/05/06/investigating-discord-a-primer/). Credit to [BOsintBlanc](https://twitter.com/bosintblanc).

* [Disboard, Discord Servers](https://disboard.org/)
* [Discord Bee](https://discordbee.com/)
* [Discord Bot List](https://discordbotlist.com/)
* [DiscoList](https://discolist.net/) - added by [Blackholered](https://github.com/blackholered)
* [Discord Centre](https://discord.center/)
* [Discord.com, Discord Bots](https://discord.com/invite/0cDvIgU2voWn4BaD)
* [Discord History Tracker](https://dht.chylex.com/)
* [Discord Hub](https://discordhub.com/user/search)
* [Discord ID Creation Date Checker](https://hugo.moe/discord/discord-id-creation-date.html)
* [Discord ID Lookup](https://discord.id/)
* [Discord Servers](https://discordservers.com/)
* [Public Discord Bots & Servers](https://discord.me/servers)
* [Top.gg, Discord Bots & Servers](https://top.gg/)

### Snapchat

* [Snapchat Maps](https://map.snapchat.com)

## Websites

* [BuiltWith](https://builtwith.com/)
* [Domain Dossier](https://centralops.net/co/)
* [DNSlytics](https://dnslytics.com/reverse-ip)
* [SpyOnWeb](https://spyonweb.com/)
* [VirusTotal](https://www.virustotal.com/)
* [Visual Ping](https://visualping.io/)
* [Back Link Watch](http://backlinkwatch.com/index.php)
* [ViewDNS](https://viewdns.info/)
* [Pentest-Tools Subdomain Finder](https://pentest-tools.com/information-gathering/find-subdomains-of-domain)
* [Spyse](https://spyse.com/)
* [crt.sh](https://crt.sh/)
* [Shodan](https://shodan.io)
* [Wayback Machine](https://web.archive.org/)

### Tools

* Wappalyzer plugin/extension
* [Subfinder](https://github.com/projectdiscovery/subfinder)

```
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
subfinder -d domain
```

image 10.png

Put this into a file for httprobe.

* [Assetfinder](https://github.com/tomnomnom/assetfinder)

```
go install -v github.com/tomnomnom/assetfinder@latest
assetfinder domain
```

image 11.png

Put this into a file for httprobe.

* [httprobe](https://github.com/tomnomnom/httprobe)

```
go install -v github.com/tomnomnom/httprobe@latest
cat tesla.txt | sort -u | httprobe -s -p https:443
```

image 12.png

Only returns sites that are up/active.

* [Amass](https://github.com/OWASP/Amass)

```
go install -v github.com/owasp-amass/amass/v4/...@master
amass enum -d domain
```

image 13.png

* [GoWitness](https://github.com/sensepost/gowitness/wiki/Installation)

```
go install github.com/sensepost/gowitness@latest
gowitness file -f ./alive.txt -P ./pics --no-http
```

Strip `http`/`https`/`:443` from the `alive.txt` made from httprobe.

image 14.png

image 15.png

image 16.png

* whois

```
whois domain
```

image 17.png

## Business OSINT

* [OpenCorporates](https://opencorporates.com/)
* [AI HIT](https://www.aihitdata.com/)

## Wireless OSINT

* [WiGLE](https://wigle.net/)

## Frameworks

* [Recon-ng](https://github.com/lanmaster53/recon-ng)
* [Maltego](https://www.maltego.com/downloads/)
  * [Requires an account.](https://www.maltego.com/ce-registration/?utm_source=maltego-suite\&utm_medium=software)

## Passwords

* [Dehashed](https://dehashed.com/) - has a fee
* [Hashes.org](https://hashes.org)
* [WeLeakInfo](https://weleakinfo.to/v2/)
* [LeakCheck](https://leakcheck.io/) - has a fee
* [SnusBase](https://snusbase.com/)
* [Scylla.sh](https://scylla.sh/)
* [HaveIBeenPwned](https://haveibeenpwned.com/)

## Physical Location

* [Google Maps](http://maps.google.com)
  * Google Satellite Images
  * Google Street View
* [Google Earth](https://earth.google.com/)

## URL and URL Sandboxing

* [URLScan](https://urlscan.io/) - "A sandbox for the web." Scans a submitted URL for malicious intent; details in [their about page](https://urlscan.io/about/).
* [URLHaus](https://urlhaus.abuse.ch/) - search IP/domain, URL, MD5, SHA256, and more to see if they have been flagged as malicious/suspicious.
* [URLVoid](https://www.urlvoid.com/) - website reputation checker. Shows location, IP, WHOIS, DNS records, and whether various services have blacklisted the URL.
* [Browserling](https://www.browserling.com/) - sandbox URLs on various browsers and interact with them in a live secure environment.
* [Wannabrowser](https://www.wannabrowser.net/) - simulate any browser.
* [Hybrid-Analysis](https://hybrid-analysis.com/) - malware analysis service.
* [Joe Sandbox](https://www.joesandbox.com/) - detects and analyzes potentially malicious files and URLs on various OSes.
* [Triage](https://tria.ge/) - malware analysis sandbox.
* [Any.run](https://any.run/) - an interactive online malware analysis service for dynamic and static research of most types of threats using any environment. Free to use and sign up for.

## Image

### Websites

* [Google Image Search](https://images.google.com)
* [Yandex](https://yandex.com/images/)
* [TinEye](https://tineye.com)

### Tools

* [ExifTool](https://exiftool.org/)

```
sudo apt install libimage-exiftool-perl
exiftool IMAGE
```

image 8.png

## People Search/PII

This section will get stalker-ish real quick. While limited in usefulness for a penetration test, it can help you discover all the interesting data surrounding a person, or link data you have found back to an individual. For those who would like a premium all-in-one option, there are a few handy platforms that can make collection faster and easier.

* [WhitePages](https://www.whitepages.com/)
* [TruePeopleSearch](https://www.truepeoplesearch.com/)
* [FastPeopleSearch](https://www.fastpeoplesearch.com/)
* [FastBackgroundCheck](https://www.fastbackgroundcheck.com/)
* [WebMii](https://webmii.com/)
* [PeekYou](https://peekyou.com/)
* [411](https://www.411.com/)
* [Spokeo](https://www.spokeo.com/)
* [That'sThem](https://thatsthem.com/)
* [Social Links](https://sociallinks.io/) - premium collection of OSINT tools focusing on data gathered from social media and other sites.
* [Gamayun](https://sociallinks.io/products/gamayun) - a web-based tool designed for conducting OSINT investigations when searching for emails, locations, phone numbers, aliases, and photos.
* [SL-Pro](https://sociallinks.io/products/sl-pro) - a professional tool for searching data from social media accounts, the Darknet, blockchains, and internet data leaks. It comes with API integrations linking to 1100 methods of search across 50+ sources of data on over 800 million identities.
* [Melissa](https://www.melissa.com/v2/lookups/) - arguably one of the best search tools for people. Provides a massive amount of tools and resources to search people by name, address, phone number, and so on, plus maps, federal data, property records, and more.
* [SocialCatfish](https://socialcatfish.com) - find connections and verify a person's online identity using a name, image, email address, phone number, username, or physical address.
* [GoFindWho](https://gofindwho.com/) - find people for free by phone number, name, email address, and username on Facebook and in public records.
* [EffectGroup](https://effectgroup.io) - search people by username, email address, real name, or phone number and build a dossier on your target. Searches social media sites, data breaches, documents, and more. Requires a paid subscription after first search.
* [How to find information on anyone – Medium article](https://medium.com/the-first-digit/osint-how-to-find-information-on-anyone-5029a3c7fd56)

### Name Search

Name search records can get muddy really quickly when dealing with names like "John Smith"; however, many tools will allow you to refine the search with other data points such as location or other context. As with any search tool, the more data you feed it, the more accurate your results will be. As always, I like to start with one of Michael Bazzell's handy tools, Name.html. This tool will search databases of names that return associated data points for building a full profile of your target. From here, the next step is to start looking for any public records associated with the name you are searching for. Remember to use location to aid in context.

* [Xlek](https://xlek.com) - searches millions of online records for a given name.
* [That'sThem](https://thatsthem.com/) - find all sorts of information about a person including address, email, even their car's VIN number.
* [Public Records](https://www.blackbookonline.info/) - search public government records for entries relating to your target.
* [PeekYou](https://www.peekyou.com/) - popular people search engine.
* [BeenVerified](https://www.beenverified.com/) - people search engine that can return people, vehicle, property, and contact info.
* [OpenSanctions](https://opensanctions.org/) - the persons-of-interest database.
* [Verecor](https://verecor.com/) - generic people search site for U.S. citizens.
* [UFind.Name](https://ufind.name/) - search for a person's name and see matching results including LinkedIn and Facebook accounts, white page results, vehicle registration database entries, marketing data, and more.

### Gov and Business Records

* [GLEIF](https://search.gleif.org/) - look up company information from the Global Legal Entity Identifier Foundation (GLEIF).
* [OpenCorporates](https://opencorporates.com) - giant public database of corporate information.
* [Public Records](https://www.blackbookonline.info/) - search public government records for entries relating to your target.
* [PACER Court Case documents](https://pacer.uscourts.gov/)
* [Legacy.com Obituary Search](https://www.legacy.com/search)
* [Background checks](https://freebackgroundcheck.org/) - search for mentions of a person in court cases, contact information, assets, police records, and much more!
* [SEC filings](https://www.sec.gov/edgar.shtml) - all companies, foreign and domestic, are required to file registration statements, periodic reports, and other forms electronically through EDGAR. Anyone can access and download this information for free.
* [Vital Records Search Tools](https://stevemorse.org/index.html) - tools for finding immigration records, census records, vital records, and for dealing with calendars, maps, foreign alphabets, and numerous other applications. Created by Stephen P. Morse.
* [JudyRecords](https://www.judyrecords.com/) - search over 580 million United States court cases.
* [CaseLaw](https://case.law/) - a free tool that allows you to search over 1.7 million U.S. federal cases and over 4.9 million state cases.
* [CourtRecords](https://www.courtrecord.net/) - search complete and up-to-date public court records in the U.S.
* [Public Records](https://publicrecords.searchsystems.net/) - search for United States public records.
* [Arrests](https://arrests.org)

### Voter Records

* [Voter Records](https://www.voterrecords.com)

## Phone Numbers

### Websites

* [TrueCaller](https://www.truecaller.com/)
* [CallerID Test](https://calleridtest.com/)
* [Infobel](https://infobel.com/)
* [Carrier lookup](https://freecarrierlookup.com/) - enter a phone number and get the carrier name and whether the number is wireless or landline.
* [Number Validator](https://www.twilio.com/lookup) - search phone number format and origin.
* [CallerID check](http://calleridservice.com/) - a database of caller names used to identify the name of a caller when receiving an inbound call from the United States or Canada.
* [TrueCaller Caller ID check](https://www.truecaller.com/) - one of the best Caller ID utilities.
* [Spy Dialer](https://spydialer.com/default.aspx) - reverse phone number lookup for cell phones, VOIP, and landlines.
* [Seon.io](https://seon.io/intelligence-tool/#phone-analysis-module) - confirm if the number is valid, and detect the origin country, carrier, and number type.
* [800 Notes](https://800notes.com/) - a crowd-sourced reverse phone number search. Good for identifying scammer numbers.
* [Caller Name](https://callername.com/) - free phone number lookup service for cell phone, VoIP, or landline numbers.

### Tools

* [Phoneinfoga](https://github.com/sundowndev/phoneinfoga)

```
bash <( curl -sSL https://raw.githubusercontent.com/sundowndev/phoneinfoga/master/support/scripts/install )
sudo install ./phoneinfoga /usr/local/bin/phoneinfoga
```

```
phoneinfoga scan -n (countrycode)(phonenumber)
phoneinfoga serve -p 8080
```

image 9.png

## Additional OSINT

* [Spiderfoot](https://github.com/smicallef/spiderfoot) - automates OSINT for threat intelligence and mapping your attack surface.
* [CyberChef](https://gchq.github.io/CyberChef/) - [Decode Base64](https://icyberchef.com/#recipe=From_Base64\('A-Za-z0-9%2B/%3D',true\)\&input=U0dGamF5QjBhR1VnVUd4aGJtVjBJUT09), [Convert data from a hexdump, then decompress](https://icyberchef.com/#recipe=From_Hexdump\(\)Gunzip\(\)\&input=MDAwMDAwMDAgIDFmIDhiIDA4IDAwIDEyIGJjIGYzIDU3IDAwIGZmIDBkIGM3IGMxIDA5IDAwIDIwICB8Li4uLi6881cu/y7HwS4uIHwKMDAwMDAwMTAgIDA4IDA1IGQwIDU1IGZlIDA0IDJkIGQzIDA0IDFmIGNhIDhjIDQ0IDIxIDViIGZmICB8Li7QVf4uLdMuLsouRCFb/3wKMDAwMDAwMjAgIDYwIGM3IGQ3IDAzIDE2IGJlIDQwIDFmIDc4IDRhIDNmIDA5IDg5IDBiIDlhIDdkICB8YMfXLi6%2BQC54Sj8uLi4ufXwKMDAwMDAwMzAgIDRlIGM4IDRlIDZkIDA1IDFlIDAxIDhiIDRjIDI0IDAwIDAwIDAwICAgICAgICAgICB8TshObS4uLi5MJC4uLnw), [Decrypt and disassemble shellcode](https://icyberchef.com/#recipe=RC4\(%7B'option':'UTF8','string':'secret'%7D,'Hex','Hex'\)Disassemble_x86\('64','Full%20x86%20architecture',16,0,true,true\)\&input=MjFkZGQyNTQwMTYwZWU2NWZlMDc3NzEwM2YyYTM5ZmJlNWJjYjZhYTBhYWJkNDE0ZjkwYzZjYWY1MzEyNzU0YWY3NzRiNzZiM2JiY2QxOTNjYjNkZGZkYmM1YTI2NTMzYTY4NmI1OWI4ZmVkNGQzODBkNDc0NDIwMWFlYzIwNDA1MDcxMzhlMmZlMmIzOTUwNDQ2ZGIzMWQyYmM2MjliZTRkM2YyZWIwMDQzYzI5M2Q3YTVkMjk2MmMwMGZlNmRhMzAwNzJkOGM1YTZiNGZlN2Q4NTlhMDQwZWVhZjI5OTczMzYzMDJmNWEwZWMxOQ), and more.
* [TorWhois](https://torwhois.com/) - look up a .onion address and see basic information such as date last seen, open ports, running software, and banners.
* [IntelligenceX](https://intelx.io/) - search Tor, I2P, data leaks, domains, and emails.
* [GreyNoise](https://viz.greynoise.io/) - search for devices connected to the internet.
* [Dehashed](https://dehashed.com/) - view leaked credentials and compromised assets.
  * [DeHashed-API-Tool](https://github.com/hmaverickadams/DeHashed-API-Tool) by Heath Adams (TCM)
* [Fast-Google-Dorks-Scan](https://github.com/IvanGlinkin/Fast-Google-Dorks-Scan)
* [Ultimate Windows Security](https://www.ultimatewindowssecurity.com/) - view Windows event codes, CVEs, and multiple other tools relating to Windows Security.
* [AlienVault OTX](https://otx.alienvault.com/) - extensive threat intelligence feed.
* [Censys](https://search.censys.io/) - assessing attack surface for internet-connected devices.
* [URL2PNG](https://www.url2png.com/) - get a screenshot of a website rather than browsing to it.
* [DNSChecker](https://dnschecker.org/all-tools.php) - a wide variety of DNS, IP, and other tools.
* [Bash.ws](https://bash.ws/) - whois, host, dig, nslookup, ping, traceroute, and geoiplookup tools on IPs and domains.
* [NSLookup.io](https://www.nslookup.io/ns-lookup/) - find all name servers for a domain name with this online DNS NS checker.
* [Malware Bazaar](https://bazaar.abuse.ch/) - search file hashes to see if they have been flagged as malicious.
* [HaveIBeenPwned](https://haveibeenpwned.com/?ref=websitehunt) - check if your email or phone is in a data breach.
* [DorkSearch](https://dorksearch.com/) - faster Google dorking.
* [ExploitDB](https://www.exploit-db.com/) - archive of various exploits.
* [Wayback Machine](https://web.archive.org/) - view content from edited, deleted, and older websites.
* [Maltiverse](https://maltiverse.com/collection) - search for indicators of compromise or something related.
* [HoneyDB](https://honeydb.io/) - provides real-time data of honeypot activity.
* [SecurityTrails](https://securitytrails.com/dns-trails) - extensive and historical DNS data.
* [ZoomEye](https://www.zoomeye.org/) - gather information about targets.
* [Pulsedive](https://pulsedive.com/) - search for threat intelligence.
* [GrayHatWarfare](https://grayhatwarfare.com/) - search public S3 buckets.
* [MHA Azure Websites](https://mha.azurewebsites.net/) - Message Header Analyzer.
* [PolySwarm](https://polyswarm.network/) - scans files and URLs for threats.
* [LeakIX](https://leakix.net/) - search publicly indexed information.
* [FullHunt](https://fullhunt.io/) - search and discover attack surfaces.
* [ONYPHE](https://www.onyphe.io/) - collects cyber-threat intelligence data.
* [Grep App](https://grep.app/) - Git repository search.
* [Vulners](https://vulners.com/search) - search vulnerabilities in a large database.
* [Netlas](https://app.netlas.io/host/) - search and monitor internet-connected assets.
* [crt.sh](https://crt.sh/) - search for certs that have been logged by CT.
* [WiGLE](https://wigle.net/) - database of wireless networks, with statistics.
* [PublicWWW](https://publicwww.com/) - marketing and affiliate marketing research.
* [Binary Edge](https://www.binaryedge.io/) - scans the internet for threat intelligence.
* [Hunter.io](https://hunter.io/) - search for email addresses belonging to a website.
* [Packet Storm Security](https://packetstormsecurity.com/) - browse latest vulnerabilities and exploits.
* [SearchCode](https://searchcode.com/) - search 75 billion lines of code from 40 million projects.
