# OWASP Zap

## About

[OWASP Zap](https://www.zaproxy.org/) is a security testing framework, like Burp Suite. It acts as a very robust enumeration tool and is used to test web applications. It’s completely open source, free, there is no premium version, no features are locked behind a paywall, and there is no proprietary code.

**\*Note:** This section is currently still being updated.

There’s a couple of feature benefits too with using OWASP ZAP over Burp Suite:

* **Automated Web Application Scan**: This will automatically, passively, and actively, scan a web application, build a sitemap, and discover vulnerabilities. This is a paid feature in Burp.&#x20;
* **Web Spidering**: You can passively build a website map with Spidering. This is a paid feature in Burp.
* **Unthrottled Intruder**: You can bruteforce login pages within OWASP as fast as your machine and the web-server can handle. This is a paid feature in Burp.
* **No need to forward individual requests through Burp**: When doing manual attacks, having to change windows to send a request through the browser, and then forward in burp, can be tedious. OWASP handles both and you can just browse the site and OWASP will intercept automatically. This is NOT a feature in Burp.&#x20;

Some keyword translations from Burp to Zap(and vice versa)

![](<../../../.gitbook/assets/image (54).png>)

## Install

ZAP can be downloaded from [here](https://www.zaproxy.org/download/).

## Usage

### Automated Scans

We can click on Automated Scan\


![](<../../../.gitbook/assets/image (411).png>)

The automated scan performs both passive and automated scans to build a sitemap and detect vulnerabilities.

On the next page you may see the options to select either to use “traditional spider” or “Ajax spider”.\


A traditional spider scan is a passive scan that enumerates links and directories of the website. It builds a website index without brute-forcing. This is much quieter than a brute-force attack and can still net a login page or other juicy details, but is not as comprehensive as a bruteforce.\


The Ajax Spider is an add-on that integrates in ZAP a crawler of AJAX rich sites called Crawljax. You can use it in conjunction with the traditional spider for better results. It uses your web browser and proxy.\


The easiest way to use the Ajax Spider is with HTMLUnit. \


To install HTML Unit use the command

`sudo apt install libjenkins-htmlunit-core-js-java`

And then select HtmlUnity from the Ajax Spider Dropdown.&#x20;

Both utilities can further be configured in the options menu (Ctrl+Alt+O)

![](<../../../.gitbook/assets/image (59).png>)

![](<../../../.gitbook/assets/image (396).png>)

![](<../../../.gitbook/assets/image (409).png>)

### Brute Force Directories

If the passive scans are not enough, you can use a wordlist attack and directory bruteforce through ZAP just as you would with gobuster. This would pick up pages that are not indexed.

We navigate to Tools > Options > Forced Browse > Add Custom Forced Browse file

![](<../../../.gitbook/assets/image (417).png>)

From here, right click on site > Attack > Forced Browse Site

![](<../../../.gitbook/assets/image (448).png>)

We click the play button to begin

![](<../../../.gitbook/assets/image (295).png>)

![](<../../../.gitbook/assets/image (14) (3).png>)
