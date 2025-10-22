# OWASP Zap

## About

[OWASP Zap](https://www.zaproxy.org/) is a security testing framework, like Burp Suite. It acts as a very robust enumeration tool and is used to test web applications. It’s completely open source, free, there is no premium version, no features are locked behind a paywall, and there is no proprietary code.

\***Note:** This section is currently still being updated.

There’s a couple of feature benefits too with using OWASP ZAP over Burp Suite:

* **Automated Web Application Scan**: This will automatically, passively, and actively, scan a web application, build a sitemap, and discover vulnerabilities. This is a paid feature in Burp.
* **Web Spidering**: You can passively build a website map with Spidering. This is a paid feature in Burp.
* **Unthrottled Intruder**: You can bruteforce login pages within OWASP as fast as your machine and the web-server can handle. This is a paid feature in Burp.
* **No need to forward individual requests through Burp**: When doing manual attacks, having to change windows to send a request through the browser, and then forward in burp, can be tedious. OWASP handles both and you can just browse the site and OWASP will intercept automatically. This is NOT a feature in Burp.

Some keyword translations from Burp to Zap(and vice versa)

&#x20;

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FEniLUICWJ64fccnFtUp7%252Fimage.png%3Falt%3Dmedia%26token%3D78e09a4d-1e42-4b97-b93c-8b447c110dfd&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4ce07d37&#x26;sv=2" alt=""><figcaption></figcaption></figure>

## Install

ZAP can be downloaded from [here](https://www.zaproxy.org/download/).

## Usage

### Automated Scans

We can click on Automated Scan&#x20;

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FbadvjQ2Inx2BkV3DrIEo%252Fimage.png%3Falt%3Dmedia%26token%3D38e4dc94-dcd7-455c-8987-0aaea063199d&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=cf18aac9&#x26;sv=2" alt=""><figcaption></figcaption></figure>

The automated scan performs both passive and automated scans to build a sitemap and detect vulnerabilities.

On the next page you may see the options to select either to use “traditional spider” or “Ajax spider”.

A traditional spider scan is a passive scan that enumerates links and directories of the website. It builds a website index without brute-forcing. This is much quieter than a brute-force attack and can still net a login page or other juicy details, but is not as comprehensive as a bruteforce.

The Ajax Spider is an add-on that integrates in ZAP a crawler of AJAX rich sites called Crawljax. You can use it in conjunction with the traditional spider for better results. It uses your web browser and proxy.

The easiest way to use the Ajax Spider is with HTMLUnit.

To install HTML Unit use the command

`sudo apt install libjenkins-htmlunit-core-js-java`

And then select HtmlUnity from the Ajax Spider Dropdown.

Both utilities can further be configured in the options menu (Ctrl+Alt+O)

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252Fk5jRHnu5IasU7JZH8lcb%252Fimage.png%3Falt%3Dmedia%26token%3D30250236-c2be-4f03-8e07-841d2c495e4a\&width=768\&dpr=4\&quality=100\&sign=aed4b14c\&sv=2)

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FKaoyn8QCYFry1xCw2CKh%252Fimage.png%3Falt%3Dmedia%26token%3De81c34b0-1711-4600-bfef-06a5543d58e1\&width=768\&dpr=4\&quality=100\&sign=9d7c3cd5\&sv=2)

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FeVem31vNCKHC49smPx70%252Fimage.png%3Falt%3Dmedia%26token%3D410c17c9-d660-4e00-9ec5-94b37b9b3931\&width=768\&dpr=4\&quality=100\&sign=b9021841\&sv=2)

### Brute Force Directories

If the passive scans are not enough, you can use a wordlist attack and directory bruteforce through ZAP just as you would with gobuster. This would pick up pages that are not indexed.

We navigate to Tools > Options > Forced Browse > Add Custom Forced Browse file&#x20;

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FV8FGinggnoBQL1A3CYn7%252Fimage.png%3Falt%3Dmedia%26token%3D975aaf60-d100-4edc-8cc2-788f091dd501&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c898fc69&#x26;sv=2" alt=""><figcaption></figcaption></figure>

From here, right click on site > Attack > Forced Browse Site&#x20;

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252F7IdWlVLJnHnL0Q0gc0om%252Fimage.png%3Falt%3Dmedia%26token%3D440d3dcf-84ea-4a51-912f-df24c90a940b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4de49953&#x26;sv=2" alt=""><figcaption></figcaption></figure>

We click the play button to begin&#x20;

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FetoyUWM3e8Ak5OM8yspA%252Fimage.png%3Falt%3Dmedia%26token%3D9731e431-4890-47ab-9d80-deed12194072&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7169eb87&#x26;sv=2" alt=""><figcaption></figcaption></figure>

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252F4Rf3JTiaGhzy0YY0mzPl%252Fimage.png%3Falt%3Dmedia%26token%3D752cd521-c239-4647-a2a5-ddea4fd34283\&width=768\&dpr=4\&quality=100\&sign=a152adc2\&sv=2)
