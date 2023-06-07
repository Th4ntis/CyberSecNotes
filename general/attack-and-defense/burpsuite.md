# BurpSuite

[BurpSuite](https://portswigger.net/burp) is industry standard tool for web application hacking, and is essential in any web pentest. Free community edition can be downloaded from [here](https://portswigger.net/burp/communitydownload).&#x20;

Plenty of good info and hands on from the [TryHackMe modules](https://tryhackme.com/module/learn-burp-suite).



\*Note: This section is currently still being updated.

## Setup

### Browser Setup

We can install [FoxyProxy](https://foxyproxy.com/) Standard to setup for easy proxy to pass traffic through Burpsuite.

* [Chrome](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)
* [Firefox](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)

With FoxyProxy installed we can right click on the extension > Options

&#x20;

![](<../../.gitbook/assets/image (335).png>)

Add new Proxy

![](<../../.gitbook/assets/image (341).png>)

From here, we add the IP to be our machine `127.0.0.1`, and the port to `8080`&#x20;

Then click on the General tab at the tab and give this a name, like Burp or Burpsuite or something.&#x20;

![](<../../.gitbook/assets/image (388).png>)

Click Save and ta-da!

From here, when we want to use BurpSuite, we can click on the extension icon and select our Burp proxy

![](<../../.gitbook/assets/image (6) (1) (2).png>)

## Usage

With our browser proxy setup, when we open Burpsuite we can choose a temporary project, or if we have the professional edition we can open exiting projects.

![](<../../.gitbook/assets/image (68).png>)

When we're ready to start intercepting our traffic, we can go to the proxy tab, and turn on intercept.

![](<../../.gitbook/assets/image (7) (2) (1).png>)

**\*NOTE** - This will intercept ALL browser traffic. If we want to intercept only specific IPs or websites, we need to setup our scope.

### Scope

Setting a scope for the project allows us to define what gets proxied and logged. We can restrict Burp Suite to _only_ target the web application(s) that we want to test. We can set our scope by Selecting: `Target > Scope`

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

To do this switch over to the "Target" tab, right-click our target from the list on the left, then choose "Add To Scope". Burp will then ask us whether we want to stop logging anything which isn't in scope, we want to choose yes.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

The scope will be sure to only intercept traffic to the specific IPs or websites.

or we can manually add them: `Target > Scope Settings > Include in Scope > Add`

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

We chose to disable _logging_ for out of scope traffic, but the proxy will still be intercepting everything. So lets turn that off. Proxy > Options/Proxy Settings > Select "AND | URL | Is in target scope". The proxy will completely ignore anything that isn't in the scope, cleaning up the traffic coming through Burp.

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

### HTTPS Traffic

If we want to intercept HTTPS traffic, we need to do a couple extra steps. When we attempt to, we're met with

<figure><img src="../../.gitbook/assets/image (1) (1) (3).png" alt=""><figcaption></figcaption></figure>

Telling us that the PortSwigger certificate isn't authorized to secure the connection. To fix this: with the proxy activated head to [http://burp/cert](http://burp/cert), this will download a file called `cacert.der`.

With that file saved to your machine, open your Firefox setting, then search the page for "certificates" to find the option to "View Certificates" OR under "Privacy & Security" we can view the certificates.

<figure><img src="../../.gitbook/assets/image (40) (2).png" alt=""><figcaption></figcaption></figure>

Select "View Certificates" and under the "Authorities" tab, we can import a new cert.

<figure><img src="../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

Select "Trust this CA to identify websites" and click OK.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

and we're set.

### Burp Browser

There IS an option to start and use the Burp Browser that opens a Chromium window that makes all traffic go through burp without any extra setup, this is not super commonly used to my knowledge as most people prefer to use their browser of choice.

To get to this: `Proxy > Intercept > Open Browser`

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

