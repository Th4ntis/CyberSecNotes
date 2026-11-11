---
description: Open Source Intelligence
---

# 🔎 OSINT

Open Source Intelligence (OSINT) is a multi-method methodology for collecting, analyzing, and making decisions about data accessible in publicly available sources, to be used in an intelligence context. In the intelligence community, the term "open" refers to overt, publicly available sources, a way to gather information that is publicly available, essentially.

OSINT is crucial for any penetration test because it provides a foundation of publicly available information that helps testers understand the target environment. It can help identify potential attack vectors, vulnerabilities, and entry points without alerting the target or causing disruption. We can find domain names, IP addresses, technology stacks, exposed services, user accounts, and more.

There is a helpful resource called the [OSINT Framework](https://osintframework.com/) that is focused on gathering information from free tools or resources.

## Sock Puppets

### What is a Sock Puppet?

An online identity used as an alternate or fake account. The point is to make a person/account that is not you.

#### Creating a Sock Puppet

* [Creating an Effective Sock Puppet for OSINT Investigations – Introduction](https://web.archive.org/web/20210125191016/https://jakecreps.com/2018/11/02/sock-puppets/)
* [The Art Of The Sock](https://www.secjuice.com/the-art-of-the-sock-osint-humint/)
* [Reddit – My process for setting up anonymous sockpuppet accounts](https://www.reddit.com/r/OSINT/comments/dp70jr/my_process_for_setting_up_anonymous_sockpuppet/)
* [Fake Name Generator](https://www.fakenamegenerator.com/)
* [This Person Does Not Exist](https://www.thispersondoesnotexist.com/)
* [Privacy.com](https://privacy.com/) - make burner credit cards

## Search Engines

* [Google](https://www.google.com/)
* [Google Advanced Search](https://www.google.com/advanced_search)
* [Google Search Guide](http://www.googleguide.com/print/adv_op_ref.pdf)
* [Bing](https://www.bing.com/)
* [Bing Search Guide](https://www.bruceclay.com/blog/bing-google-advanced-search-operators/)
* [Yandex](https://yandex.com/)
* [DuckDuckGo](https://duckduckgo.com/)
* [DuckDuckGo Search Guide](https://help.duckduckgo.com/duckduckgo-help-pages/results/syntax/)
* [Baidu](http://www.baidu.com/)

## Operator Examples

* `site:reddit.com`
* `filetype:pdf`
* `"Exact results"`
* `AND`
* `OR`
* `-www`
* `intext:password` - shows the term "password" in the text
* `inurl:password` - shows if the term "password" is in the URL

> For a full dorking table and more operators, see > Google and Google Dorking.

## Technologies

Identifying the technologies used on a website is important for identifying versioning, to then search for vulnerabilities and exploits. For this I use:

* [Wappalyzer](https://www.wappalyzer.com/)
  * [Firefox Plugin](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)
  * [Chrome Plugin](https://chromewebstore.google.com/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg)

## Websites

* [Shodan](https://www.notion.so/th4ntis/shodan.io/)
* [Fofa](https://en.fofa.info/)
* [Web-check.xyz](https://www.notion.so/th4ntis/web-check.xyz/)
* [Censys](https://search.censys.io/)
* [DNSDumpster](https://dnsdumpster.com/) - [DNSDumpster GitHub](https://github.com/nmmapper/dnsdumpster)
* [DNSTwist](https://dnstwist.it/)
* [HaveIBeenPwned](https://haveibeenpwned.com/)
* [BeenVerified](https://www.beenverified.com/)
* [Hunter.io](https://hunter.io/)
  * [Domain Search](https://hunter.io/domain-search)
  * [Email Finder](https://hunter.io/email-finder)
  * [Email Verifier](https://hunter.io/email-verifier)
* [Google Transparency Report](https://transparencyreport.google.com/)
* [IntelTechniques PasteBins](https://inteltechniques.com/osint/pastebins.html)
* [CertGrep](https://certgrep.sh/)

Using multiple websites also helps us find other ports and services running, and more. Be sure to note down:

* **A records** - map the network and identify potential targets for scanning or exploitation.
* **AAAA records** (if IPv6 infrastructure is being used).
* **MX records** - mail servers can be attack vectors.
* **NS records** - knowing authoritative DNS servers helps in DNS enumeration and potential DNS attacks.
* **TXT records.**
* **Subdomains** - often host different services or environments (dev, staging, etc.).
