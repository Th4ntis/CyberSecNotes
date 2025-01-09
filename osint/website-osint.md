# Website OSINT

## Websites

* [BuiltWith](https://builtwith.com/)
* [Domain Dossier](https://centralops.net/co/)
* [DNSlytics](https://dnslytics.com/reverse-ip)
* [SpyOnWeb](https://spyonweb.com/)
* [Virus Total](https://www.virustotal.com/)
* [Visual Ping](https://visualping.io/)
* [Back Link Watch](http://backlinkwatch.com/index.php)
* [View DNS](https://viewdns.info/)
* [Pentest-Tools Subdomain Finder](https://pentest-tools.com/information-gathering/find-subdomains-of-domain)
* [Spyse](https://spyse.com/)
* [crt.sh](https://crt.sh/)
* [Shodan](https://shodan.io)
* [Wayback Machine](https://web.archive.org/)

## Tools

* Wappalyzer Plugin/Extention
* [Subfinder](https://github.com/projectdiscovery/subfinder)

```
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
subfinder -d domain
```

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

Put this into a file for httprobe&#x20;

* [Assetfinder](https://github.com/tomnomnom/assetfinder)

```
go install -v github.com/tomnomnom/assetfinder@latest
assetfinder domain
```

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

Put this into a file for httprobe&#x20;

* [httprobe](https://github.com/tomnomnom/httprobe)

```
go install -v github.com/tomnomnom/httprobe@latest
cat tesla.txt | sort -u | httprobe -s -p https:443
```

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Only returns sites that are up/active

* [Amass](https://github.com/OWASP/Amass)

```
go install -v github.com/owasp-amass/amass/v4/...@master
amass enum -d domain
```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* [GoWitness](https://github.com/sensepost/gowitness/wiki/Installation)

```
go install github.com/sensepost/gowitness@latest
gowitness file -f ./alive.txt -P ./pics --no-http
```

strip http/https/:443 from the alive.txt made from httprobe

![](<../.gitbook/assets/image (11).png>)  &#x20;

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

* whois

```
whois domain
```

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
